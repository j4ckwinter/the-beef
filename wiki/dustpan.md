# dustpan on this Mac

[dustpan](https://github.com/j4ckwinter/dustpan) is a terminal tool that finds what coding agents leave behind (`node_modules`, worktrees, test and build output) and clears only what Jack ticks. It came out of the idea queue and was built in the queue build on 18 November 2026, as devsweep. Its checkout is `../dustpan`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../dustpan/AGENTS.md) and [README](../../dustpan/README.md).

## The state of the checkout

Checked on 18 November 2026.

- It was renamed from devsweep because npm refuses that name as too close to the existing `dev-sweep` package, a similar node_modules cleaner. GitHub redirects the old repository address.
- The GitHub repository is public. The npm package `dustpan` is not published yet. Jack runs `npm publish` himself; a new version, or posting about it, needs his request.
- It is not installed or linked anywhere. Run it from the checkout with `npm start -- <folder>`.
- A list-only run over `~/dev` found about 5 GB, mostly `node_modules`. It also found a worktree of Panky's at `/private/tmp/panky-milestone2` whose folder is gone, ready to prune. Nothing was cleared.
- `docs/demo.gif` is a static image. Nothing in the repository regenerates it, so a new one is made by hand.

## Showcase

- Idea: [the post that asked for it](https://x.com/bradvin/status/2120925590555668576), posted 12 November 2026.
- Demo: `../dustpan/docs/demo.gif`, about 15 seconds, at the top of the README.
- Status: not ready. The README's `npx dustpan` command waits on the npm package, which is not published yet.
