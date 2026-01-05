---
layout: post
title:  "Who's Flying the Plane? Coding with AI"
date: 2026-01-05
---

We used to fly with a yoke and rudder pedals. Every line of code was a deliberate adjustment—pull back to climb, push forward to dive, careful pressure on the pedals to keep things coordinated. You felt every detail of the aircraft through your fingertips.

Now? Now we're drifting.

I've been using ChatGPT and other models since they first came out—asking questions, debugging errors, generating snippets. But 2025 changed everything. AI went from being a helpful reference to an active participant in the development loop. Tools like Claude Code and Codex don't just answer questions; they read your files, run your tests, edit your code, and maintain context across hours-long sessions.

## The New Cockpit

Coding with AI isn't about typing every character anymore. It's about momentum, direction, and making smooth corrections at altitude. You're still flying the plane—don't mistake that—but the controls have fundamentally changed.

Takeoff is everything. That first prompt, that initial context you give AI, determines whether you're going to climb smoothly or struggle to get off the ground. A good takeoff means being clear about your destination: "We're building a REST API with authentication, using TypeScript and PostgreSQL." AI needs heading, altitude, and speed. Vague directions like "make me an app" are like shoving the throttle forward and hoping.

Once you're airborne, your job is navigation, not manipulation. You're not controlling every detail anymore. You're checking: Are we still heading toward our destination? Is the code maintaining altitude—solving the actual problem rather than drifting into abstraction? Are we building up dangerous technical debt like ice on the wings?

## The Drift

Here's what's different: abrupt movements are dangerous now.

In the old days, if you wrote bad code, you knew it immediately. You typed it. You saw the error. You fixed it. Cause and effect were direct.

With AI, you can ask for a feature and get 300 lines of code that looks right. Compiles clean. Runs without errors. But six changes later, you realize the architecture is tangled, the patterns are inconsistent, and you can't remember which parts you wrote versus which parts AI generated versus which parts are some messy hybrid of both.

This is the drift. And if you overcorrect—if you keep yanking the controls with contradictory prompts, major refactors, shifting requirements—you can put the codebase into a spin that's genuinely hard to recover from. AI will gamely try to comply with each request, but code has momentum. Change the authentication pattern halfway through and suddenly you've got two different systems trying to coexist.

## Your Instruments

This is where the analogy gets powerful: your tools are your instruments, and they're what keep you from flying blind.

A pilot without instruments is helpless in clouds. They can't tell if they're climbing or diving, turning or flying straight. Spatial disorientation is real, and it's killed experienced pilots who stopped trusting their instruments.

When you're coding with AI, you need instruments:

**Tests** tell you if you're maintaining altitude — if the code still does what it's supposed to do. AI might generate something that looks elegant, but if things are breaking, you're losing altitude fast.

**Linters and type checkers** keep you oriented — they show you when the code is consistent, when it's following good patterns, when things are starting to tilt dangerously even when everything feels fine. I built [Compass](https://github.com/lyledean1/compass) for this exact reason—a linter that enforces my coding preferences on LLM-generated code using Tree-sitter queries.

**Your debugger** helps you triangulate — when you're lost, when AI has taken you somewhere you don't recognize, you can step through the code, watch what's actually happening, figure out where you are.

**Version control** is your black box recorder — when something goes wrong, you need to know what changed. AI doesn't remember what it wrote yesterday. Your commit history does.

Without these instruments, you're flying blind. And in the clouds of AI-generated code, that's when pilots crash.

## You Still Need to Know How to Fly

Here's the uncomfortable truth: if you don't know how to pilot, you're going to crash.

AI can get you airborne. It can handle smooth air and clear skies. But it's not actually flying the plane—you are. And when things go wrong, you need to know what to do.

You need to recognize when AI-generated code is architecturally unsound, even if it runs. You need to spot the subtle bug, even if the syntax is perfect. You need to understand why things are failing, not just ask AI to fix them until they pass.

The crash comes gradually, then all at once. Someone who doesn't know how to code might build something impressive with AI. For a while, it works. They keep adding features. AI keeps generating code.

But technical debt is accumulating. The architecture is inconsistent. There are subtle bugs they can't see. And then one day, they need to make a change that should be simple, but it breaks three other things. They ask AI to fix it. It breaks two more. They're in a spin, the ground is rushing up, and they don't know how to recover because they never learned to fly.

## The Skill Has Changed, Not Disappeared

The really good developers I know who work with AI. They're better at using it because they know how to code, not despite it.

They can read the generated code and immediately spot the problems. They know which prompts will lead to maintainable architecture and which will create a mess. They trust their instruments. They make smooth corrections. They know when to take manual control.

AI is an extraordinary copilot. It can handle routine tasks, suggest solutions, even navigate complex problems. But it's not the pilot. It doesn't understand the mission. It doesn't know when to abort. It doesn't feel the plane getting too slow or too fast.

You're still flying. The controls are just different now.
