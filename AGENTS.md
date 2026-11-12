# the-beef

This is Jack Winter's home repo for coding agents. Start sessions here. Standing rules live in this checkout. Workflows come from the Pancake Stack plugin, which stays in its own repo. Other projects are cloned only when a task needs them.

Before working in any repo, including this one, read `steering/`. Use the Pancake Stack plugin for the task workflow.

## Jack

Jack Winter is a London-based senior frontend engineer. His public portfolio in winterbot describes 8+ years building customer-facing products with React and TypeScript, specialising in real-time interfaces and browser performance, and open-source tools for AI coding agents.

He develops on a Mac and a Windows PC. Local models run through Ollama on the Windows machine.

## How to work

- Follow `steering/code-style.md`, `steering/testing.md`, and `steering/commits-and-prs.md`. When the repo you are editing has its own `AGENTS.md` or `CLAUDE.md`, that file wins for that repo.
- Match the code, formatter, package manager, and recent commits already in the repo. Leave a gap as a gap rather than inventing a house rule to fill it.
- Stay inside the requested change. Publishing, deploying, merging, and global tool configuration need an explicit request.
- Clone a repo below only when the task needs it. If `~/repos/<name>` already exists, use that checkout.
- There is no wiki, and no copy of the Pancake Stack skills in this repo. Do not add either unless Jack asks.

## Pancake Stack

The daily workflows are the [pancake-stack](https://github.com/j4ckwinter/pancake-stack) plugin, packaged for Claude Code and Codex. Clone it first: `~/repos/pancake-stack`, which is `../pancake-stack` when this repo is `~/repos/the-beef`.

`.claude/settings.json` registers that checkout as a local marketplace and enables `pancake-stack@pancake-stack`. Claude Code reads the plugin from the checkout after this folder is trusted. The shell command needs `./`, not a bare `.`.

If Claude Code reports that the plugin is enabled here but not installed, run this once from `~/repos/pancake-stack`:

```sh
claude plugin marketplace add ./
claude plugin install pancake-stack@pancake-stack
```

Codex copies the plugin into its own cache. From `~/repos/pancake-stack`, install once:

```sh
codex plugin marketplace add .
codex plugin add pancake-stack@pancake-stack
```

After pulling pancake-stack, run `codex plugin add pancake-stack@pancake-stack` again. A pull on its own does not refresh the Codex cache. Claude Code picks up checkout edits at the next session or after `/reload-plugins`.

In Claude Code the skills are `/pancake-stack:<skill>`. In Codex they are `$pancake-stack:<skill>`. `pancake` is the general entry. `scope`, `challenge`, and `verify` cover scoping a change, stress-testing a design, and proving a fix. The other names are the rest of that set, listed in the pancake-stack README.

On a host that does not load either plugin, read `~/repos/pancake-stack/skills/<skill>/SKILL.md`. Leave those files in that repo.

## Repos

- For brain-cache, clone j4ckwinter/brain-cache to ~/repos/brain-cache. Local context engine for Claude Code: it indexes a codebase with AST-aware chunking so retrieval returns relevant chunks instead of whole files. Default branch is `master`.
- For pancake-stack, clone j4ckwinter/pancake-stack to ~/repos/pancake-stack. The Claude Code and Codex plugin for the workflows above.
- For pancake-stack-evals, clone j4ckwinter/pancake-stack-evals to ~/repos/pancake-stack-evals. Checks, comparisons, and recorded results for whether those skills help.
- For panky, clone j4ckwinter/panky to ~/repos/panky. A local-model AI teammate that runs on his PC and on his phone, with saved chats and a Pancake UI interface.
- For pancake-ui, clone j4ckwinter/pancake-ui to ~/repos/pancake-ui. Reusable React components, compiled styles, and design tokens for web apps.
- For fantasy-pancake, clone j4ckwinter/fantasy-pancake to ~/repos/fantasy-pancake. A Next.js app for picking Fantasy Premier League transfers, with no login and no automatic transfers.
- For deedspan, clone j4ckwinter/deedspan to ~/repos/deedspan. A TypeScript SDK for exposing application actions to agents, while the application keeps permissions, approvals, and saved data.
- For winterbot, clone j4ckwinter/winterbot to ~/repos/winterbot. An explorable portfolio town built with Astro, Preact, and TypeScript, plus a plain portfolio of the same content.
- For fpl-radar, clone j4ckwinter/fpl-radar to ~/repos/fpl-radar. Private repository. Clone it only when the task needs it, and do not copy anything from it into this public repo.
- For padel-potato, clone j4ckwinter/padel-potato to ~/repos/padel-potato. An Expo and React Native app for organising padel games with friends.
