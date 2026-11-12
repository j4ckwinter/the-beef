# the-beef

This is Jack Winter's home repo for coding agents. Start sessions here. Standing rules live in this checkout. Workflows come from the Pancake Stack plugin. Other projects are cloned only when a task needs them, and only after they are listed under Repos.

Before working in any repo, including this one, read `steering/`. Use the Pancake Stack plugin for the task workflow.

## Jack

Jack Winter is a London-based senior frontend engineer with 8+ years building customer-facing products in React and TypeScript. He specialises in real-time interfaces, browser performance, and tools for AI coding agents.

He develops on a Mac and a Windows PC. Local models run through Ollama on the Windows machine.

## How to work

- Follow `steering/code-style.md`, `steering/testing.md`, and `steering/commits-and-prs.md`. When the repo you are editing has its own `AGENTS.md` or `CLAUDE.md`, that file wins for that repo.
- Match the code, formatter, package manager, and recent commits already in the repo. Leave a gap as a gap rather than inventing a house rule to fill it.
- Stay inside the requested change. Publishing, deploying, merging, and global tool configuration need an explicit request.
- Clone a repo from the list below only when the task needs it. If `~/repos/<name>` already exists, use that checkout.
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

## Adding a repo

Add a project here only when Jack asks. Edit this file. Append one bullet to the Repos list. Do not create a directory, a wiki page, or a copy of that repo's files in the-beef.

Use this form, as its own bullet:

```text
- For <name>, clone <owner>/<repo> to ~/repos/<name>. <one sentence.>
```

`<name>` is the directory under `~/repos/`. `<owner>/<repo>` is the GitHub repository. End the clone sentence with a full stop, then one sentence of description.

Read that repo's README or code and take the sentence from there. Do not invent it. If the default branch is not `main`, say so in that same bullet.

A private repo gets the clone line and a neutral sentence that does not come from inside the repo. Copy nothing from a private repo into this public one.

Leave the Repos list otherwise unchanged. Commit the new bullet when Jack asks for the change.

## Repos

- For pancake-stack, clone j4ckwinter/pancake-stack to ~/repos/pancake-stack. Claude Code and Codex plugin for the workflows above.
