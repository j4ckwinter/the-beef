# mezzala on this Mac

mezzala is an MCP server for Football Manager 27. It reads a career save with [fmsave](https://github.com/rhiever/fmsave), keeps a snapshot each time the save changes, and answers recruitment, squad, history, market and match-preparation questions through its tools (the README lists them). It came out of the idea queue as "poacher", was renamed, and Jack asked for it to be built directly on 24 November 2026, rather than in a queue build. Its checkout is `../mezzala`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../mezzala/AGENTS.md) and [README](../../mezzala/README.md).

## The state of the checkout

Checked on 25 November 2026.

- It is on `main`, pushed to [j4ckwinter/mezzala](https://github.com/j4ckwinter/mezzala). Jack made the repository public on 25 November 2026 and asked for the first release, [v0.1.0](https://github.com/j4ckwinter/mezzala/releases/tag/v0.1.0). It carries `mezzala.mcpb`, a Claude Desktop extension built with Anthropic's `mcpb` packer; AGENTS.md in the project has the release steps. Jack reported on 25 November 2026 that he installed it on the Windows PC by asking the Claude desktop app with the README's prompt, and that mezzala works there.
- Jack's own Claude Code and Claude Desktop still run the checkout's `.venv` server, not the release.
- On 25 November 2026 `main` gained a fog-of-war option, a format-9 snapshot store, and six more tools (player_profile, training_plan, dressing_room, fitness, staff_review, performance), 32 in all, and tools now default to the saved tactic's formation. None of it is in a release yet: v0.1.0 has 26 tools and no fog-of-war setting. Jack's own setups pick it up after both apps restart.
- It runs on Homebrew's `python3.15`, in `.venv` inside the checkout. The system Python is 3.9, which fmsave does not support.
- Jack's save is `~/Library/Application Support/Sports Interactive/Football Manager 27/games/Anky Panky Negi - St Mirren.fm`, a St Mirren career at 29 June 2026. It is on FM27 build `27.1.1+2511875`, which fmsave 0.14.3 has not verified; every fmsave reader passed its structural checks.
- Snapshots and the watchlist go to `~/.mezzala/snapshots.db`. It held one snapshot of the St Mirren career (29 June 2026) in the original format; newer servers keep it readable and re-read the save once to upgrade it. After updating mezzala, both Claude Code and Claude Desktop must be restarted, because an older running server cannot read newer snapshots.
- Jack registered it with Claude Code at user scope (`claude mcp add --scope user mezzala -- ~/dev/mezzala/.venv/bin/mezzala`). Adding it from a session was blocked by the permission check. `claude mcp list` shows it connected. It is also in Claude Desktop's `~/Library/Application Support/Claude/claude_desktop_config.json` under `mcpServers`, added on 24 November 2026; the file before that change is kept as `claude_desktop_config.json.before-mezzala`.
- Money is stored in pounds (`STORED_UNITS_PER_POUND = 1`). Jack confirmed on 24 November 2026 that values and the transfer budget match what FM shows for his St Mirren save.

## Showcase

- Idea sources: [fmsave](https://github.com/rhiever/fmsave) (created 14 September 2026), [FMSuperScout](https://github.com/mavarobli/FMSuperScout) (created 11 July 2026), [MCPFM](https://github.com/FootballManagerMCP/FootballManagerMCP) (created 11 November 2026), [fm-career-mcp](https://github.com/oguzhanozfe/fm-career-mcp) (created 12 November 2026).
- Demo: `../mezzala/docs/demo.gif`, about 15 seconds, centred at the top of the README. It replays a real headless Claude Code session (`claude -p` with stream-json output) against the St Mirren save, rendered by a throwaway Playwright and gifenc script outside the repository, so nothing in the repository regenerates it.
- Status: ready to post. Jack approved the demo and asked for this status on 25 November 2026.
