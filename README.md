# the-beef

Home repo for Jack Winter's coding agents. One checkout holds the skills and the standing rules. Agents are started here, then sent to other repositories when a task needs them.

This follows Matt Pocock's [home repo](https://x.com/mattpocockuk/status/2120260969750540327) pattern: steering and tooling live in one place, there is a single directory to run agents from, and one session can work across repos.

## Use it

Clone this repo to `~/repos/the-beef` and start the agent in that directory.

`AGENTS.md` is the entry point. It says who Jack is, how he wants agents to work, and where to clone each project:

```text
For brain-cache, clone j4ckwinter/brain-cache to ~/repos/brain-cache.
```

The same shape covers the rest of the list. The agent should read `skills/` and `steering/` before editing any repo.

| Path | What it is |
| --- | --- |
| `AGENTS.md` | Session brief and clone pointers. |
| `skills/` | Agent workflows copied from [pancake-stack](https://github.com/j4ckwinter/pancake-stack), so this repo stands on its own. `skills/ATTRIBUTION.md` records the source commit. |
| `steering/` | Standing rules for code style, verification, and commits, taken from conventions already visible in Jack's repos. |

Other projects stay in their own git history. Clone one under `~/repos/` when the work needs it, and follow that repo's own `AGENTS.md` or `CLAUDE.md` while you are there. There is no wiki in this repo.
