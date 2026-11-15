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
- No Docker, Colima, OrbStack, or Podman is installed. The start script calls `docker info` and `docker compose`, so Nod cannot start from source until a container runtime with Compose v2 and Buildx is installed.

## What starting it touches

Read from the start script, the compose file, and the install guide on 15 November 2026. None of it has been observed on this Mac yet.

- `pnpm run dev` and `pnpm start` both run `scripts/start.mjs`. Use `pnpm run dev`. It reloads on change and leaves usage analytics off. `pnpm start` builds for production and shares usage data with n8n unless `NOD_ANALYTICS_ENABLED=false` is set in `.env`.
- The script installs dependencies when the lockfile changed. The install sets up Lefthook hooks in the checkout: Prettier and, when it is installed, gitleaks before a commit, and `pnpm run lint` before a push.
- It creates `.env` from `.env.example` and a data folder at `.local/`, both ignored by Git. `.env` holds the generated database password.
- It starts the compose project `nod-local`: PostgreSQL on `127.0.0.1:54329`, the containers `nod-workspace` and `nod-browser`, a firewall container, and three Docker volumes.
- The server listens on `127.0.0.1:4310` and prints an access link ending in `#access=`. The key behind that link is in `.local/access-key`. Treat the link as a credential.
- On macOS the server keeps its Vault key in the Keychain item `dev.nod.vault`. Saved logins, keys, and cards cannot be read without it.
- Stopping takes two steps: Ctrl-C for the server, then `docker compose stop` for the containers.

## Source links

The sibling links above work locally. For readers on GitHub, these preserve the inspected version:

- [Contributor instructions](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/AGENTS.md), [CONTRIBUTING](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/CONTRIBUTING.md), and [Install from source](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/docs/src/content/docs/get-started/install-from-source.mdx).
- [Start script](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/scripts/start.mjs), [compose file](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/compose.yaml), and [configuration](https://github.com/n8n-io/nod/blob/15397ab47dcc5c8aa11b269b88a9ff6fbe4a7026/docs/src/content/docs/deploy/configuration.md).
