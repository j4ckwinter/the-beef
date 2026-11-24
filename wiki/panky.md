# Panky on the Windows PC

[Panky](https://github.com/j4ckwinter/panky) is Jack's AI teammate: a React web app, a Node backend with SQLite, and local models through Ollama. Its checkout is `../panky`, relative to this repository's root.

The project owns its own facts. Read its [contributor instructions](../../panky/AGENTS.md) for the commands, the security rules, and which milestones are authorized. Read its [running guide](../../panky/docs/running-locally.md) for running it locally, the local model, the Windows launcher and backups. The [project brief](../../panky/brief.md) holds the milestone detail, and the [architecture case study](../../panky/docs/architecture.md) follows a reply through streaming, cancellation, and recovery.

This page holds only what that repository cannot: how Panky is set up on Jack's Windows PC, and what an agent needs to know to work without disturbing it. The other wiki pages describe Jack's Mac. This one describes the PC.

## The checkout is the production host

Checked on 15 November 2026 against `1853be26378a84338c2b07a32dec0d541c53ba71`. These points were read from the source, not observed running.

- The public site at [panky.vercel.app](https://panky.vercel.app) sends every `/api` request to an ngrok address, set in [vercel.json](../../panky/apps/web/vercel.json). The [launcher](../../panky/scripts/start-panky.ps1) opens that tunnel to `127.0.0.1:3001` on this PC. When the launcher is running, the backend in this checkout is production.
- The launcher runs `apps/server/dist/index.js` with `apps/server/.env`. `pnpm build` rewrites `dist`, so the next launcher start runs whatever was last built in the checkout.
- `start-panky.ps1 -Update` runs `git pull --ff-only`, installs, and builds. It builds the branch that is checked out, so leave the checkout on the branch Jack expects.
- Since 20 November 2026 Panky's [contributor instructions](../../panky/AGENTS.md) let an agent commit each completed change on `main` and push it without asking, which redeploys the web app. Since 15 November 2026 they also hold its decision-owners table and conventions.
- On 16 November 2026 `ede0eca` was pushed to `main`, and GitHub showed a successful `Vercel` status on it. Jack reported that he then updated this checkout, started the launcher, and that `pnpm --filter @panky/server test` passed on this PC, which covers the backup's file rename on Windows. He reported that **Account → Status** then showed what was expected: the running backend built from `ede0eca`, with Ollama reachable.
- Vercel builds what is pushed to GitHub. On 15 November 2026 GitHub showed a successful `Vercel` commit status on the checked revision, the head of `main`, linking to a deployment in the Vercel project `panky`. Treat a push to `main` as a deploy of the public site. Whether that deployment was promoted to production was not checked in Vercel, and the checkout has no `.vercel` folder, so the Vercel CLI is not linked here.

## What this PC has

Checked on 15 November 2026 with Claude Code 2.1.325.

- Windows 11 Pro with an NVIDIA GeForce RTX 3080 with 10 GB of memory, and 32 GB of RAM. The agent shell offers Windows PowerShell 5.1 and Git Bash.
- Node.js 24.20.0 and pnpm 12.16.1. Panky asks for Node 24 or newer and pins that pnpm version.
- Ollama 0.40.16, installed for Jack's user account. A shortcut in the Startup folder launches it at login. It answered on `127.0.0.1:11434`. The user environment variables `OLLAMA_NO_CLOUD` and `OLLAMA_GO_TEMPLATE` are both `1`, as the running guide asks, and `OLLAMA_HOST` is unset.
- Ollama held two models: `qwen3:8b` and `panky-qwen3:8b`. `panky-qwen3:4b`, the earlier configuration, was not installed. Commit `8751e45`, pushed the same day, made the 8b model the documented one. `apps/server/.env` sets `MODEL_NAME=panky-qwen3:8b`. A repository-wide search printed that line by accident.
- ngrok 3.39.11, installed from the Microsoft Store.
- Playwright's Chromium is installed under `%LOCALAPPDATA%\ms-playwright`.
- `apps/server` and `apps/web` each have `.env` and `.env.development`. Apart from that one line, their contents were not read. The running guide describes the development files as moving `pnpm dev` to port 3002 and its own database.
- `apps/server/data` holds the live database `panky.sqlite`, the development database `panky-dev.sqlite`, and a `chatgpt` folder. The folder was not opened. The example configuration puts the ChatGPT subscription credentials there.
- No backend, tunnel, or development server was running. Nothing answered on ports 3001, 3002, or 5173.
- `~/.claude/CLAUDE.md` imports the two steering files from `~/Documents/dev/the-beef`, so a Claude Code session that starts in the Panky checkout loads Jack's steering. The file was created on 15 November 2026.

## Work without disturbing it

- Do not read or print `apps/server/.env`, and exclude `.env` files from any search of the checkout. Git ignores them, but `grep -r` does not. The example file shows it holds the owner's bearer token and the Notion secrets and key. Git ignores every `.env` file except the examples.
- Starting or stopping the launcher needs Jack's request. So does restarting Ollama, changing its environment variables, or creating and removing `panky-` models. `ollama create panky-qwen3:8b` replaces the model the backend is configured to ask for by name.
- The browser tests are built to stay clear of production. [playwright.config.ts](../../panky/playwright.config.ts) starts its own backend on port 3101 and web app on port 5174, with an in-memory database and the mock model. This was read from the configuration. The tests were not run for this page.
- `pnpm check` runs the backend tests. Panky's instructions require isolated test databases and forbid test conversations in the live one. That rule was not audited test by test for this page.
- `pnpm evaluate:ollama --run` uses an in-memory database and the real Ollama. It shares the graphics card with any live reply, so expect it to slow production while it runs. That is an inference and was not measured.
- SQLite stores chats in plaintext. Treat `apps/server/data` as private, including the `backups` folder inside it. Since `ede0eca`, `pnpm backup` copies the live database while the backend runs. Restoring a copy still needs the backend stopped.
- The web app no longer uses [Pancake UI](https://github.com/j4ckwinter/pancake-ui). On 20 November 2026 the move to shadcn/ui and Tailwind was pushed to `main`, followed by Tech Test (`cfe1ea2`). The same day, at 14:09, the launcher's `-Update` pulled `8c9e970` into this checkout, built it, and started the backend and ngrok; the built server is stamped `8c9e970`. GitHub's `Check` run on `8c9e970` passed. Jack reported that **Connections → ChatGPT** was connected and that a live Tech Test capture got an answer that read the task. The handover file was then removed in `078ad9c` and pushed.
- Until `aa49110`, Biome's file list excluded only the root `data` folder. On this PC `pnpm check` then failed on the ChatGPT credentials in `apps/server/data/chatgpt` and printed them. Do not run Biome on this checkout from a revision older than that.
- Later on 20 November 2026 a UX pass and Tech Test changes were pushed to `main`, ending at `fc599f3`. Two more polish passes followed that evening, ending at `6e04b93`. `pnpm build` ran in this checkout after each, so `apps/server/dist` now holds `6e04b93`. The backend started at 14:09 kept running from memory and was not restarted, so it still serves `8c9e970` until the launcher restarts. The deployed web app sends Tech Test captures as `techTest.screenshots`, which the running `8c9e970` backend rejects, so Tech Test captures fail until the launcher restarts on the new build. Jack disconnected ChatGPT the same day, so Tech Test needs that restart anyway.
- Later still on 20 November 2026 a third polish pass was pushed to `main`, ending at `95b4943`, and GitHub showed a successful `Vercel` status on it. It adds a server change: replies record the model that wrote them, in a new nullable `answeredBy` column the backend adds to the live database on its next start. On 21 November 2026 Jack reported that the PC had been rebuilt and restarted on this build, so replies now record their model. The rebuilt revision was not checked from this session.
- On 24 November 2026 two server changes were pushed to `main`, ending at `f6faad3`: a long streamed reply no longer fails as "invalid response" before the output limit, and a shorter Tech Test script. Both are server-side, so the PC serves them only after the launcher rebuilds and restarts. That restart was not checked from this session.

## Source links

The sibling links above work locally. For readers on GitHub, these preserve the inspected version:

- [Contributor instructions](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/AGENTS.md), [README](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/README.md), and [project brief](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/brief.md).
- [Online backup in the README](https://github.com/j4ckwinter/panky/blob/ede0eca0d0d7e5d482f48afbbdfc9b975dfd4174/README.md#back-up), at `ede0eca`.
- [Launcher](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/scripts/start-panky.ps1), [deployment routing](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/apps/web/vercel.json), [browser test configuration](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/playwright.config.ts), and [example configuration](https://github.com/j4ckwinter/panky/blob/1853be26378a84338c2b07a32dec0d541c53ba71/apps/server/.env.example).
