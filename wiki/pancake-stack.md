# Pancake Stack and its evaluator

Checked on 13 November 2026 against library `634f6549d8e78800b9e1c821d1536417d99c7c45` and evaluator `4915ed27495a0d64423f251ceee8462895598017`. These identifiers describe the sources used to write this page, not a requirement to stay on those revisions.

| Repository | Path from the home repo | Purpose |
| --- | --- | --- |
| [Pancake Stack](https://github.com/j4ckwinter/pancake-stack) | `../pancake-stack` | Plugin manifests, the shared skills, and user documentation for Codex, Claude Code, and Cursor. |
| [Pancake Stack Evals](https://github.com/j4ckwinter/pancake-stack-evals) | `../pancake-stack-evals` | Package checks, fixtures, historical evidence, and evaluation tooling. |

Each project owns its own facts. For the library, read its [contributor instructions](../../pancake-stack/AGENTS.md), [README](../../pancake-stack/README.md), and [verification guide](../../pancake-stack/docs/verification.md). For the evaluator, read its [contributor instructions](../../pancake-stack-evals/AGENTS.md) and [README](../../pancake-stack-evals/README.md). They hold the commands, the commit rules, what needs authorization, and what the checks do and do not prove.

This page holds only what neither repository can own alone: how the two fit together, and how the library is installed on Jack's Mac.

## How the two fit together

- A change to a workflow belongs in the library. Its tests, fixtures, and trial evidence belong in the evaluator. One task can need both, and each repository needs its own authorization.
- The evaluator treats the library checkout as a read-only input. A check run records both revisions and fails if either tree changes while it runs, so leave both checkouts alone until it finishes. The [runner](../../pancake-stack-evals/run_checks.py) refuses an output file inside either checkout.
- The checks can start from either checkout. The library's contributor instructions give the command to run there, and the evaluator's README gives the command to run from the evaluator.
- Both commands use whatever evaluator revision is checked out locally. CI uses the revision pinned in the library's [checks workflow](../../pancake-stack/.github/workflows/checks.yml), which can differ. On 13 November 2026 the pin was `563502ee4c6caa43504446a6d13bdd450835d521`, not the local evaluator's revision. The verification guide shows how to run against the pin.
- Publish an evaluator change before advancing the library's pin to it.

## How the library is installed here

Checked on 13 November 2026 with Claude Code 2.1.323.

- The plugin is installed at user scope from the local checkout as a marketplace. `claude plugin list --json` reports `readFromFolder` as `../pancake-stack`, and a session on that day loaded its skills from `../pancake-stack/skills`.
- The same command reports the installed version as 0.21.20 beside a folder version of 0.21.22. The first figure is only the install record.
- An edit to a skill in the checkout therefore changes the workflow every Claude Code session on this Mac uses. The verification guide says a local install picks up edits at the next session start or after `/reload-plugins`. While a skill is half edited, new sessions get the half-edited version.

## Source links

The sibling links above work locally. For readers on GitHub, these preserve the inspected versions:

- [Library instructions](https://github.com/j4ckwinter/pancake-stack/blob/634f6549d8e78800b9e1c821d1536417d99c7c45/AGENTS.md), [README](https://github.com/j4ckwinter/pancake-stack/blob/634f6549d8e78800b9e1c821d1536417d99c7c45/README.md), and [verification guide](https://github.com/j4ckwinter/pancake-stack/blob/634f6549d8e78800b9e1c821d1536417d99c7c45/docs/verification.md).
- [Evaluator instructions](https://github.com/j4ckwinter/pancake-stack-evals/blob/4915ed27495a0d64423f251ceee8462895598017/AGENTS.md), [README](https://github.com/j4ckwinter/pancake-stack-evals/blob/4915ed27495a0d64423f251ceee8462895598017/README.md), and [runner](https://github.com/j4ckwinter/pancake-stack-evals/blob/4915ed27495a0d64423f251ceee8462895598017/run_checks.py).
