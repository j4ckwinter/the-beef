---
status: found
found: 2026-11-24
title: poacher
pitch: A local MCP server for Football Manager 27 that snapshots a career save every time it changes and answers transfer questions from how players have moved since, so Claude can say who replaces an ageing midfielder under budget, who is rising fastest against his value, and which of last year's regens are actually developing.
demo: Point poacher at an FM27 career with snapshots from two in-game seasons; ask Claude "who replaces my 31-year-old DM for under £8m?" and see a ranked list with fee, age, CA gain since last season and the reason each one fits; ask "who did I sell too early?" and see former players whose CA and value climbed after they left; ask for this summer's best regens and see them sorted by potential with growth since intake.
sources:
  - https://github.com/rhiever/fmsave  # created 2026-09-14, pushed 2026-11-21
  - https://github.com/mavarobli/FMSuperScout  # created 2026-07-11, pushed 2026-11-24
  - https://github.com/FootballManagerMCP/FootballManagerMCP  # created 2026-11-11, pushed 2026-11-22
  - https://github.com/oguzhanozfe/fm-career-mcp  # created 2026-11-12, pushed 2026-11-13
---

Started as an Electron "recruitment intelligence" app. FMSuperScout already ships that app for free: it reads the whole FM27 save from memory, keeps snapshots, shows growth and an intake radar, flags squad succession gaps, and hides CA/PA on request. So the app is out. What is left is the question-answering layer on top of save history.

Two FM27 MCP servers already exist. MCPFM is a mod that reads the game live and can act in it (tactics, scouting, shortlists). fm-career-mcp reads the save file through fmsave and covers match reviews, scouting and training. Both are general assistant managers working from the present state of the save. Neither keeps snapshots across a career, which is what poacher is for. These are claims from their READMEs, checked on 2026-11-24; their code has not been read.

## Before building

Jack plays a few sessions with fm-career-mcp (tested on macOS) and notes what he keeps wishing it could answer. If those wishes are about change over time, poacher is worth building. If it already answers them, drop this idea.

## How it gets built

Jack builds this one in steered sessions, not a queue build, because it needs his own FM27 career saves across in-game seasons to test against.

## Scope

A Python MCP server on [fmsave](https://github.com/rhiever/fmsave), with snapshots in SQLite. The scoring and ranking code takes records and returns ranked results with reasons, and is tested from fixture records. Reading the save, the database and the MCP transport sit at the edges.

| Tool | Answers |
| --- | --- |
| `snapshot` | Stores players, values and contracts from the current save, keyed by in-game date |
| `squad_gaps` | Where the squad is thin, ageing, or has no successor in the next two seasons |
| `find_replacement(player, max_fee, max_age)` | Players with a similar attribute profile inside the budget |
| `risers(since, min_ca_gain)` | Fastest improvers since an earlier snapshot, ranked against their value |
| `sell_high` | Own players whose value has peaked, or whose CA has stalled while value climbs |
| `contract_watch` | Contracts ending soon, free agents and pre-contract targets that fill a gap |
| `regen_intake(since)` | Regens new since the last snapshot, sorted by potential |

The smallest version worth showing is `snapshot`, `risers` and `find_replacement`.

Known limits from fmsave's README: FM27 is verified on build `27.0.0+2486695` only. Money comes back in the game's stored units, so poacher needs its own conversion to display currency. Asking prices are not read. Most tactic settings come back as raw numbers, so "fit" comes from roles and attribute weights poacher defines, not from FM's own role ratings.

Not in scope: an Electron or web UI, reading game memory, editing saves, and acting in the game.

## Fit

A fun side project, not a startup: free open-source tools already set FM players' price expectation at zero. It uses Python, MCP and deterministic scoring with an AI layer on top, and needs no paid API beyond the MCP client Jack already uses.
