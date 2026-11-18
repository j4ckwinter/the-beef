---
status: found
found: 2026-11-18
title: leave it
pitch: Wrap code that already works in `leave-it:start` and `leave-it:end` comments, and a git hook stops any commit that changes what is inside, so a coding agent's "improvements" to it get caught before they land.
demo: Show a function wrapped in leave-it comments, make an agent-style edit that rewrites it and also touches another file, run `git commit` and watch it get blocked with the frozen block's diff in red and its file:line, then restore the block and see the same commit go through.
sources:
  - https://x.com/GhostFarmenw/status/2122554089494237431 # posted 2026-11-17
  - https://x.com/elenacruz52_/status/2123147383832027521 # posted 2026-11-18
---

Both posts above describe the same itch: coding agents rewrite functions and config that were working fine, and the only defence is repeating "only this, nothing else" in every prompt. A marker in the code itself is a rule the agent can't forget between sessions.

Scope for a day: a TypeScript Node CLI. `leave-it check` compares the working tree, or the staged changes with `--staged`, against HEAD; finds regions between `leave-it:start` and `leave-it:end` in any comment syntax (`//`, `#`, `<!-- -->`, `/* */`); and reports every changed line inside one. It also flags a marker that was deleted or moved, so the agent can't just remove the fence. `leave-it install` adds a git pre-commit hook, and `leave-it list` prints every frozen region with its file and lines. A reason after the start marker (`leave-it:start payment rounding, see #12`) is shown in the failure message. An explicit `--allow` flag lets Jack approve a change on purpose. Tests use temporary git repos with fixtures.

Checked on 18 November 2026: the npm registry has no `leave-it` package. Claude Code's permission deny rules and the new `stet-cli` package (a few thousand downloads, first published 13 November 2026) protect whole files or globs and scope a task to files, but neither freezes a block inside a file. GitHub searches for region locks against AI edits found only tiny or unrelated projects.
