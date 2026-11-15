# Nod on this Mac

[Nod](https://github.com/n8n-io/nod) is n8n's open source personal agent. It runs as one Node server with Docker containers for PostgreSQL, a sandbox workspace, and a browser. Jack works on a fork, [j4ckwinter/nod](https://github.com/j4ckwinter/nod). Its checkout is `../nod`, relative to this repository's root.

The project owns its own facts. Read its [contributor instructions](../../nod/AGENTS.md) for the rules, the architecture, and the safety invariants. Read [CONTRIBUTING](../../nod/CONTRIBUTING.md) for the checks and pull request conventions, and [Install from source](../../nod/docs/src/content/docs/get-started/install-from-source.mdx) for requirements, day-to-day commands, and troubleshooting.

This page holds only what that repository cannot: how the fork is arranged, and how Nod is set up on Jack's Mac.

## How the fork is arranged

Checked on 15 November 2026 against `15397ab4`.

- `origin` is Jack's fork and `upstream` is `n8n-io/nod`. The fork was made and cloned on 15 November 2026 with `main` level with upstream.
- Nod is an upstream project, so its instructions and style come before Jack's coding standards. Its first rule is not to push, deploy, or publish without explicit authorization. That covers pushes to the fork too.
- A pull request to upstream leaves Jack's account and reaches n8n's maintainers. It needs his request each time.

## What this Mac has for running it

Checked on 15 November 2026.

- Node.js 26.13.0 and pnpm 12.16.1 come from Homebrew. Nod asks for Node.js 24.21.0 or newer.
- Corepack is not installed, so the guide's `corepack enable` step fails here. It was not needed: inside the checkout `pnpm -v` reports 10.34.5, the version `package.json` pins, because pnpm switches to it by itself.
- Docker runs under Colima. Jack chose it in a question dialog on 15 November 2026, when this Mac had no container runtime. Homebrew installed Colima 0.10.3, Docker 29.9.3, Compose 5.7.1, and Buildx 0.39.0. `~/.docker/config.json` was created with `cliPluginsExtraDirs` pointing at `/opt/homebrew/lib/docker/cli-plugins`, which is how `docker` finds the two plugins.
- The Colima VM was created with `colima start --cpu 4 --memory 8`. It has 4 CPUs, 8 GB of this Mac's 16 GB, and a 100 GB disk. It is not a Homebrew service, so it does not start at login. Run `colima start` before Nod and `colima stop` to give the memory back.

## What starting it does

Nod first started on this Mac on 15 November 2026 with `pnpm run dev`. The web app answered on `http://127.0.0.1:4310/`, and `/api/session` returned 401 without the access key. Nothing past the start was tried: no onboarding, no model connection, and no task.

- `pnpm run dev` and `pnpm start` both run `scripts/start.mjs`. Use `pnpm run dev`. It reloads on change and leaves usage analytics off. `pnpm start` builds for production and shares usage data with n8n unless `NOD_ANALYTICS_ENABLED=false` is set in `.env`. That difference was read from the source and the configuration page, not observed.
- The first start took about five minutes, most of it building the workspace image at 2.87 GB and the browser image at 1.85 GB. The browser image build logs a Lefthook error about a missing `git`. It is harmless and the build carries on.
- `pnpm install` set up Lefthook hooks in the checkout, `pre-commit` and `pre-push`. Upstream's `lefthook.yml` says what they run.
- The start created `.env` from `.env.example` and a data folder at `.local/`, both ignored by Git. `.env` holds the generated database password.
- It started the compose project `nod-local`: PostgreSQL on `127.0.0.1:54329`, the containers `nod-workspace` and `nod-browser`, a firewall container, and three Docker volumes.
- The server prints an access link ending in `#access=`. The key behind it is in `.local/access-key`. Treat the link as a credential and keep it out of this wiki, commits, and chat.
- The server created the Keychain item `dev.nod.vault` for its Vault key. Saved logins, keys, and cards cannot be read without it, so deleting the item needs Jack's request.
- Stopping takes two steps: Ctrl-C for the server, then `docker compose stop` in the checkout for the containers. The upstream rule against resetting the normal local database covers the `nod-local_postgres-data` volume.

## Source links

The sibling links above work locally. For readers on GitHub, these preserve the inspected version:

- [Contributor instructions](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/AGENTS.md), [CONTRIBUTING](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/CONTRIBUTING.md), and [Install from source](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/docs/src/content/docs/get-started/install-from-source.mdx).
- [Start script](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/scripts/start.mjs), [compose file](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/compose.yaml), and [configuration](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/docs/src/content/docs/deploy/configuration.md).
