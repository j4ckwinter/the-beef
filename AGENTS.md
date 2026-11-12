# Start here

This is Jack Winter's home repository for agent sessions. Use it to find the right project and working context. Project facts live in the wiki; personal preferences live in steering; the target repository owns its project-specific instructions.

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
| Elvis | `../elvis` | [Desktop spaniel for Claude Code](wiki/elvis.md) |

## Keep context trustworthy

Treat wiki pages as orientation, not proof of current behavior. Check source files before relying on commands or constraints. Flag stale facts; reconcile them with the current repository and task instructions. Surface genuine instruction conflicts rather than silently choosing whichever is convenient.

When asked to maintain this home repo, keep durable project knowledge, source links, and verification dates. Separate observed facts from personal preferences and proposals. Do not accumulate session transcripts, credentials, or raw evaluation records here. Commit, push, publish, install plugins, or change global settings only when the task authorizes those actions.
