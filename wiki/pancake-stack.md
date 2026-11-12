# Pancake Stack and its evaluator

Source snapshot checked on 12 November 2026:

- Library: `634f6549d8e78800b9e1c821d1536417d99c7c45`.
- Evaluator: `4915ed27495a0d64423f251ceee8462895598017`.

Both checkouts were clean when inspected. These identifiers describe the sources used to write this page, not a requirement to stay on those revisions. Recheck current files before acting.

## What lives where

| Repository | Path from the home repo | Purpose |
| --- | --- | --- |
| [Pancake Stack](https://github.com/j4ckwinter/pancake-stack) | `../pancake-stack` | Declarative plugin manifests, 19 shared skills, and user documentation for Codex, Claude Code, and Cursor. |
| [Pancake Stack Evals](https://github.com/j4ckwinter/pancake-stack-evals) | `../pancake-stack-evals` | Package checks, fixtures, historical evidence, and evaluation tooling. |

Start with the library's [contributor instructions](../../pancake-stack/AGENTS.md) and [README](../../pancake-stack/README.md). For evaluator work, read its [contributor instructions](../../pancake-stack-evals/AGENTS.md) and [README](../../pancake-stack-evals/README.md) too.

The library is a collection of instructions, not an application server. Use its [installation guides](../../pancake-stack/README.md) to load it in an agent host when installation is authorized. Keep workflow changes in the library and tests or trial evidence in the evaluator.

## Run package checks

From the library checkout:

```sh
python3 -B ../pancake-stack-evals/run_checks.py --source .
```

Or from the evaluator checkout:

```sh
python3 -B run_checks.py --source ../pancake-stack --output /tmp/pancake-checks.json
```

The evaluator README specifies Python 3.12, matching CI. These commands use the local evaluator revision. To reproduce CI's exact evaluator, follow the library's [verification recipe](../../pancake-stack/docs/verification.md#run-the-checks), which resolves the pin in [.github/workflows/checks.yml](../../pancake-stack/.github/workflows/checks.yml) through a temporary detached checkout.

The [runner](../../pancake-stack-evals/run_checks.py) runs the test suite and records source identity. Keep both trees unchanged during checks: an edit during the run invalidates its preservation check. An optional output file must be outside both checkouts. The output path above is overwritten if reused; choose another path when retaining earlier results.

Commands here were checked against the source, not rerun while creating this page. Consult current output and the project's verification records for test results.

## Gotchas and boundaries

- Do not bundle executable helpers, tests, or evaluation evidence into the library. Its contributor instructions also restrict additions to the authorized skills.
- Keep the portable manifest and native Claude package identity consistent. Installation and discovery are separate host checks; passing package tests does not prove them.
- The documented Cursor route clones into its local plugins directory and updates with Git. Cursor loading and workflows were still unverified in the inspected sources; see the [Cursor guide](../../pancake-stack/docs/cursor.md).
- Live model trials require explicit task authorization, isolated profiles, and bounded execution. Keep raw records private and outside both repositories. Ordinary package checks do not authorize live trials, installation, publication, or global settings changes.
- Historical helper tests exercise retired functionality in evaluator fixtures. Do not interpret their success as proof of current plugin capabilities.
- The library uses Conventional Commits. Read current repository instructions before committing or preparing a PR.

## Source links

For readers on GitHub, these links preserve the inspected versions:

- [Library instructions](https://github.com/j4ckwinter/pancake-stack/blob/634f6549d8e78800b9e1c821d1536417d99c7c45/AGENTS.md), [README](https://github.com/j4ckwinter/pancake-stack/blob/634f6549d8e78800b9e1c821d1536417d99c7c45/README.md), and [verification guide](https://github.com/j4ckwinter/pancake-stack/blob/634f6549d8e78800b9e1c821d1536417d99c7c45/docs/verification.md).
- [Evaluator instructions](https://github.com/j4ckwinter/pancake-stack-evals/blob/4915ed27495a0d64423f251ceee8462895598017/AGENTS.md), [README](https://github.com/j4ckwinter/pancake-stack-evals/blob/4915ed27495a0d64423f251ceee8462895598017/README.md), and [runner](https://github.com/j4ckwinter/pancake-stack-evals/blob/4915ed27495a0d64423f251ceee8462895598017/run_checks.py).
