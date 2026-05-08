---
layout: post
title:  "It’s the Model"
date: 2026-05-08
---

My current coding workflow increasingly revolves around agents.

- agents.md
- orchestration loops
- MCP servers
- memory systems
- recursive planning

But beneath the layers of tooling and orchestration, the center of gravity is the model.

My coding life now exists in constant tension between how I want code written and how the model wants to write it.

I tell it:

- make the smallest possible change
- don’t refactor unrelated code
- preserve the structure
- avoid abstractions
- just fix the bug

And without the guard rails I’ve put in place, it responds like an ambitious engineer trying to improve the entire system:

- introducing interfaces
- reorganizing files
- abstracting early
- “cleaning up” architecture
- touching code that didn’t need touching

This has increasingly become my experience of AI coding. It almost feels less like giving instructions and more like negotiating with the model.

Prompts are negotiations.

## The Agent Is Mostly the Model

Agents matter.

Retrieval matters.
Tools matter.
Memory matters.
Diffing, retries, and orchestration all matter.

As the Amp team put it in ["The Coding Agent Is Dead"](https://ampcode.com/news/the-coding-agent-is-dead):

> “the agent is no longer the bottleneck”

Systems shape reliability, but the underlying intelligence still comes from the model.

The model is still the thing that:

- understands intent
- plans changes
- synthesizes abstractions
- writes code
- debugs
- decides what matters

Without a strong model, the rest is plumbing.

That’s why weak models with sophisticated agents still feel brittle, while strong models with thin wrappers feel surprisingly capable.

And as models get stronger, the interaction starts to feel strange.

You stop feeling like you’re programming a machine.

You start feeling like you’re collaborating with an engineer who already has opinions.

Usually strong ones.

You want:

- minimalism
- surgical edits
- local fixes

The model wants:

- generalization
- cleaner architecture
- systemic consistency

And sometimes the model is right.

That’s the uncomfortable part.

The best AI coding sessions no longer feel like command execution.

They feel like managing a very fast, very opinionated engineer who has read most of GitHub.

## Less Prompting, More Teaching

Most AI coding workflows today are built around resistance.

You prompt the model.
Then constrain it.
Then lint it.
Then review it.
Then add another instruction file to stop it from doing what it keeps trying to do.

That works, but it feels temporary.

Because the deeper problem is alignment, not orchestration.

The model already has a learned sense of what “good engineering” looks like.

The real challenge is teaching it:

- how your team thinks
- what your repository values
- which tradeoffs you prefer
- what “clean” means in your context

The next generation of AI coding tools will not just be better at generating code.

They’ll be better at learning taste.

Not through more guard rails or increasingly elaborate instruction files, but through systems that gradually understand how you think and why you make the decisions you do.

Because eventually, the best coding models will already understand the tradeoffs you care about.

They’ll already understand what good looks like in your environment.

Less fighting.

More teaching.