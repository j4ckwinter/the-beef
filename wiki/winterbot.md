# Winterbot on this Mac

[Winterbot](https://github.com/j4ckwinter/winterbot) is Jack's portfolio site. It is a small explorable town, Winter Town, built with Astro, Preact and TypeScript, with a plain portfolio beside it. Its checkout is `../winterbot`, relative to this repository's root. The names differ by layer: the repository is `winterbot`, `package.json` calls it `winterbot-scaffold`, the site calls itself Winter Town, and it is served at [winterbyte.vercel.app](https://winterbyte.vercel.app). This page describes the Mac. Whether the Windows PC has a checkout was not checked.

The project owns its own facts. Read its [README](../../winterbot/README.md) for what the site does, the commands, and how agents can visit it. Read its [project guide](../../winterbot/docs/project-guide.md) for controls, focused tests, sharing cards and performance measurements.

This page holds only what that repository cannot: how it is deployed, how the checkout sat on the Mac, and how it relates to Jack's other projects.

## Before working in it

Checked on 16 November 2026.

- The repository has no `AGENTS.md` or `CLAUDE.md`, so it states no commit, push or release rules of its own. [This repository's instructions](../AGENTS.md) then apply: commit or push only when the task asks. The [steering](../steering/working-preferences.md) still applies, and the README's `npm run check`, `npm run build` and `npm test` are the project's checks.
- The checkout was on the branch `winter-design`, level with its remote and with a clean working tree. That branch is one commit ahead of `main`, and it is open as [pull request 2](https://github.com/j4ckwinter/winterbot/pull/2). Leave the checkout on the branch Jack expects.
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
