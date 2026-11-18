# devsweep on this Mac

[devsweep](https://github.com/j4ckwinter/devsweep) is a terminal tool that finds what coding agents leave behind (`node_modules`, worktrees, test and build output) and clears only what Jack ticks. It came out of the idea queue and was built in the queue build on 18 November 2026. Its checkout is `../devsweep`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../devsweep/AGENTS.md) and [README](../../devsweep/README.md).

## The state of the checkout

Checked on 18 November 2026.

- The GitHub repository is private. Publishing to npm or making it public needs Jack's request.
- It is not installed or linked anywhere. Run it from the checkout with `npm start -- <folder>`. Once the repository is public, `npx --allow-git=root github:j4ckwinter/devsweep <folder>` runs it anywhere. npm 12 refuses installs from git without that flag; checked on this Mac with npm 12.2.1 against a local git URL.
- A list-only run over `~/dev` found about 5 GB, mostly `node_modules`. It also found a worktree of Panky's at `/private/tmp/panky-milestone2` whose folder is gone, ready to prune. Nothing was cleared.
- `npm run demo` records through macOS's `script` command, so it works only on the Mac.

## Showcase

- Idea: [the post that asked for it](https://x.com/bradvin/status/2120925590555668576), posted 12 November 2026.
- Demo: `../devsweep/docs/demo.gif`, about 15 seconds, at the top of the README.
- Status: not ready. The GitHub repository is private, so the README's `npx` command and the link would fail for anyone else. Everything else is in place: the README GIF, a one-command run, and the MIT licence.
