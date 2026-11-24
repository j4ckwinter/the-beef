# Fantasy Pancake on this Mac

[Fantasy Pancake](https://fantasy-pancake.vercel.app) is Jack's FPL transfer planner: import a team ID, compare single transfers, two transfers or rolling, and preview the effect on the starting XI. It is a Next.js app on Vercel with no login and no database; settings stay in the browser. Its checkout is `../fantasy-pancake`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../fantasy-pancake/AGENTS.md), [README](../../fantasy-pancake/README.md), [deployment guide](../../fantasy-pancake/docs/deployment.md) and [model assumptions](../../fantasy-pancake/docs/model.md).

## How it ships

Checked on 23 November 2026.

- Merging to `main` deploys to production through Vercel's Git integration. The Vercel project is `fantasy-pancake` in the `jacks-projects-8a38ccc4` team. Branches get preview deployments.
- Code changes go through a pull request, merged with a merge commit. Small docs changes have gone straight to `main`.
- GitHub Actions runs the Verify workflow on every push. It is not a required check, so look at it before merging. Its `npm audit --omit=dev` step fails when a new Next.js advisory lands, even with no code change.
- The Vercel connector in Claude Code is not authorised for the `jacks-projects-8a38ccc4` team. The Vercel status on the GitHub commit shows whether a deployment finished.

## The state of the checkout

Checked on 23 November 2026.

- The GitHub repository [j4ckwinter/fantasy-pancake](https://github.com/j4ckwinter/fantasy-pancake) is public. The project's README, LICENSE and deployment guide say it is proprietary and should stay private. Jack has not said which is intended; changing visibility needs his request.
- `.nvmrc` pins Node 22.23.4, and `package.json` allows only Node 22. This Mac has Node 26 from Homebrew and no Node 22 under fnm. Checks pass on Node 26 anyway; CI is the Node 22 check.
- `next dev` and `next build` sometimes stop on a Next.js security notice. `next build` succeeds when run again; `next dev` exits, so run the browser tests against `npm run start` with `PLAYWRIGHT_BASE_URL`, as CI does.
- Playwright's Firefox fails to launch on this Mac. Chromium and WebKit work. CI covers Firefox.
- `.env.local` and `.vercel/` are in the checkout and ignored by Git.
- [PR #3](https://github.com/j4ckwinter/fantasy-pancake/pull/3) brought the project up to the coding standards: design tokens with a style check, a pure session reducer, split browser tests, and the bugs the audit found. Merged and deployed on 23 November 2026.
- [PR #4](https://github.com/j4ckwinter/fantasy-pancake/pull/4) moved the app from Pancake UI to shadcn and restyled every screen in "direction A · Tactics board, refined", which Jack picked from mocks. It added a dark mode that follows the system setting. Merged and deployed on 23 November 2026; the live page showed the new UI in light and dark that evening.
- Overnight on 23–24 November 2026, with Jack's authority to merge and deploy, four features shipped, each through an independent review and a live check on a public team:
  - [PR #5](https://github.com/j4ckwinter/fantasy-pancake/pull/5) adds a captain pick and bench order.
  - [PR #6](https://github.com/j4ckwinter/fantasy-pancake/pull/6) backtests the model against this season and calibrates it (`forecast-v6`). Numbers now read as expected points, with a dated accuracy note.
  - [PR #7](https://github.com/j4ckwinter/fantasy-pancake/pull/7) adds a multi-week "Plan ahead" planner (`forecast-v7`).
  - [PR #8](https://github.com/j4ckwinter/fantasy-pancake/pull/8) adds chip timing advice. Every chip is valued along one path built from the recommended plan. It needed three independent reviews before the advice was internally consistent.
- The backtest's main finding: the model's top transfer forecast about +7.6 points over four gameweeks but realised about +1.4 over holding. Refit the calibration later in the season. `scripts/fetch-backtest-data.ts` and `scripts/backtest.ts` rerun it; the data cache is gitignored.
- CI's Verify job has a 20-minute limit, and a slow runner can hit it during the browser tests. Rerunning the job passed.
- `next build` and the browser tests on this Mac take several minutes. Running four feature worktrees at once on different ports worked.
- Claude Code's `isolation: "worktree"` option made worktrees of `the-beef`, where the session started, not of this project. A worker that needs its own copy of this repository has to create the worktree itself.
