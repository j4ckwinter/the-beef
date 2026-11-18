# leave it on this Mac

[leave it](https://github.com/j4ckwinter/leave-it) is a command-line tool and git pre-commit hook. Code between `leave-it:start` and `leave-it:end` comments is frozen, and a commit that changes it is stopped, so a coding agent's unasked-for edits get caught. It came out of the idea queue and was built in the queue build on 18 November 2026. Its checkout is `../leave-it`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../leave-it/AGENTS.md) and [README](../../leave-it/README.md).

## The state of the checkout

Checked on 18 November 2026.

- The GitHub repository is private. The package is not on npm, though the name `leave-it` was free when checked. Publishing, or making the repository public, needs Jack's request.
- It is not installed or linked anywhere, and no repository on this Mac has its hook. The README's install steps use `npm link` from a clone.
- `leave-it install` writes the absolute paths of the Node binary and the CLI into the hook. Moving the checkout, or changing Node version through a version manager, means running `leave-it install` again in each protected repository.
- `docs/demo.gif` was made with throwaway scripts outside the repository, adapted from the recorder dustpan used to have. Nothing in the repository regenerates it.

## Showcase

- Idea: [one post](https://x.com/GhostFarmenw/status/2122554089494237431), posted 17 November 2026, and [another](https://x.com/elenacruz52_/status/2123147383832027521), posted 18 November 2026, both about agents rewriting code that already worked.
- Demo: `../leave-it/docs/demo.gif`, about 29 seconds, at the top of the README.
- Status: not ready. The repository is private and the package is not on npm, so the README's install steps only work for Jack.
