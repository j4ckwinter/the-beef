---
status: found
found: 2026-11-20
title: mcp-once
pitch: A small product that keeps one canonical MCP config, with personal and work profiles, and writes each coding agent's native file in the right shape and secret syntax so the set of servers cannot drift.
demo: Open a repo whose Cursor, Claude Code and VS Code MCP files already disagree; import them into a local mcp-once UI and see the servers land in one list; add a server, switch from a personal profile to a work one, and run sync; watch each client's file update with the right keys and env or input secret refs; hand-edit one file, run diff to see the drift, then sync it clean.
sources:
  - https://x.com/emadev01/status/2121699773703225828  # posted 2026-11-14
  - https://x.com/maomao000211/status/2121787469507198982  # posted 2026-11-15
  - https://x.com/toirant/status/2121994476927197224  # posted 2026-11-15
  - https://x.com/PowerduckLabs/status/2122459619146785081  # posted 2026-11-16
  - https://x.com/AgentScoutHQ/status/2121320990437175327  # posted 2026-11-13
---

Ema's post above is about the chore of adding the same MCP servers again and again to Claude Code, Codex, Cursor and the Claude app, and of keeping personal and work accounts in step. Mao's reply in that thread says the unsolved bit is exactly that split, plus the fact that each tool keeps its config in a different place. Miles's reply maps the paths and shapes (Cursor, VS Code, Claude Code) and points at a small web form he built that only prints the right JSON. Powerduck's follow-up is the recurring pain: they already keep a canonical file and a transform step, and hand-editing the three native files still drifts within a week. AgentScout's post is the secrets half of the same job, because Claude Code expands `${VAR}` while VS Code wants an `inputs` entry with `${input:id}`, so a shared file that pastes a raw token is unsafe.

This is a week-long TypeScript product, not a one-day converter. Fit is strong: Node CLI, a local React UI, and the AI and dev-tool work Jack already cares about. No paid API.

Rough milestones:

1. A canonical schema and adapters for Cursor, Claude Code, VS Code, Windsurf, Codex and Claude Desktop, covering project and user paths, top-level keys, remote field names and the fields each client cannot represent.
2. A CLI with `init`, `import`, `sync`, `diff` and `validate`. Import reads the files already on the machine, merge-safe. Diff prints drift before a sync overwrites anything.
3. Secret rewriting, never raw tokens in a file that can go in git: `${VAR}` / `${VAR:-default}` for Claude Code, `${env:…}` for Cursor, and VS Code `inputs` with `password: true`.
4. Personal and work profiles, so the same repo can point at different accounts and server sets without copying files by hand. This is the part the thread says nobody has solved.
5. A local React UI to list servers, edit them, switch profiles, and preview each client's output before writing.
6. A watch mode or pre-commit hook that fails when a native file has drifted from the canonical one.
7. Fixture tests for each adapter, including secret rewriting and a merge of two imported configs.

Checked on 20 November 2026: the npm registry has no `mcp-once` package. Closest existing tools are not widely adopted. mcpfold is a polished CLI that folds one config out to many clients, but the GitHub repo has no stars and last-week npm downloads were in single digits. mcp-config-sync does the same convert/import/sync job and has no GitHub stars and three weekly downloads. agentinit (four stars) and cyncia (one star) cover a broader "write agent config once" idea, including skills and rules. Toolkien (two stars), launched in Ema's post, is a different shape: a proxy MCP in front of other servers, not a writer of native client files. Miles's Connectory builder only prints JSON in the browser. Axis MCP and a number of one-page validators also generate a single file. Avoid the names `mcpfold`, `mcp-config-sync`, `agentinit`, `cyncia`, `toolkien` and `unify-mcp` (the last is an unrelated CRM connector).
