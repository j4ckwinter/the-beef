# same again on this Mac

same again records a real click-through of a web app with a script tag, replays it in Chromium with time, randomness, data responses, settling and CSS animations pinned, and diffs the screenshots against a second build. It also picks the recorded sessions a code change can affect, from coverage. It came out of the idea queue and Jack asked for it to be built directly on 24 November 2026, rather than in a queue build. Its checkout is `../same-again`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../same-again/AGENTS.md) and [README](../../same-again/README.md).

## The state of the checkout

Checked on 24 November 2026.

- It is a local Git repository on `main` with no remote. Nothing is on GitHub or npm; the npm name `same-again` was free when checked. Creating a repository or publishing needs Jack's request.
- It runs TypeScript directly on Node 26, with no build step for the engine. `shop/` and `report/` are separate npm packages and must be built before the engine tests.
- It uses the Chromium that Playwright 1.65.0 downloads into `~/Library/Caches/ms-playwright`. Playwright is pinned to 1.65.0 because that version's browsers were already installed.
- The tests drive a real Chromium and start the demo shop on ports 5196 to 5198. `npm run record:examples` and `npm run demo:gif` use port 5180.
- Milestone 4 of the idea, measuring replays on an open-source React app Jack didn't write, is not done. Delegating it was blocked by the permission check, because it meant cloning, installing and running a third-party repository unsupervised. It needs Jack's decision on how to run it.

## Showcase

- Idea: the idea file had no sources. No dated post prompted it.
- Demo: `../same-again/docs/demo.gif`, about 22 seconds, at the top of the README. `npm run demo:gif` regenerates it from real runs.
- Status: not ready. There is no remote repository, and the real-app result the idea calls the one that counts is missing.
