# agentcanuse on this Mac

[agentcanuse](https://github.com/j4ckwinter/agentcanuse) is a scoreboard of the browser engines AI agents use. It runs Chromium, Lightpanda and Obscura against 30 real sites, scores each visit, and shows a leaderboard, a side-by-side view per site and a diff between engine releases. It came out of the idea queue, where it started as headless.fyi and was renamed because that domain was taken, and was built in the queue build on 19 November 2026. Its checkout is `../agentcanuse`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../agentcanuse/AGENTS.md) and [README](../../agentcanuse/README.md).

## The state of the checkout

Checked on 19 November 2026.

- On Jack's request the same day, the GitHub repository was made public and the site deployed. Jack bought `agentcanuse.com` through Vercel. It and `www.agentcanuse.com` are assigned to the Vercel project `agentcanuse` in the team `jacks-projects-8a38ccc4`. The first production deployment was made with `npx vercel@66.2.0 deploy --prod` from the checkout at `c281466`. Loading https://agentcanuse.com in headless Chromium showed the leaderboard and site screenshots with no failed requests.
- The Vercel project is not connected to GitHub, so a push does not deploy. `vercel link` tried to connect it and was refused, probably because the Vercel GitHub app is limited to selected repositories. Granting it this repository in GitHub settings, then running `npx vercel git connect`, would make pushes to `main` deploy.
- The Vercel CLI is not installed globally. `npx vercel@66.2.0` used the login already saved on this Mac, as `jackwinter10-4598`. `vercel link` wrote `.vercel` and an `.env.local` holding a Vercel OIDC token. Both are git-ignored.
- `public/data` holds two runs from that day, both from this Mac's home connection. The first pinned Lightpanda 1.0.1 and Obscura v0.2.4 so the release diff had something to compare; the second ran the pins in `engines.json`.
- Kitesurf is not in any run. Its README warns against opening untrusted sites with a local Kitesurf, and hosting it needs a Cloudflare Workers Paid plan. The runner drives it only when `KITESURF_ENDPOINT` is set.
- The `Survey` workflow runs only when dispatched by hand. Turning on a nightly schedule while the repository is private would spend Jack's GitHub Actions minutes, and a run from GitHub's data-centre addresses gets blocked more than one from home. Both are open decisions.
- Engine builds download into `.cache/engines`, which Git ignores. On this Mac it held Chromium headless shell 158.0.8127.36, Lightpanda 1.0.1 and 1.0.4, and Obscura v0.2.4 and v0.2.7.
- Port 4319 on this Mac is held by an SSH tunnel. Don't use it for a preview server.
- `docs/demo.gif` was made with a throwaway recorder outside the repository: headless Chromium driving `vite preview`, frames encoded with gifenc. Nothing in the repository regenerates it.

## Showcase

- Idea: Cloudflare open-sourced its Kitesurf agent browser on [13 November 2026](https://blog.cloudflare.com/kitesurf-open-source/), and every comparison of agent browser engines so far has been a one-off, for example [Lightpanda's own](https://lightpanda.io/blog/posts/benchmarking-lightpanda-for-agents) and [an independent one](https://jacar.es/en/lightpanda-vs-obscura-headless-browser-benchmark/), neither dated on the page. [Help Net Security](https://www.helpnetsecurity.com/?p=391308) covered self-hosting Kitesurf in November 2026.
- Demo: `../agentcanuse/docs/demo.gif`, about 25 seconds, at the top of the README.
- Status: ready to post. The repository is public, the README shows the demo and how to run it, and the site is live at https://agentcanuse.com.
