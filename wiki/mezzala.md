# mezzala on this Mac

mezzala is an MCP server for Football Manager 27. It reads a career save with [fmsave](https://github.com/rhiever/fmsave), keeps a snapshot each time the save changes, and answers transfer questions through seven tools. It came out of the idea queue as "poacher", was renamed, and Jack asked for it to be built directly on 24 November 2026, rather than in a queue build. Its checkout is `../mezzala`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../mezzala/AGENTS.md) and [README](../../mezzala/README.md).

## The state of the checkout

Checked on 24 November 2026.

- It is a local Git repository on `main`. Jack asked for a private GitHub repository, but creating it failed with `HTTP 401: Bad credentials` from `gh`, so there is no remote yet.
- It runs on Homebrew's `python3.15`, in `.venv` inside the checkout. The system Python is 3.9, which fmsave does not support.
- Jack's save is `~/Library/Application Support/Sports Interactive/Football Manager 27/games/Anky Panky Negi - St Mirren.fm`, a St Mirren career at 29 June 2026. It is on FM27 build `27.1.1+2511875`, which fmsave 0.14.3 has not verified; every fmsave reader passed its structural checks.
- Snapshots go to `~/.mezzala/snapshots.db` by default. Nothing has been written there yet: checks so far used a copy of the save and a scratch database.
- Registering it with Claude Code (`claude mcp add --scope user mezzala -- ~/dev/mezzala/.venv/bin/mezzala`) was blocked by the permission check, so Jack runs it himself.
- Money is assumed to be stored in pounds (`STORED_UNITS_PER_POUND = 1`). That has not been checked against values FM shows in game.

## Showcase

- Idea sources: [fmsave](https://github.com/rhiever/fmsave) (created 14 September 2026), [FMSuperScout](https://github.com/mavarobli/FMSuperScout) (created 11 July 2026), [MCPFM](https://github.com/FootballManagerMCP/FootballManagerMCP) (created 11 November 2026), [fm-career-mcp](https://github.com/oguzhanozfe/fm-career-mcp) (created 12 November 2026).
- Demo: none. Jack did not ask for one.
- Status: not ready. There is no GitHub repository yet, and no demo.
