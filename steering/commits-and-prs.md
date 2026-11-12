# Commits and pull requests

Commit when the task asks for a commit. Push, open a pull request, merge, publish, and deploy only when the task asks for that action.

## Messages

Use Conventional Commits:

```text
type(scope): imperative summary
```

Scope is optional. pancake-stack's `AGENTS.md` states this form and says the subject should describe the actual change.

Recent history splits on whether a scope is included. brain-cache, pancake-stack, pancake-stack-evals, deedspan, and padel-potato often use one (`fix(ci): ...`, `docs(notifications): ...`). panky, pancake-ui, fantasy-pancake, and winterbot often omit it (`fix: ...`, `docs: ...`). Match the repo you are committing to.

Types in use across those histories: `feat`, `fix`, `docs`, `test`, `chore`, `refactor`, `perf`, `ci`, `style`, `revert`.

Write the subject in the imperative. Describe the resulting change, not the conversation that produced it.

## Pull requests

None of the public repos read for this file had a pull request template. If the target repo gains one, follow it.

Otherwise lead with the problem and the resulting behaviour. Add the checks that actually ran, and any risk or unfinished check that still matters. `skills/pr/SKILL.md` is the longer workflow. Do not invent ticket links or closing keywords.

## What stays out of a commit

Leave credentials, `.env` files, and tokens uncommitted. panky keeps auth tokens on the server and out of frontend environment variables, URLs, logs, and persistent browser storage.

Do not copy files from fpl-radar, or from any other private repo, into this public repo.

## Where this came from

pancake-stack `AGENTS.md` at `e4f2061`, panky's auth rules in its `AGENTS.md` at `1853be2`, and the commit subjects on the default branches of the public repos named above. No shared pull request template was present in those checkouts.
