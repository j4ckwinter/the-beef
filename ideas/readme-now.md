---
status: found
found: 2026-11-18
title: readme-now
pitch: A small linter that flags changelog-style sentences in a README ("now supports", "previously", "no longer", "was renamed", dated update notes) so the page describes the project as it is today, not how it got there.
demo: Run `npx readme-now` on an agent-written README and watch it list the history-flavoured lines with file:line, the matched phrase and a one-line hint; delete two of them, run it again and the count drops; finish with a clean run and exit code 0.
sources:
  - https://x.com/Danmoreng/status/2121509625916715084 # posted 2026-11-14
---

Sebastian's post above says every README a coding agent writes turns into a record of past changes, and he has to tell it each time to describe only the current state for people meeting the project. Anyone letting agents maintain docs hits this, and it matches the rule in this repo's own AGENTS.md about keeping release logs out of pages.

Scope for a day: a TypeScript Node CLI. It reads README.md (or any Markdown paths or globs given), skips fenced code blocks, inline code and link URLs, and runs a short list of phrase rules: change verbs ("now supports", "has been updated", "we added", "was renamed", "no longer", "previously", "used to", "instead of the old"), version-timeline phrases ("as of v1.2", "since 0.3"), dated notes ("Update (2026-11-14):", "New:"), and struck-through text. Output is eslint-style lines with a coloured excerpt, plus `--json` for scripts and a non-zero exit code for CI or a pre-commit hook. Rules can be switched off by id in a small `.readme-now.json`. Tests cover each rule against Markdown fixtures, including the code-block skipping.

Checked on 18 November 2026: the npm registry has no `readme-now` (or `readmenow`) package. npm and GitHub searches for README linters turned up only tiny projects (readme-sanity, readme-gauge) that check for missing sections, badges and links, not changelog language. General prose linters such as Vale, write-good and alex ship no rule for it.
