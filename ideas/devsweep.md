---
status: found
found: 2026-11-18
title: devsweep
pitch: A terminal tool that finds the junk coding agents leave behind (node_modules, abandoned git worktrees, test traces and build output), shows how much space each takes, and lets you clear the ones you pick.
demo: Run devsweep over a folder of sample projects, watch it list node_modules, stale worktrees and Playwright traces sorted by size, tick a few, confirm, and see the space reclaimed.
sources:
  - https://x.com/bradvin/status/2120925590555668576 # posted 2026-11-12
---

The poster's machine for agent work keeps running out of disk, mostly from node_modules, worktrees and test traces, and they asked for a cleanup tool built for that. devsweep scans a directory tree, groups what it finds by kind and age, and deletes only what the user selects. Worktrees are removed with `git worktree remove` and pruned, never by deleting folders blindly.

Scope for a day: TypeScript CLI with an interactive checklist, dry run by default, a `--yes` flag only for explicit use, and tests against a generated fixture tree.
