# Testing and verification

Prove the behaviour the task asked for. A passing lint or typecheck covers only what it exercises.

Use the command that repo documents. If this table disagrees with the repo's README or `package.json`, the repo wins.

| Repo | What to run |
| --- | --- |
| brain-cache | `npm run typecheck` and `npm test`. `npm run test:distribution` is for packaging changes and needs registry access. Node `>=22.12.0`. Install with `npm ci`. |
| pancake-stack | No suite in the repo. With pancake-stack-evals checked out beside it, run `python3 -B ../pancake-stack-evals/run_checks.py --source .`. Tests live in the evals repo. |
| pancake-stack-evals | `python3 -B run_checks.py --source ../pancake-stack` on Python 3.12. Do not modify the pancake-stack checkout from these tests. Live model trials need an explicit request, an isolated profile, and private raw output. |
| panky | `pnpm check` runs lint, format, typecheck, and backend tests. Also `pnpm build`, and `pnpm test:e2e` when UI or API behaviour changes. Node 24+ and pnpm 12.16.1. Install with `pnpm install --frozen-lockfile`. |
| pancake-ui | `npm run verify` before committing. Read `docs/styling.md` and `docs/verification.md` before adding a component. Node `>=22.18.0`. |
| fantasy-pancake | `npm run typecheck`, `npm run lint`, `npm run format:check`, `npm test`, `npm run test:e2e`, and `npm run build`. Node `>=22.23.4 <23`. Browser tests use fixtures; check live FPL separately before a release. |
| deedspan | `npm run check` runs lint, format, typecheck, and unit tests. `npm run test:e2e` covers browser flows. Node 24+. |
| winterbot | `npm run check`, `npm run build`, and `npm test`. Node `^22.23.4`, `^24.16.0`, or `>=26.3.0`. |
| padel-potato | `npm run verify` for format, types, lint, behaviour tests, and the web Storybook smoke check. `npm run supabase:test` resets the local database and runs the database checks. Native iOS and Android behaviour is authoritative over browser pixel parity. |

fpl-radar is private. Its checks are not recorded here.

## How to report it

Say which commands ran and what they showed. pancake-ui's agent file says not to claim hosted CI ran from a local result.

For a refactor, take a baseline and repeat the affected checks afterwards. panky and fantasy-pancake both ask for that, and fantasy-pancake asks for the changed flow on desktop and mobile when layout or interaction changes. padel-potato reviews visual changes in native Storybook on the available iOS and Android targets.

When a check fails, find out whether the implementation or the expectation is wrong. pancake-ui forbids dropping assertions, skipping tests, broadening exceptions, or updating screenshot baselines merely to make a failure pass. Its ESLint config rejects focused, skipped, and expected-failure tests in the verification suites.

Exercise the interface the claim is about. A screenshot of an unrelated build is not coverage for a component change. The verify skill in `skills/verify/SKILL.md` is the longer procedure.

Use isolated test data. panky forbids creating test conversations in the live database, and its server binds to loopback by default. Keep credentials out of logs and frontend environment variables.

## Where this came from

Package scripts, README verification sections, and agent files at the same commits listed in `steering/code-style.md`, plus pancake-stack `e4f2061` and pancake-stack-evals `4915ed2`.
