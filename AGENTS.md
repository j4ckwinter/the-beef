# Start here

This is Jack Winter's home repository for agent sessions. Start a session here when the work spans repositories, when the right project is unclear, or to maintain this repository. For work inside one project, start in that project's checkout, where the host loads its instructions, Git state, and history. A single-project task that arrives here anyway can go ahead through the steps below.

Each project's repository owns its facts and instructions. The wiki holds what no single project can own; personal preferences live in steering.

## Enter a project

1. Identify the project and requested outcome. Read only its wiki page and the relevant steering guidance. Start with [working preferences](steering/working-preferences.md). Before changing code, read the [coding standards](steering/coding-standards.md).
2. Resolve the project path relative to this repository root, not the current shell directory. Confirm the checkout and remote before acting. If it is missing, ask for its location rather than cloning or creating a replacement without authorization.
3. Read the target repository's applicable contributor instructions, including instructions for the files you will touch. Inspect its current Git state and preserve existing work.
4. Load the relevant Pancake Stack workflow when available. Do not read every skill or copy the plugin into this repository. If an explicitly requested skill is unavailable, report that rather than claiming to have used it.
5. Run commands from the target repository. Keep edits within the task's authorized scope. A relationship between repositories does not authorize changes in both.

## Project map

| Project | Checkout, relative to this root | Context |
| --- | --- | --- |
| Pancake Stack | `../pancake-stack` | [Library and evaluator](wiki/pancake-stack.md) |
| Pancake Stack Evals | `../pancake-stack-evals` | [Library and evaluator](wiki/pancake-stack.md) |
| Elvis | `../elvis` | [Elvis on this Mac](wiki/elvis.md) |

## Keep context trustworthy

Treat wiki pages as orientation, not proof of current behavior. Check source files before relying on commands or constraints. Flag stale facts; reconcile them with the current repository and task instructions. Surface genuine instruction conflicts rather than silently choosing whichever is convenient.

A wiki page holds what the project's repository cannot own: how projects relate, and facts about Jack's machine and working setup. For anything the project could own, link to its instructions rather than copying them. Keep source links and verification dates. Separate observed facts from personal preferences and proposals. Do not accumulate release logs, task history, session transcripts, credentials, or raw evaluation records here.

Committing is expected in this repository. Commit each completed change on `main` and push it, without asking first. This covers this repository only. Each project's own instructions govern commits and pushes there; where they are silent, commit or push only when the task asks. Publish anything beyond this repository's own pushes, install plugins, or change global settings only when the task authorizes those actions.
