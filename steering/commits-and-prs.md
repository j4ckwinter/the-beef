# Commits and pull requests

Commit when the task asks for a commit. Push, open a pull request, merge, publish, and deploy only when the task asks for that action.

## Messages

Use Conventional Commits. pancake-stack's `AGENTS.md` states this form and says the subject should describe the actual change:

```text
type(scope): imperative summary
```

Scope is optional. Match the recent subjects in the repo you are committing to: some include a scope, some do not.

Write the subject in the imperative. Describe the resulting change, not the conversation that produced it.

## Pull requests

If the target repo has a pull request template, follow it.

Otherwise lead with the problem and the resulting behaviour. Add the checks that actually ran, and any risk or unfinished check that still matters. The pr workflow in the pancake-stack plugin (`~/repos/pancake-stack/skills/pr/SKILL.md`) is the longer version. Do not invent ticket links or closing keywords.

## What stays out of a commit

Leave credentials, `.env` files, and tokens uncommitted. Keep tokens off frontend environment variables, URLs, logs, and persistent browser storage.

Do not copy files from a private repo into this public repo.
