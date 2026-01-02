---
layout: post
title:  "MCC: Multiplayer Mode for Claude Code"
date: 2026-01-02
---

It's 1am. Production is down. You've been debugging with Claude Code for two hours and you've found something—maybe not the root cause, but a solid lead. Your teammate Slacks you: "I've got a different theory, let me take a look."

You could copy-paste your conversation history. You could write up what you've tried. Or you could just hand them your entire Claude Code session—every message, every file change, every debugging step—and let them pick up exactly where you left off.

That's why I built [**MCC**](https://github.com/lyledean1/mcc).

## The problem

Claude Code is incredible for debugging. It reads files, runs commands, edits code, and maintains full context across a conversation that can span hours. But that context lives in `~/.claude/projects/` on your machine, locked in JSONL files that aren't designed to be shared.

When you need to hand off to a teammate—whether it's a production fire or just a complex feature—you lose all that accumulated context. They start fresh, and you waste time explaining what you've already explored.

## The solution

MCC makes sharing Claude Code sessions dead simple:

```bash
# You
cd /my/project
mcc export

# Send the file to your teammate via Slack/email

# Teammate
cd /my/project
mcc import mcc-export.json.gz
claude
/resume
```

That's it. They see your full debugging session and continue from there.

## What gets shared

When you export a session, MCC packages:

- **Full conversation history** - Every message and response
- **Tool call results** - File reads, edits, bash commands
- **File snapshots** - State of modified files
- **Git context** - Branch info and working directory
- **Session metadata** - When exported, by whom

When your teammate imports it, MCC rewrites paths to match their local environment and registers the session with Claude Code. They open `claude`, hit `/resume`, and they're in.

## How it works

MCC reads Claude Code's session files from `~/.claude/projects/`, which are stored as JSONL (one JSON object per line). Each line is a message object containing the conversation, tool calls, and metadata.

The export process:
1. Finds the most recent session for your current directory
2. Packages all messages into a single JSON structure
3. Compresses it with gzip (typically 10-50KB)
4. Saves to current directory as `mcc-export.json.gz`

The import process:
1. Decompresses the file
2. Rewrites `cwd` and path references to match the target directory
3. Creates a new session file in `~/.claude/projects/`
4. Registers it in `~/.claude.json` so it appears in `/resume`

Path rewriting is critical—your `/Users/alice/myapp` needs to become `/Users/bob/myapp` on import. MCC handles this automatically.

## Optional: Cloud storage

For teams that want seamless sharing without manual file transfer, MCC supports Google Cloud Storage:

```bash
mcc config set-bucket gs://my-team-sessions
mcc share mcc-export.json.gz
# Teammate: mcc fetch gs://my-team-sessions/mcc-export.json.gz
```

But honestly? Start with local files. Drag and drop a file in Slack. The friction is minimal and you don't need infrastructure.

## Try it!

If you use Claude Code for debugging, especially in team settings, [give MCC a try](https://github.com/lyledean1/mcc). It's open source and the whole thing is under 1000 lines of Rust.

And if you're ever debugging something at 1am—may your sessions be short and your teammates be nearby.
