# Testing and verification

Prove the behaviour the task asked for. A passing lint or typecheck covers only what it exercises.

Use the command that repo documents in its README, package scripts, or agent file. If this file and that repo disagree, the repo wins. Install with the lockfile command that repo already uses, and use the Node version it names.

## How to report it

Say which commands ran and what they showed. Do not claim hosted CI ran from a local result.

For a refactor, take a baseline and repeat the affected checks afterwards. When layout or interaction changes, exercise the changed flow on the surfaces that repo already cares about.

When a check fails, find out whether the implementation or the expectation is wrong. Do not drop assertions, skip tests, broaden exceptions, or update screenshot baselines merely to make a failure pass.

Exercise the interface the claim is about. A screenshot of an unrelated build is not coverage for a component change. The verify workflow in the pancake-stack plugin (`~/repos/pancake-stack/skills/verify/SKILL.md`) is the longer procedure.

Use isolated test data. Keep credentials out of logs and frontend environment variables.
