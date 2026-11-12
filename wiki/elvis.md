# Elvis

Source snapshot checked on 12 November 2026: `4c736a96c3fc6d7a0e4c1b0d50e3752086a6db64`. The checkout was clean when inspected. This identifier describes the source used to write this page, not a requirement to stay on that revision. Recheck current files before acting.

## What lives where

| Repository | Path from the home repo | Purpose |
| --- | --- | --- |
| [Elvis](https://github.com/j4ckwinter/elvis) | `../elvis` | A macOS desktop pet, a black sprocker, that reacts to Claude Code through a hooks plugin. |

Start with the project's [contributor instructions](../../elvis/AGENTS.md) and [README](../../elvis/README.md). The contributor instructions own the working rules: one responsibility per file, almost no comments, commit as work completes, no AI attribution in commits, and which actions need Jack's request.

Elvis is a Swift package. `Sources/ElvisKit` holds the logic and drawing with no AppKit, clock, or unseeded randomness. `Sources/elvis` holds the app and command line. `plugin/` is the Claude Code plugin.

## Run checks

From the Elvis checkout:

```sh
make test         # the suite
make fingerprint  # proves a refactor changed no behaviour
```

Use `make test`, not `swift test`. On a Mac with Command Line Tools only, the Swift Testing macros need the plugin path the Makefile supplies.

## Things to know before acting

- A copy of Elvis is usually running on Jack's screen. Use a separate instance with `ELVIS_HOME` set for anything that sends events or films frames. The contributor instructions show how.
- The hook runs inside every Claude Code session. It must stay silent and exit 0.
- Screen capture was not permitted from the agent shell on 12 November 2026, so how he looks live was checked through `make sheets` and filmed frames, not screenshots.
