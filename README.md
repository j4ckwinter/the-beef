# the beef

i work across a few repos. this is where i start when the work spans more than one of them, or when i'm not sure which one it belongs to. an agent can find the right project without me explaining the whole setup every time.

for work inside one project, start the session in that project. the agent gets that repo's instructions, git state and history without being told where to look.

to start here, open an agent session and say what you want to work on. [AGENTS.md](AGENTS.md) is the entry point. if your client doesn't load it automatically, ask it to read that file first.

> read AGENTS.md, then look at pancake stack and its evals. explain how the package checks work across the two. keep it read-only.

## what's here

- [AGENTS.md](AGENTS.md): where to start and where the projects live.
- [steering](steering/working-preferences.md): how i like to work.
- [wiki](wiki/pancake-stack.md): what no single project can own. how the projects relate, and how things are set up on my machine.

[Pancake Stack](https://github.com/j4ckwinter/pancake-stack) supplies the workflows. this repo doesn't duplicate them. personal skills can come later if there's something the shared plugin doesn't cover.

## where it lives

keep this checkout beside the projects it describes:

```text
dev/
├── the-beef/
├── pancake-stack/
├── pancake-stack-evals/
└── elvis/
```

paths in the project map are relative to this repo. links inside wiki pages are relative to the page itself. the sibling links work locally; use the source links for browsing on GitHub.

## steering everywhere

steering should reach a session wherever it starts. in Claude Code, `~/.claude/CLAUDE.md` imports both files:

```text
@~/dev/the-beef/steering/working-preferences.md
@~/dev/the-beef/steering/coding-standards.md
```

the import breaks if this checkout moves. only Claude Code is wired up this way. in other hosts the steering is read in a session that starts here.

## keep it useful

if a project's own repo could hold a fact, that's where it belongs, and the wiki links to it. the wiki can go stale. project instructions and code are the place to verify what is true now.

keep lasting facts and useful gotchas here, with links to where they came from. release notes, task history and raw logs belong elsewhere.
