# Elvis on this Mac

[Elvis](https://github.com/j4ckwinter/elvis) is a macOS desktop pet that reacts to Claude Code through a hooks plugin. His checkout is `../elvis`, relative to this repository's root.

The project owns its own facts. Read its [contributor instructions](../../elvis/AGENTS.md) for the commands, the working rules, the conventions, and how a release goes out. Read its [README](../../elvis/README.md) for what he does and his known limits. Releases and open work are on GitHub, under [releases](https://github.com/j4ckwinter/elvis/releases) and [issues](https://github.com/j4ckwinter/elvis/issues).

This page holds only what that repository cannot: how Elvis is set up on Jack's Mac, and what an agent needs to know to work without disturbing it.

## How he is installed here

Checked on 13 November 2026 with Claude Code 2.1.323.

- The plugin is installed at user scope from the local checkout as a marketplace. `claude plugin list --json` reports `readFromFolder` as the checkout's `plugin/`, so every Claude Code session on this Mac runs `../elvis/plugin/bin/elvis` as its hook.
- The same command reports the installed version as 0.2.1 beside a folder version of 0.4.0. The first figure is only the install record. The hook that runs is the folder's.
- `~/.local/bin/elvis` is a link to `plugin/bin/elvis` in the checkout.
- Jack's `~/.zshrc` loads the zsh shell integration from the same binary. It reports his own test runs, commits, and pushes to Elvis.

A build in the checkout therefore changes the hook for every session, and the `elvis` on the `PATH`, at once. The contributor instructions list the `make` targets that do this and how to build without it.

## Work without disturbing him

- A copy of Elvis is usually running on Jack's screen. Use a separate instance with `ELVIS_HOME` set for anything that sends events or films frames, and add `ELVIS_HEADLESS` so that no second dog appears. A headless copy still plays sounds.
- Tell Jack before starting a copy with a window. On 12 November 2026 a second dog appeared on his screen, and he closed his own Elvis thinking it was the extra.
- Starting, quitting, or restarting the Elvis on screen needs Jack's request.
- `make test` is safe while he is on screen, because every test gets its own temporary home. So is `elvis status`, which only reads.
- To test an install without touching Jack's settings, set `CLAUDE_CONFIG_DIR` to a scratch directory for the `claude plugin` commands.
- To see what Claude Code sends, load a scratch plugin whose hooks append their payload to a file, with `claude -p ... --plugin-dir <scratch plugin>`.
- To see what Elvis sends on, copy `plugin/` with a new build to a scratch directory, listen on a scratch socket, and run `claude -p ... --plugin-dir <that copy>` with `ELVIS_HOME` set to the socket's directory. Start the listener first: with nothing listening there, the session-start hook launches a new Elvis with a window.
- A plugin loaded with `--plugin-dir` replaces the installed one of the same name for that session. Each `claude -p` run costs a short headless session.

## What an agent cannot do here

- Screen capture was not permitted from the agent shell on 12 November 2026 and was not tried again on 13 November. Check how he looks through `make sheets` and filmed frames.
- An agent cannot hear him. The bark and yip were checked for length, loudness, and timing, not by ear.
- This Mac has the Command Line Tools without Xcode. `swift test --arch x86_64` fails to link, because they ship the Swift Testing library for Apple silicon only. Rosetta 2 was installed on 12 November 2026, so an Intel binary runs under `arch -x86_64`. To get one without replacing `plugin/bin/elvis`, build with `swift build -c release --arch arm64 --arch x86_64 --scratch-path <scratch>` and take the Intel half of a copy with `lipo -thin x86_64`. Under Rosetta the Intel half has run only `elvis help`, `elvis version`, and `elvis status`.

## What the permission classifier refuses

The agent's permission classifier has refused these even after Jack asked for the work in chat. Approval in a question dialog has worked for the three it was tried on, so ask that way before handing Jack a command to run.

- Creating and pushing a release tag, on 12 November 2026. It went through once Jack approved it in a dialog, and again on later releases when he approved before the attempt.
- Running a downloaded binary, on 12 November 2026. On later releases the released binary ran from a scratch profile after approval in a dialog.
- Creating `~/.claude/CLAUDE.md`, on 13 November 2026. It went through after approval in a dialog.
- `claude plugin marketplace add` and `claude plugin install` against his real settings, on 12 November 2026. Jack ran the install himself.
- Appending to `~/.zshrc`, on 12 November 2026. Jack edited it himself.

The classifier let `git push origin main`, `make install`, `elvis restart`, and `claude plugin update elvis@elvis` through without a dialog. That shows only what the classifier allows. The contributor instructions say which of these need Jack's request, and they still do.
