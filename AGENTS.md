# the-beef

This is Jack Winter's home repo for coding agents. Start sessions here. Skills and standing rules live in this checkout. Other projects stay in their own repositories and are cloned only when a task needs them.

Before working in any repo, including this one, read `skills/` and `steering/`.

## Jack

Jack Winter is a London-based senior frontend engineer. His public portfolio in winterbot describes 8+ years building customer-facing products with React and TypeScript, specialising in real-time interfaces and browser performance, and open-source tools for AI coding agents.

He develops on a Mac and a Windows PC. Local models run through Ollama on the Windows machine.

## How to work

- Read the skill that matches the task. `skills/pancake/SKILL.md` is the general entry for getting work done. `skills/scope`, `skills/design`, `skills/challenge`, and `skills/verify` cover scoping a change, planning it, stress-testing a design, and proving a fix. The other folders under `skills/` are the rest of that same set. See `skills/ATTRIBUTION.md` for where they came from.
- Follow `steering/code-style.md`, `steering/testing.md`, and `steering/commits-and-prs.md`. When the repo you are editing has its own `AGENTS.md` or `CLAUDE.md`, that file wins for that repo.
- Match the code, formatter, package manager, and recent commits already in the repo. Leave a gap as a gap rather than inventing a house rule to fill it.
- Stay inside the requested change. Publishing, deploying, merging, and global tool configuration need an explicit request.
- Clone a repo below only when the task needs it. If `~/repos/<name>` already exists, use that checkout.
- There is no wiki. Do not add one unless Jack asks.

## Repos

- For brain-cache, clone j4ckwinter/brain-cache to ~/repos/brain-cache. Local context engine for Claude Code: it indexes a codebase with AST-aware chunking so retrieval returns relevant chunks instead of whole files. Default branch is `master`.
- For pancake-stack, clone j4ckwinter/pancake-stack to ~/repos/pancake-stack. The skills Jack uses so agents write code he wants to keep.
- For pancake-stack-evals, clone j4ckwinter/pancake-stack-evals to ~/repos/pancake-stack-evals. Checks, comparisons, and recorded results for whether those skills help.
- For panky, clone j4ckwinter/panky to ~/repos/panky. A local-model AI teammate that runs on his PC and on his phone, with saved chats and a Pancake UI interface.
- For pancake-ui, clone j4ckwinter/pancake-ui to ~/repos/pancake-ui. Reusable React components, compiled styles, and design tokens for web apps.
- For fantasy-pancake, clone j4ckwinter/fantasy-pancake to ~/repos/fantasy-pancake. A Next.js app for picking Fantasy Premier League transfers, with no login and no automatic transfers.
- For deedspan, clone j4ckwinter/deedspan to ~/repos/deedspan. A TypeScript SDK for exposing application actions to agents, while the application keeps permissions, approvals, and saved data.
- For winterbot, clone j4ckwinter/winterbot to ~/repos/winterbot. An explorable portfolio town built with Astro, Preact, and TypeScript, plus a plain portfolio of the same content.
- For fpl-radar, clone j4ckwinter/fpl-radar to ~/repos/fpl-radar. Private repository. Clone it only when the task needs it, and do not copy anything from it into this public repo.
- For padel-potato, clone j4ckwinter/padel-potato to ~/repos/padel-potato. An Expo and React Native app for organising padel games with friends.
