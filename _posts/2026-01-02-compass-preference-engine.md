---
layout: post
title:  "Compass: Preferences for LLM-Assisted Coding"
date: 2026-01-02
---

I spent the holiday break pulling together a tool I've wanted for a while: **Compass**. Large language models can crank out code in seconds, but coaching them into _my_ style takes way more prompting than I like. Compass gives me a declarative way to describe those preferences and enforce them automatically.

## Why build Compass?

Every time I collaborate with an LLM I end up repeating the same flavor of feedback. Rather than write it out over and over, Compass lets me encode the expectations as [Tree-sitter](https://tree-sitter.github.io/tree-sitter/) queries inside a TOML config. When I run `compass <file>` it parses the file, applies my rules, and emits JSON with a score plus the issues the LLM needs to fix.

If you’re new to Tree-sitter, it’s an incremental parsing library that powers a lot of modern editors. This [excellent intro talk](https://www.youtube.com/watch?v=Jes3bD6P0To) breaks down how it works and why it’s perfect for structural code analysis.

## How it works

The CLI auto-detects `.rs`, `.go`, `.js`, and `.jsx` files. If you run it without a config, it uses the bundled preferences in `config/config.toml`:

```bash
compass src/main.rs
```

Each rule in that file is a `[[rules]]` entry. Here’s a simple example that enforces “`match` arms should delegate to helpers” in Rust:

```toml
[[rules]]
name = "large_match_prefer_functions"
language = "rust"
query = '''
(match_expression
  body: (match_block
    (match_arm value: (block) @body)
  )
) @match
'''
severity = "info"
message = "Match arm contains inline logic"
suggestion = "Extract helper functions per arm."
weight = 1.5
enabled = true
```

Tree-sitter does the heavy lifting. If you’d rather enforce custom patterns, just prompt your favorite LLM with _“write a Tree-sitter query that finds Go functions with 6+ parameters”_, drop the output into the config, and rerun Compass.

## Designed to be LLM-friendly

The JSON output is easy for scripts or chat bots to digest:

```json
{
  "score": 7.3,
  "rating": "Fair",
  "issues": [
    {
      "rule": "go_missing_error_check",
      "severity": "Warning",
      "line": 42,
      "message": "Potential unchecked error",
      "suggestion": "Follow this assignment with `if err != nil`."
    }
  ]
}
```

I feed that straight back into my LLM loop. If the score isn’t high enough, I tell the model _why_ using the `message` / `suggestion` fields and let it iterate until Compass shuts up.

## Next steps

Right now Compass handles Rust, Go, JavaScript/JSX, and Zig. Adding another language follows a repeatable playbook:

1. Pull in the Tree-sitter grammar crate for that language.
2. Teach the CLI how to route file extensions to that grammar.
3. Add `language = "python"` (or whatever) rules to the config that reflect your house style.

To prove it out, I added Zig support by calibrating against [zjvm](https://github.com/lyledean1/zjvm), my JVM-in-Zig side project. The steps were:

- Add `tree-sitter-zig` to the dependencies and wire `.zig` files through the CLI.
- Encode the idioms I already follow in zjvm: don’t call `@panic` and avoid `catch unreachable`.
- Run `compass zjvm/src/main.zig` and iterate until the score hit 10/10.

It only took a couple of config tweaks for Compass to understand Zig well enough to keep zjvm honest. That’s the extensibility I’m aiming for: if I can teach Compass to enforce my own conventions, it’s easy to hand the same rules to an LLM.

I’m already drafting some TypeScript and Python preferences, and I’m curious how far I can push the “LLM writes its own rules” idea. If you try Compass, let me know what you teach it!
