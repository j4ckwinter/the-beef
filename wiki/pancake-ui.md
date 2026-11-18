# Pancake UI on this Mac

[Pancake UI](https://github.com/j4ckwinter/pancake-ui) was Jack's React component library, published to npm as `@jack.winter/pancake-ui`. Its checkout is `../pancake-ui`, relative to this repository's root. It is checked out only on the Mac. The [Panky page](panky.md) records that the Windows PC had no checkout of it on 15 November 2026.

The project owns its own facts. Read its [contributor instructions](../../pancake-ui/AGENTS.md) for the commands, the owners table, the conventions, and which actions need Jack's request. Read its [README](../../pancake-ui/README.md) for what the library holds and how an app uses it. The [installation and releases guide](../../pancake-ui/docs/installation.md) covers versioning and publishing. The [verification guide](../../pancake-ui/docs/verification.md) covers what the checks run and the rules GitHub enforces on `main`.

This page holds only what that repository cannot: which of Jack's projects use the library, how the checkout sits on his Mac, and what an agent needs to know before working in it.

## Status

Checked on 17 November 2026.

- Jack retired it to start again on a new component library. The last release is 0.6.0, merge `7c087dc` on `main`.
- Uncommitted work on a local `feat/ink-lime` branch, a new ink and lime palette with Geist fonts, was discarded at his request without being committed. The branch had no commits of its own and was deleted.
- The GitHub repository is archived and read-only. Unarchive it on GitHub before pushing, opening a pull request or changing settings.
- The GitHub Pages site was deleted, and https://j4ckwinter.github.io/pancake-ui/ returns 404.
- The npm package `@jack.winter/pancake-ui` is not yet deprecated: npm was not logged in on this Mac. Every published version stays installable either way.
- Panky's web app pins 0.4.0 on GitHub. On 18 November 2026 the Mac's Panky checkout replaced it with shadcn/ui in local, unpushed `main` at `f48598c`; the [Panky page](panky.md) has the details. [jackwinter](jackwinter.md) still presents Pancake UI.
- The local checkout is on `main` at `7c087dc`, level with `origin/main`. The merged local and remote branches remain.

The sections below describe the library while it was active.

## Who uses it

Checked on 15 November 2026 by reading the manifests and lockfiles in the checkouts beside this repository on the Mac.

- Panky's web app pins `@jack.winter/pancake-ui` at exactly 0.1.1 in [apps/web/package.json](../../panky/apps/web/package.json). The Mac's Panky checkout was at `8751e457b64fd08f49b1e68c99b0be1f0ca36feb`.
- `../fantasy-pancake`, which is not in the project map, pins the same version. Its lockfile resolves the package from `registry.npmjs.org`.
- Both apps install the published package. Neither is linked to the library's checkout, and `npm ls -g` showed no global link. An edit or a build in `../pancake-ui` therefore changes neither app. This differs from Elvis and Pancake Stack, where the checkout is what runs.
- Versions 0.1.2 and 0.2.0 were published on 15 November 2026, and the registry listed 0.2.0 as `latest` that day. Both apps still pinned 0.1.1. 0.2.0 makes the default sizing compact after Jack found the components too large in Panky, and removes button `size={48}`. Panky never passes 48, but its own CSS overrides were written against the old sizes.
- On 16 November 2026 Panky moved to exactly 0.2.0 in `0c23fd2`, and its Settings and Manage chat dialogs now use the library's `Dialog`, `Tabs`, `Avatar` and `StatusChip`. Screenshots of Panky's chat, sidebar and account menu were pixel-identical before and after the upgrade. The same day Jack asked for 0.2.1, which quiets tab selection; it went out through pull request 6, merge `cd099ee` and the Publish workflow, and npm listed it as `latest` afterwards. Verify on `main` passed on its second attempt after a Firefox page-load timeout in an unrelated Button test. Panky moved to exactly 0.2.1 in `a83b9cc`, and its `pnpm-workspace.yaml` exempts that version from pnpm's minimum release age. `../fantasy-pancake` was not checked again.
- Later on 16 November 2026 Jack asked for 0.3.0, which adds `List`, `ListItem` and `DialogActions`, plus icon triggers and text lines for `DropdownMenu`. It went out through pull request 7, merge `51e683b` and the Publish workflow, and npm listed it as `latest` afterwards. Verify on `main` needed three attempts: two different Firefox tests timed out on the hosted runner. Locally, the timed-out accessibility test ran in the same time before and after the change. Panky moved to exactly 0.3.0 in `f0a6bcf` and replaced its own menu, Settings rows and dialog button rows with the library's in `27d62cf` and `d14c619`. Vercel reported success on `d14c619`.
- Later the same day Jack asked for a better answer-model picker in Panky. Pancake UI 0.4.0 adds radio items and item descriptions to `DropdownMenu`; it went out through pull request 8, merge `3a6bcec` and the Publish workflow, and Verify on `main` passed first time. Panky moved to exactly 0.4.0 in `fc5aa91` and rebuilt the picker as a menu in `2a48d0e`. Vercel reported success on `2a48d0e`.
- On 17 November 2026 Jack asked for a polish release. Pancake UI 0.5.0 adds motion, an opt-in dark theme (`data-pancake-theme`), SVG close and chevron icons, and 0.5 disabled opacity. It went out through pull requests 9 and 10, merge `963037e` and the Publish workflow, and the registry listed 0.5.0 as `latest` a minute after the run. Verify on `main` failed once after pull request 9: a new motion test loaded two stories in a row, and Firefox reported the first story's aborted font download. Pull request 10 split the test. Its own run then hit the Firefox Button page-load timeout seen in 0.2.1, and passed on a rerun. Panky still pins 0.4.0. Moving it to 0.5.0 needs two checks: its `dialog.css` sizes the close mark with `font-size`, which no longer applies to the SVG icon, and any accent overrides must move to the new `accentHover`, `onAccent` and `backdrop` tokens.
- Later on 17 November 2026 Jack asked for a second polish pass. Pancake UI 0.6.0 adds an overlay shadow token, inverts tooltips (ink behind surface text), and brands the hosted Storybook. It went out through pull request 11, merge `7c087dc` and the Publish workflow; Verify on `main` passed first time. An independent review caught that removing the tooltip border left it with no outline in forced colours; a transparent border was restored before merging. No API changes, so Panky's move past 0.4.0 still only needs the checks noted for 0.5.0.
- GitHub Pages was set to build from Actions on 17 November 2026, and the Storybook workflow deployed each successful `main` Verify build to https://j4ckwinter.github.io/pancake-ui/. The site was deleted when the library was retired.
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
