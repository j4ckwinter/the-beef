# Winterbot on this Mac

[Winterbot](https://github.com/j4ckwinter/winterbot) is Jack's portfolio site. It is a small explorable town, Winter Town, built with Astro, Preact and TypeScript, with a plain portfolio beside it. Its checkout is `../winterbot`, relative to this repository's root. The names differ by layer: the repository is `winterbot`, `package.json` calls it `winterbot-scaffold`, the site calls itself Winter Town, and it is served at [winterbyte.vercel.app](https://winterbyte.vercel.app). This page describes the Mac. Whether the Windows PC has a checkout was not checked.

The project owns its own facts. Read its [contributor instructions](../../winterbot/AGENTS.md) for the commands, the owners table, the standards and which actions need Jack's request. Read its [README](../../winterbot/README.md) for what the site does and how agents can visit it, and its [project guide](../../winterbot/docs/project-guide.md) for controls, focused tests, sharing cards and performance measurements.

This page holds only what that repository cannot: how it is deployed, how the checkout sat on the Mac, and how it relates to Jack's other projects.

## Before working in it

Checked on 16 November 2026.

- On 16 November 2026 the checkout was on the branch `winter-design`, open as [pull request 2](https://github.com/j4ckwinter/winterbot/pull/2). That day it gained local commits that put the frame back to `main`'s style, added `AGENTS.md` and refactored the code to the coding standards; they were not pushed. Leave the checkout on the branch Jack expects.
- Playwright's own Chromium was not installed on the Mac. Browser tests ran in installed Chrome with `PLAYWRIGHT_CHANNEL=chrome`.
- The Mac runs Node 26.13.0, which the project's `engines` range accepts.
- GitHub Actions runs the checks in `.github/workflows/checks.yml` on every push and pull request.

## How it is deployed

- Vercel builds what is pushed to GitHub. On 16 November 2026 GitHub showed a successful `Vercel` commit status on the head of `main` and on the head of `winter-design`, both from the Vercel project `winterbot`. Treat a push to `main` as a deploy of the public site, and a push to another branch as a preview.
- Whether a deployment was promoted to production was not checked in Vercel. The checkout has no `.vercel` folder, so the Vercel CLI is not linked here.

## How it relates to the other projects

Checked on 16 November 2026 by reading `src/components/town/projects.ts` on `winter-design`.

- The town presents [Pancake Stack](pancake-stack.md) and `brain-cache`, which is not in the project map. It links to the Pancake Stack repository and to `docs/validation-controls.md` in Pancake Stack Evals. Moving or renaming that file breaks a link on the site.
- It does not present Panky, Pancake UI or Elvis.
- It does not use Pancake UI. Its styling is its own, built with Tailwind, so a Pancake UI release does not change it.
