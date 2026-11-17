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
├── elvis/
├── panky/
├── pancake-ui/
└── winterbot/
```

i use two machines, a Mac and a Windows PC. not every project is on both: Elvis and Pancake UI are Mac only, Panky runs on the PC, and winterbot has only been checked on the Mac. each wiki page says which machine it describes.

paths in the project map are relative to this repo. links inside wiki pages are relative to the page itself. the sibling links work locally; use the source links for browsing on GitHub.

## steering everywhere

steering should reach a session wherever it starts. in Claude Code, `~/.claude/CLAUDE.md` imports both files:

```text
@~/dev/the-beef/steering/working-preferences.md
@~/dev/the-beef/steering/coding-standards.md
```

that's the Mac. on the Windows PC the checkout is under `Documents`, so the same file there reads:

```text
@~/Documents/dev/the-beef/steering/working-preferences.md
@~/Documents/dev/the-beef/steering/coding-standards.md
```

the import breaks if this checkout moves. only Claude Code is wired up this way. in other hosts the steering is read in a session that starts here.

## make your own

this one's mine, so the wiki and the project map won't mean much to you. the shape is the useful bit. to start your own:

1. copy or fork it, then empty `wiki/` and clear the project map in [AGENTS.md](AGENTS.md).
2. read the [working preferences](steering/working-preferences.md) and [coding standards](steering/coding-standards.md). keep what you agree with and rewrite the rest. they talk about me by name, so make them about you.
3. put the checkout beside your projects and add a row to the project map for each one. give a project a wiki page only for what its own repo can't hold.
4. point your agent at the steering from its user-level instructions, like the `CLAUDE.md` imports above, with your own paths.

the workflows come from [Pancake Stack](https://github.com/j4ckwinter/pancake-stack), so grab that too.

## keep it useful

if a project's own repo could hold a fact, that's where it belongs, and the wiki links to it. the wiki can go stale. project instructions and code are the place to verify what is true now.

keep lasting facts and useful gotchas here, with links to where they came from. release notes, task history and raw logs belong elsewhere.

## licence

[MIT](LICENSE). take whatever's useful.
