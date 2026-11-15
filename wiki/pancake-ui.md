# Pancake UI on this Mac

[Pancake UI](https://github.com/j4ckwinter/pancake-ui) is Jack's React component library, published to npm as `@jack.winter/pancake-ui`. Its checkout is `../pancake-ui`, relative to this repository's root. It is checked out only on the Mac. The [Panky page](panky.md) records that the Windows PC had no checkout of it on 15 November 2026.

The project owns its own facts. Read its [contributor instructions](../../pancake-ui/AGENTS.md) for where code goes and what a component change must include. Read its [README](../../pancake-ui/README.md) for what the library holds and how an app uses it. The [installation and releases guide](../../pancake-ui/docs/installation.md) covers versioning and publishing. The [verification guide](../../pancake-ui/docs/verification.md) covers what the checks run and the rules GitHub enforces on `main`.

This page holds only what that repository cannot: which of Jack's projects use the library, how the checkout sits on his Mac, and what an agent needs to know before working in it.

## Who uses it

Checked on 15 November 2026 by reading the manifests and lockfiles in the checkouts beside this repository on the Mac.

- Panky's web app pins `@jack.winter/pancake-ui` at exactly 0.1.1 in [apps/web/package.json](../../panky/apps/web/package.json). The Mac's Panky checkout was at `8751e457b64fd08f49b1e68c99b0be1f0ca36feb`.
- `../fantasy-pancake`, which is not in the project map, pins the same version. Its lockfile resolves the package from `registry.npmjs.org`.
- Both apps install the published package. Neither is linked to the library's checkout, and `npm ls -g` showed no global link. An edit or a build in `../pancake-ui` therefore changes neither app. This differs from Elvis and Pancake Stack, where the checkout is what runs.
- A library change reaches an app only after a new version is published and the app's pin and lockfile move to it. One task can need both repositories, and each needs its own authorization.
- The library's own [example app](../../pancake-ui/examples/web/package.json) depends on `file:../..`, so it does use the checkout's build.

## The state of the checkout

Checked on 15 November 2026 against `db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97`.

- The checkout was on `chore/validate-npm-publishing`, the branch merged as pull request 3, with a clean working tree. Its tree is identical to `origin/main` at `3930bc72c9af95937cb1f5d54ac901fedeba4d4c`, and GitHub reported that same revision for `main` that day.
- Local `main` was at `3a1be4a`, nine commits behind `origin/main`. The last fetch was on 31 October 2026. Update `main` before branching from it.
- The ignored build output dates from 31 October 2026: `dist`, `storybook-static`, and `node_modules`. Rebuild before relying on any of it.
- The ignored `.tmp` folder held 201 entries and 323 MB of logs and scratch files from earlier sessions. The verification guide says the checks rebuild their consumers under `.tmp`. Which of the other entries are safe to delete was not checked.
- The ignored `artifacts` folder held a 0.1.0 archive under the unscoped filename `pancake-ui-0.1.0.tgz`. It predates the scoped package name. The installation guide says the unscoped `pancake-ui` package on npm is unrelated.

## What this Mac has

Checked on 15 November 2026 with Claude Code 2.1.325.

- macOS 27.2.1, Node.js 26.13.0, and npm 12.2.1. The library asks for Node 22.18 or newer. Its workflows run Node 22.18.0, so a local pass and a hosted pass use different Node versions.
- The installed `@playwright/test` is 1.64.1, the pinned version. `~/Library/Caches/ms-playwright` holds the browser builds that version asks for: Chromium 1248, Firefox 1555, and WebKit 2370.
- `AppleLocale` is `en_GB` and `AppleLanguages` is `en-GB`, the values the Verify workflow sets on its runner. The verification guide says the screenshot baselines are specific to macOS Chromium and that native date and time formatting follows these settings.
- The GitHub CLI is signed in. `gh run list` returned the repository's workflow runs.
- Nothing was listening on ports 4173, 4174, 5173, 6006, or 6007.
- `npm run verify` was not run for this page, so whether the suite passes on this Mac today is unknown.

## Work without disturbing it

- The [Playwright configuration](../../pancake-ui/playwright.config.ts) starts three preview servers on `127.0.0.1` ports 4173, 4174, and 6007, with `--strictPort` and no reuse of a running server. `npm run storybook` uses port 6006. This was read from the configuration and `package.json`, not observed running.
- `npm run example` starts Vite without naming a port, so it takes Vite's default of 5173. Panky's [web configuration](../../panky/apps/web/vite.config.ts) claims 5173 with `strictPort`. Whether the two collide when both run was not tried.
- Pancake UI's instructions say to run `npm run verify` before committing. They do not say when to commit or push. This repository's rule applies: commit or push there only when the task asks.
- The verification guide says GitHub requires a pull request and the `verify` check to change `main`. Plan a change as a branch and a pull request, not a push to `main`.
- Dispatching the Publish workflow publishes to public npm, and the installation guide says published versions are immutable. It needs Jack's request, as does anything else that publishes.
- `npm run release:local` runs the full verification and writes an archive to `artifacts`. The installation guide says it does not publish or upload.

## Source links

The sibling links above work locally. For readers on GitHub, these preserve the inspected version:

- [Contributor instructions](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/AGENTS.md), [README](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/README.md), [installation and releases guide](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/docs/installation.md), and [verification guide](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/docs/verification.md).
- [Playwright configuration](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/playwright.config.ts), [example app manifest](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/examples/web/package.json), [Verify workflow](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/.github/workflows/verify.yml), and [Publish workflow](https://github.com/j4ckwinter/pancake-ui/blob/db7c78c4cdeb6c8ae915019aa7b528fe56b1cc97/.github/workflows/publish.yml).
- Panky's [web manifest](https://github.com/j4ckwinter/panky/blob/8751e457b64fd08f49b1e68c99b0be1f0ca36feb/apps/web/package.json) and [web configuration](https://github.com/j4ckwinter/panky/blob/8751e457b64fd08f49b1e68c99b0be1f0ca36feb/apps/web/vite.config.ts).
