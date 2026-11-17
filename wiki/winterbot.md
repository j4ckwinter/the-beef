# Winterbot on this Mac

[Winterbot](https://github.com/j4ckwinter/winterbot) was Jack's portfolio site: a small explorable town, Winter Town, built with Astro, Preact and TypeScript, with a plain portfolio beside it. [jackwinter](jackwinter.md) has replaced it. Its checkout is `../winterbot`, relative to this repository's root. The names differ by layer: the repository is `winterbot`, `package.json` calls it `winterbot-scaffold`, and the site calls itself Winter Town. This page describes the Mac. Whether the Windows PC has a checkout was not checked.

The project owns its own facts. Read its [contributor instructions](../../winterbot/AGENTS.md) for the commands, the owners table and the standards, its [README](../../winterbot/README.md) for what the site does, and its [project guide](../../winterbot/docs/project-guide.md) for controls, tests, sharing cards and performance measurements.

This page holds only what that repository cannot: its status, how it was deployed, and how it relates to Jack's other projects.

## Status

Checked on 17 November 2026.

- Jack retired it. [Pull request 2](https://github.com/j4ckwinter/winterbot/pull/2), the winter design with day, night and weather, was merged into `main` as `3d80dc4` with every check passing, and the GitHub repository was then archived. It is read-only: unarchive it on GitHub before pushing, opening a pull request or changing settings.
- The local checkout is on `main` at `3d80dc4`, level with `origin/main`. The `winter-design` and `agent-visitors` branches remain, both merged.
- Winter Town has no public address. `winterbyte.vercel.app` answers with a 308 to `www.jackwinter.xyz`, and jackwinter's `vercel.json` sends Winter Town's old paths on to pages there.

## How it was deployed

- The Vercel project `winterbot` built every push; the merge commit `3d80dc4` got a successful `Vercel` status. Those builds are no longer served at `winterbyte.vercel.app`, which forwards to jackwinter. Whether to delete the Vercel project is undecided; the checkout has no `.vercel` folder, so the Vercel CLI is not linked here.

## How it relates to the other projects

Checked on 16 November 2026 by reading `src/components/town/projects.ts` on `winter-design`.

- The town presented [Pancake Stack](pancake-stack.md) and `brain-cache`, and linked to `docs/validation-controls.md` in Pancake Stack Evals.
- It does not use Pancake UI. Its styling is its own, built with Tailwind.
