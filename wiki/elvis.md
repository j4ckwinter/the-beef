# Elvis

Source snapshot checked on 12 November 2026: `f5664080a792e01e49748e1e3fc7e942e7386ad6`, tagged `v0.2.1`. The checkout was clean and matched `origin/main` when inspected. This identifier describes the source used to write this page, not a requirement to stay on that revision. Recheck current files before acting.

## What lives where

| Repository | Path from the home repo | Purpose |
| --- | --- | --- |
| [Elvis](https://github.com/j4ckwinter/elvis) | `../elvis` | A macOS desktop pet, a black sprocker, that reacts to Claude Code through a hooks plugin. |

Start with the project's [contributor instructions](../../elvis/AGENTS.md) and [README](../../elvis/README.md). The contributor instructions own the working rules: one responsibility per file, almost no comments, commit as work completes, no AI attribution in commits, how to release, and which actions need Jack's request. The README owns what he does and his known limits.

Elvis is MIT licensed. The `LICENSE` file was added on 12 November 2026.

Elvis is a Swift package. `Sources/ElvisKit` holds the logic and drawing with no AppKit, clock, or unseeded randomness. `Sources/elvis` holds the app and command line. `plugin/` is the Claude Code plugin.

## Run checks

From the Elvis checkout:

```sh
make test         # the suite
make fingerprint  # proves a refactor changed no behaviour
```

Use `make test`, not `swift test`. On a Mac with Command Line Tools only, the Swift Testing macros need the plugin path the Makefile supplies.

`make test` is safe to run at any time. It builds a debug binary and gives every test its own temporary home.

## The installed plugin runs from the checkout

The plugin is installed at user scope from the local checkout as a marketplace. Claude Code reads a plugin installed that way in place, so every Claude Code session on this Mac runs `../elvis/plugin/bin/elvis` as its hook. Observed on 12 November 2026 with Claude Code 2.1.322: `claude plugin list --json` reports `readFromFolder` as the checkout's `plugin/`, and a `--debug-file` log shows the hook command resolved to that path.

Two things follow:

- `make`, `make universal`, `make sheets`, `make install`, and `make restart` all replace `plugin/bin/elvis`. Every session starts using the new hook at once. While a change to the hook is half done, build with `swift build -c release` and run `.build/release/elvis` instead.
- The Elvis on screen keeps running the build he was started from. `make restart` rebuilds and swaps him. Restarting him needs Jack's request.

An earlier version of this page said the install was a separate copy that a rebuild did not reach. That was wrong.

## Things to know before acting

- A copy of Elvis is usually running on Jack's screen. Use a separate instance with `ELVIS_HOME` set for anything that sends events or films frames, and add `ELVIS_HEADLESS` unless a second dog on screen is wanted. Keep the `ELVIS_HOME` path short, because a Unix socket path is limited to about 100 characters. A headless copy still plays sounds.
- The hook runs inside every Claude Code session. It must stay silent and exit 0, and only an event kind, the session id, a tool category, a subagent id, and a pairing hash may leave it.
- `elvis` is on Jack's `PATH` at `~/.local/bin/elvis`, installed with `make install` on 12 November 2026. Only `make install` updates that copy. It was not updated for `v0.2.1` and differed from `plugin/bin/elvis` when compared that evening.
- Jack's `~/.zshrc` loads the zsh shell integration from `../elvis/plugin/bin/elvis`, added on 12 November 2026. It reports his own test runs, commits, and pushes to Elvis.
- GitHub runs `make test` on every push to `main` and on pull requests.
- Screen capture was not permitted from the agent shell on 12 November 2026, so how he looks was checked through `make sheets` and filmed frames, not screenshots. An agent cannot hear him either: the bark and yip were checked for length, loudness, and timing, not by ear.

## Releases

`v0.2.0` and `v0.2.1` were both released on 12 November 2026. `v0.2.1` stops him whining at the door when tests fail in another session or in Jack's shell, and adds the licence. Pushing a `v<version>` tag that matches `plugin/.claude-plugin/plugin.json` runs `.github/workflows/release.yml`. It runs the suite, builds a universal binary, adds the plugin, that binary, and the licence to the `release` branch, and attaches the binary to a GitHub release.

Other people install without building from that branch:

```sh
claude plugin marketplace add j4ckwinter/elvis#release
claude plugin install elvis@elvis
```

These two commands were run on 12 November 2026 with `CLAUDE_CONFIG_DIR` set to a scratch directory, which leaves Jack's own settings alone. The plugin installed at 0.2.0 with a runnable binary. The install was not repeated for 0.2.1; the `release` branch was read back and holds version 0.2.1, the binary, and `LICENSE`. The `main` branch carries no binary.

## Checking a change against real Claude Code

Both methods were used on 12 November 2026 and cost a short headless session each.

- To see what Claude Code sends, load a scratch plugin whose hooks append their payload to a file, with `claude -p ... --plugin-dir <scratch plugin>`.
- To see what Elvis sends on, copy `plugin/` with a new build to a scratch directory, listen on a scratch socket, and run `claude -p ... --plugin-dir <that copy>` with `ELVIS_HOME` set to the socket's directory. A plugin loaded with `--plugin-dir` replaces the installed one of the same name for that session.

## What needed Jack on 12 November 2026

The agent's permission classifier refused these even after Jack had asked for the work in chat: `claude plugin marketplace add` and `claude plugin install` against his real settings, appending to `~/.zshrc`, running a downloaded binary, and creating and pushing a release tag. The tag push went through once Jack approved it in a question dialog. `git push origin main`, `make install`, `elvis restart`, and `claude plugin update elvis@elvis` went through without one.

For `v0.2.1` Jack approved the Rosetta install and the tag push in a question dialog before either was tried, and both went through.

## Open on 12 November 2026

- The Intel half of the binary has barely been run. Rosetta 2 was installed on this Mac on 12 November 2026, and the Intel half of a local universal build printed its help under it. Jack chose to skip the rest of the check. The suite cannot be built for Intel here: `swift test --arch x86_64` fails to link because the Command Line Tools ship the Swift Testing library for Apple silicon only.
- The shell integration covers zsh and bash, tested with the bash 3.2 that ships with macOS. Jack chose to leave fish out.
