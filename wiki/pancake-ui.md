# Pancake UI on this Mac

[Pancake UI](https://github.com/j4ckwinter/pancake-ui) is Jack's React component library, published to npm as `@jack.winter/pancake-ui`. Its checkout is `../pancake-ui`, relative to this repository's root. It is checked out only on the Mac. The [Panky page](panky.md) records that the Windows PC had no checkout of it on 15 November 2026.

The project owns its own facts. Read its [contributor instructions](../../pancake-ui/AGENTS.md) for the commands, the owners table, the conventions, and which actions need Jack's request. Read its [README](../../pancake-ui/README.md) for what the library holds and how an app uses it. The [installation and releases guide](../../pancake-ui/docs/installation.md) covers versioning and publishing. The [verification guide](../../pancake-ui/docs/verification.md) covers what the checks run and the rules GitHub enforces on `main`.

This page holds only what that repository cannot: which of Jack's projects use the library, how the checkout sits on his Mac, and what an agent needs to know before working in it.

## Who uses it

Checked on 15 November 2026 by reading the manifests and lockfiles in the checkouts beside this repository on the Mac.

- Panky's web app pins `@jack.winter/pancake-ui` at exactly 0.1.1 in [apps/web/package.json](../../panky/apps/web/package.json). The Mac's Panky checkout was at `8751e457b64fd08f49b1e68c99b0be1f0ca36feb`.
- `../fantasy-pancake`, which is not in the project map, pins the same version. Its lockfile resolves the package from `registry.npmjs.org`.
- Both apps install the published package. Neither is linked to the library's checkout, and `npm ls -g` showed no global link. An edit or a build in `../pancake-ui` therefore changes neither app. This differs from Elvis and Pancake Stack, where the checkout is what runs.
- Version 0.1.2 was published on 15 November 2026, and the registry listed it as `latest` that day. Both apps still pinned 0.1.1. The changelog says 0.1.2 changes no component API or behaviour.
- A library change reaches an app only after a new version is published and the app's pin and lockfile move to it. One task can need both repositories, and each needs its own authorization.
- The library's own [example app](../../pancake-ui/examples/web/package.json) depends on `file:../..`, so it does use the checkout's build.

## The state of the checkout

Checked on 15 November 2026 against `382ae6c36f92f1cc1f29db2da9498f964f11c863`.

- The checkout was on `main` with a clean working tree, level with `origin/main`. That revision is the merge of pull request 4, which carries version 0.1.2.
- Four merged branches remain locally and on GitHub: `chore/align-with-steering`, `chore/validate-npm-publishing`, `feat/npm-release`, and `fix/consumer-install-and-ci`.
- The ignored build output, `dist` and `storybook-static`, was last built on 15 November 2026 from `9750262`, the branch head before the merge. Rebuild before relying on it.
- The ignored `.tmp` folder held 201 entries and 325 MB of logs and scratch files from earlier sessions. The verification guide says the checks rebuild their consumers under `.tmp`. Which of the other entries are safe to delete was not checked.
- `.tmp/ci-replay` is a full copy of the repository from 31 October 2026. Playwright's test patterns match its spec files as well, so a local `npm run verify` reported 898 browser tests where hosted CI runs 449. The copy's specs matched `main` at `3930bc7` byte for byte. Read a local count with that doubling in mind, and expect the copy to drift from `main` as the suite changes.
- The ignored `artifacts` folder held the local 0.1.2 archive from `npm run release:local`, and a 0.1.0 archive under the unscoped filename `pancake-ui-0.1.0.tgz`. The second predates the scoped package name. The installation guide says the unscoped `pancake-ui` package on npm is unrelated.

## What this Mac has

Checked on 15 November 2026 with Claude Code 2.1.325.

- macOS 27.2.1, Node.js 26.13.0, and npm 12.2.1. The library asks for Node 22.18 or newer. Its workflows run Node 22.18.0, so a local pass and a hosted pass use different Node versions.
- The installed `@playwright/test` is 1.64.1, the pinned version. `~/Library/Caches/ms-playwright` holds the browser builds that version asks for: Chromium 1248, Firefox 1555, and WebKit 2370.
- `AppleLocale` is `en_GB` and `AppleLanguages` is `en-GB`, the values the Verify workflow sets on its runner. The verification guide says the screenshot baselines are specific to macOS Chromium and that native date and time formatting follows these settings.
- The GitHub CLI is signed in. `gh run list` returned the repository's workflow runs.
- Nothing was listening on ports 4173, 4174, 5173, 6006, or 6007.
- `npm run verify` passed on this Mac on 15 November 2026 with Node.js 26.13.0, three times: once on `3930bc7` and twice on the 0.1.2 branch.

## Work without disturbing it

- The browser suite starts three preview servers on `127.0.0.1` ports 4173, 4174, and 6007, with `--strictPort` and no reuse of a running server. [tests/servers.ts](../../pancake-ui/tests/servers.ts) defines them. The suite ran with those ports free on 15 November 2026. `npm run storybook` uses port 6006, read from `package.json`.
- `npm run example` starts Vite without naming a port, so it takes Vite's default of 5173. Panky's [web configuration](../../panky/apps/web/vite.config.ts) claims 5173 with `strictPort`. Whether the two collide when both run was not tried.
- The contributor instructions say what needs Jack's request: pushing a branch, opening or merging a pull request, changing the version, dispatching the Publish workflow, and updating screenshot baselines. `main` changes only through a pull request with a passing `verify` check.
- Published versions cannot be changed. The Publish workflow puts the archive from a successful Verify run on `main` onto public npm.
- On 15 November 2026 Jack asked a session to release. It pushed a branch, opened and merged pull request 4, and dispatched Publish, and the permission classifier asked for no dialog. That shows only what the classifier allows. The contributor instructions still decide what needs his request.
- `npm run release:local` runs the full verification and writes an archive to `artifacts`. The installation guide says it does not publish or upload.

## Source links

The sibling links above work locally. For readers on GitHub, these preserve the inspected version:

- [Contributor instructions](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/AGENTS.md), [README](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/README.md), [installation and releases guide](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/docs/installation.md), and [verification guide](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/docs/verification.md).
- [Test servers](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/tests/servers.ts), [example app manifest](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/examples/web/package.json), [Verify workflow](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/.github/workflows/verify.yml), and [Publish workflow](https://github.com/j4ckwinter/pancake-ui/blob/382ae6c36f92f1cc1f29db2da9498f964f11c863/.github/workflows/publish.yml).
- Panky's [web manifest](https://github.com/j4ckwinter/panky/blob/8751e457b64fd08f49b1e68c99b0be1f0ca36feb/apps/web/package.json) and [web configuration](https://github.com/j4ckwinter/panky/blob/8751e457b64fd08f49b1e68c99b0be1f0ca36feb/apps/web/vite.config.ts).
