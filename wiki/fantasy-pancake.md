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
- [PR #3](https://github.com/j4ckwinter/fantasy-pancake/pull/3), opened on 23 November 2026, brings the project up to the coding standards: design tokens with a style check, a pure session reducer, split browser tests, and the bugs the audit found. It waits for Jack to merge; merging deploys it.
- Jack's next step for the project is moving from Pancake UI to shadcn with a polish pass, built on top of PR #3. Panky made the same move on 17 November 2026, so its commits are the template.
- Claude Code's `isolation: "worktree"` option made worktrees of `the-beef`, where the session started, not of this project. A worker that needs its own copy of this repository has to create the worktree itself.
