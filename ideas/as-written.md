---
status: picked
found: 2026-11-19
title: as-written
pitch: A small linter that checks commands, scripts, file paths and env names in a README against the repo, so a stale page cannot send a person or an agent down a hole.
demo: Run `npx as-written` on a README that still documents a renamed npm script, a deleted path and a removed env var; watch it list each claim with file:line and why it fails; fix two of them, run it again and the count drops; finish with a clean run and exit code 0.
sources:
  - https://x.com/wshxnv/status/2122697152665395421  # posted 2026-11-17
  - https://x.com/kyleryan/status/2121019832355205530  # posted 2026-11-12
  - https://x.com/icanvardar/status/2123013095198949399  # posted 2026-11-18
  - https://x.com/dmshirochenko/status/2120828384754254037  # posted 2026-11-12
---

Waishnav's post above is about a pattern he keeps hitting across repos: the agent reads the docs first and then explains, or even "fixes," the code to match a page that is no longer true. Kyle's post makes the same point from the other side, that bad API calls often come from following a stale README perfectly. Can's post notes that many repos now have an AGENTS.md and still lack a README a human can trust. Dmitriy's post points at a small study in which stale docs were the largest group of agent mistakes, and a pre-commit check that printed the real figure stopped the first bad commit.

This is a different job from readme-now, which flags changelog phrasing so a page describes the project as it is today. as-written would check whether the concrete claims still match the tree.

Scope for a day: a TypeScript Node CLI. It reads README.md (or any Markdown paths or globs given), skips quoted text that is clearly output, and checks a short list of claims: package scripts (`npm run build`, `pnpm lint`, `yarn test`, `bun run dev`, plus `npm test` and `npm start`), relative file and docs paths, and environment variable names against `.env.example` or `.env.sample` when those files exist. Output is eslint-style lines with file:line, the claim and a one-line reason, plus `--json` for scripts and a non-zero exit code for CI or a pre-commit hook. It does not execute documented commands. Tests cover each rule against Markdown fixtures, including code-fence commands and inline backticks.

Checked on 19 November 2026: the npm registry has no `as-written` package. DriftFence is a TypeScript CLI for the same job but has one GitHub star, three weekly npm downloads and no release since July. RealityLint covers it more thoroughly, including Compose and Cargo, but it is a Python package with seven GitHub stars and nine PyPI downloads in the past week, so it is not widely adopted and is not an `npx` install. etymd (zero stars, 38 weekly npm downloads) checks agent instruction files such as AGENTS.md and CLAUDE.md, not the human README that agents in these posts actually followed. markdown-doctest and txm (about 2,000 and 1,500 weekly downloads) only run annotated or JavaScript code examples; they do not check that a documented script, path or env name still exists. Avoid the names `driftfence`, `realitylint` and `etymd`.
