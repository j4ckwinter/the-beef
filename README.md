# the-beef

Home repo for Jack Winter's coding agents. Start the agent here. Standing rules live in this checkout. The workflows stay in the Pancake Stack plugin, which is packaged for Claude Code and Codex.

This follows Matt Pocock's [home repo](https://x.com/mattpocockuk/status/2120260969750540327) pattern: steering in one place, one directory to run agents from, and one session can work across repos.

## Use it

Clone this repo to `~/repos/the-beef` and clone [pancake-stack](https://github.com/j4ckwinter/pancake-stack) to `~/repos/pancake-stack`. Start the agent in `the-beef`.

Read `steering/` before editing any repo. For a workflow, use the plugin rather than a copy of its files.

Claude Code loads it from the sibling checkout. `.claude/settings.json` points at `../pancake-stack` and enables `pancake-stack@pancake-stack`. If a session says the plugin is not installed, run this from `~/repos/pancake-stack`:

```sh
claude plugin marketplace add ./
claude plugin install pancake-stack@pancake-stack
```

Codex installs a cached copy. From the same checkout:

```sh
codex plugin marketplace add .
codex plugin add pancake-stack@pancake-stack
```

Skills are `/pancake-stack:<skill>` in Claude Code and `$pancake-stack:<skill>` in Codex.

| Path | What it is |
| --- | --- |
| `AGENTS.md` | Session brief, Pancake Stack install, and the repo list. |
| `.claude/settings.json` | Enables the Pancake Stack plugin from `~/repos/pancake-stack`. |
| `steering/` | Standing rules for code style, verification, and commits. |

Other projects stay in their own git history. There is no wiki in this repo.

## Add a repo

The Repos list in `AGENTS.md` starts with pancake-stack only. Add the next project there when you want an agent to know about it.

Append one bullet:

```text
- For <name>, clone <owner>/<repo> to ~/repos/<name>. <one sentence.>
```

`<name>` is the folder under `~/repos/`. The sentence comes from that repo's own README or code. A private repo gets the clone line and a neutral sentence, and nothing from inside it is copied here. Do not add a wiki page or a second copy of the project.
