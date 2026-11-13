# Elvis

Source snapshot checked on 13 November 2026: `72f2d8d2f71c10b1eca7eb51b7ef142718d7b2c0`, tagged `v0.3.0`. The checkout was clean and matched `origin/main` when inspected. This identifier describes the source used to write this page, not a requirement to stay on that revision. Recheck current files before acting.

## What lives where

| Repository | Path from the home repo | Purpose |
| --- | --- | --- |
| [Elvis](https://github.com/j4ckwinter/elvis) | `../elvis` | A macOS desktop pet, a black sprocker, that reacts to Claude Code through a hooks plugin. |

Start with the project's [contributor instructions](../../elvis/AGENTS.md) and [README](../../elvis/README.md). The contributor instructions own the working rules: one responsibility per file, almost no comments, commit as work completes, no AI attribution in commits, how to release, and which actions need Jack's request. The README owns what he does and his known limits.

The README was rewritten on 13 November 2026 in the voice of the Pancake Stack README, which is how Jack wants his project READMEs to look. Its picture is `docs/elvis-light.png` and `docs/elvis-dark.png`, copied from the `readme-*.png` strips that `make sheets` writes.

Elvis is MIT licensed. The GitHub repository has a description and four topics, set on 13 November 2026.

Elvis is a Swift package. `Sources/ElvisKit` holds the logic and drawing with no AppKit, clock, or unseeded randomness. `Sources/elvis` holds the app and command line. `plugin/` is the Claude Code plugin.

## Run checks

From the Elvis checkout:

```sh
make test          # the suite
make fingerprint   # proves a refactor changed no behaviour
make claude-check  # proves Claude Code still marks commits and pushes
```

Use `make test`, not `swift test`. On a Mac with Command Line Tools only, the Swift Testing macros need the plugin path the Makefile supplies.

`make test` is safe to run at any time. It builds a debug binary and gives every test its own temporary home.

`make claude-check` has a real Claude Code session commit and push in a scratch repository and fails unless the hook payloads carry `tool_response.gitOperation` for both. Elvis learns of Claude's commits and pushes from that field, which the hooks reference does not describe. The check needs a signed-in `claude` and `jq`, costs a short headless session, and uses a scratch `ELVIS_HOME` so the Elvis on screen hears nothing. It passed on 13 November 2026 with Claude Code 2.1.323.

## One build runs everything on this Mac

The plugin is installed at user scope from the local checkout as a marketplace. Claude Code reads a plugin installed that way in place, so every Claude Code session on this Mac runs `../elvis/plugin/bin/elvis` as its hook. Observed on 13 November 2026 with Claude Code 2.1.323: `claude plugin list --json` reports `readFromFolder` as the checkout's `plugin/`. It also reports the installed version as 0.2.1 beside a folder version of 0.3.0. That figure is only the install record; `claude plugin update elvis@elvis` would refresh it and was not run.

`elvis` on Jack's `PATH` is a link from `~/.local/bin/elvis` to `plugin/bin/elvis`, made by `make install` on 13 November 2026. Before v0.3.0 it was a copy that only `make install` refreshed. On 12 November a bare `elvis restart` started that stale copy while the hook ran a newer build.

Three things follow:

- `make`, `make universal`, `make sheets`, `make install`, and `make restart` all replace `plugin/bin/elvis`. Every session starts using the new hook at once, and so does `elvis` on the `PATH`. While a change to the hook is half done, build with `swift build -c release` and run `.build/release/elvis` instead.
- The Elvis on screen keeps running the build he was started from. `make restart` rebuilds and swaps him. Restarting him needs Jack's request.
- A session-start hook swaps the running Elvis for its own build when his version is older than the hook's. A build of the same version is never swapped, so a rebuild from source still needs `make restart`. `ELVIS_AUTOSTART=0` turns the swap off along with the wake.

## Versions

`elvis version` prints a build's version, and the paw menu shows the running one's. The running Elvis writes his version and process id into `elvis.lock` in his home directory. A record counts as his own only when its process id is the one listening on the socket. An Elvis with no record of his own, which includes every build before v0.3.0, counts as older than any release.

The version is stated twice: `plugin/.claude-plugin/plugin.json`, which Claude Code reads, and `Version.current` in `Sources/ElvisKit/Version.swift`, which the binary carries. A test fails while they differ.

Observed on 13 November 2026 after `make restart`: the running Elvis was `plugin/bin/elvis` and his record read `0.3.0` with his process id.

## Things to know before acting

- A copy of Elvis is usually running on Jack's screen. Use a separate instance with `ELVIS_HOME` set for anything that sends events or films frames, and add `ELVIS_HEADLESS` unless a second dog on screen is wanted. Keep the `ELVIS_HOME` path short, because a Unix socket path is limited to about 100 characters. A headless copy still plays sounds.
- The hook runs inside every Claude Code session. It must stay silent and exit 0, and only an event kind, the session id, a tool category, a subagent id, and a pairing hash may leave it. The version check reads `elvis.lock` and adds nothing to what crosses the socket.
- The `SessionStart` hook has a ten-second timeout and the other hooks keep five. A swap waits up to two seconds for the old Elvis to stop listening and up to two more for the new one to listen.
- Jack's `~/.zshrc` loads the zsh shell integration from `../elvis/plugin/bin/elvis`, added on 12 November 2026. It reports his own test runs, commits, and pushes to Elvis.
- GitHub runs `make test` on every push to `main` and on pull requests.
- Screen capture was not permitted from the agent shell on 12 November 2026 and was not tried again on 13 November, so how he looks was checked through `make sheets` and filmed frames, not screenshots. An agent cannot hear him either: the bark and yip were checked for length, loudness, and timing, not by ear.

## Releases

| Version | Released | What it brought |
| --- | --- | --- |
| `v0.2.0` | 12 November 2026 | The first tagged release. |
| `v0.2.1` | 12 November 2026 | He stays silent at the door when tests fail in another session or in Jack's shell. Adds the licence. |
| `v0.3.0` | 13 November 2026 | `elvis version`, the version in the menu, the swap at session start, the linked install, `make claude-check`, detection of test runs started through `php`, and the rewritten README. |

Pushing a `v<version>` tag that matches `plugin/.claude-plugin/plugin.json` runs `.github/workflows/release.yml`. It runs the suite, builds a universal binary, adds the plugin, that binary, and the licence to the `release` branch, and attaches the binary to a GitHub release.

Other people install without building from that branch:

```sh
claude plugin marketplace add j4ckwinter/elvis#release
claude plugin install elvis@elvis
```

These two commands were run for 0.3.0 on 13 November 2026 with `CLAUDE_CONFIG_DIR` set to a scratch directory, which leaves Jack's own settings alone. The plugin installed at 0.3.0. Its binary held both architectures, each printed `0.3.0` for `elvis version`, the Intel one under Rosetta, and its hook was silent for a session start and for garbage. The `main` branch carries no binary.

## Checking a change against real Claude Code

Both methods were used on 12 November 2026 and cost a short headless session each. `make claude-check` is the first method scripted for commits and pushes.

- To see what Claude Code sends, load a scratch plugin whose hooks append their payload to a file, with `claude -p ... --plugin-dir <scratch plugin>`.
- To see what Elvis sends on, copy `plugin/` with a new build to a scratch directory, listen on a scratch socket, and run `claude -p ... --plugin-dir <that copy>` with `ELVIS_HOME` set to the socket's directory. A plugin loaded with `--plugin-dir` replaces the installed one of the same name for that session.

## What needed Jack

On 12 November 2026 the agent's permission classifier refused these even after Jack had asked for the work in chat: `claude plugin marketplace add` and `claude plugin install` against his real settings, appending to `~/.zshrc`, running a downloaded binary, and creating and pushing a release tag. The tag push went through once Jack approved it in a question dialog. `git push origin main`, `make install`, `elvis restart`, and `claude plugin update elvis@elvis` went through without one.

For `v0.2.1` Jack approved the Rosetta install and the tag push in a question dialog before either was tried, and both went through.

For `v0.3.0` Jack approved four things in one question dialog: going live on this Mac, the push, the repository description, and the release. All went through: `git push origin main`, the tag push, `make install`, `make restart`, `gh repo edit`, and the scratch-profile install with a run of its binary.

## Open on 13 November 2026

- The Intel half of the binary has run only `elvis help` and `elvis version` under Rosetta. Jack chose on 12 November to skip the rest of the check. The suite cannot be built for Intel here: `swift test --arch x86_64` fails to link because the Command Line Tools ship the Swift Testing library for Apple silicon only.
- The shell integration covers zsh and bash, tested with the bash 3.2 that ships with macOS. Jack chose to leave fish out.
- The menu's version line has not been seen on screen, and the README's picture has not been viewed as GitHub renders it.
- An old Elvis too busy to answer a quit within two seconds still has the quit waiting for him. He goes when he next looks, and nothing takes his place until the next session start. An independent review reproduced this by stopping the process.
- No test shows that the session-start event reaches the new Elvis after a swap, only that he is listening.
- `Brain.swift` is 414 lines, past the 300-line prompt to look. A split of its fetch and ball code was considered on 13 November and left, because it would loosen `private` state for a small gain.
