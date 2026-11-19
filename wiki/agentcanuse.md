# agentcanuse on this Mac

[agentcanuse](https://github.com/j4ckwinter/agentcanuse) is a scoreboard of the browser engines AI agents use. It runs Chromium, Lightpanda and Obscura against 124 real sites, scores each visit, and shows a leaderboard, a side-by-side view per site and a diff between engine releases. It came out of the idea queue, where it started as headless.fyi and was renamed because that domain was taken, and was built in the queue build on 19 November 2026. Its checkout is `../agentcanuse`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../agentcanuse/AGENTS.md) and [README](../../agentcanuse/README.md).

## The state of the checkout

Checked on 19 November 2026.

- On Jack's request the same day, the GitHub repository was made public and the site deployed. Jack bought `agentcanuse.com` through Vercel. It and `www.agentcanuse.com` are assigned to the Vercel project `agentcanuse` in the team `jacks-projects-8a38ccc4`. The first production deployment was made with `npx vercel@66.2.0 deploy --prod` from the checkout at `c281466`. Loading https://agentcanuse.com in headless Chromium showed the leaderboard and site screenshots with no failed requests.
- `vercel link` could not connect the project to GitHub. Jack connected it in the Vercel dashboard the same day, and a push to `main` (`9b7cb9a`) then produced a production deployment with a successful `Vercel` commit status.
- The Vercel CLI is not installed globally. `npx vercel@66.2.0` used the login already saved on this Mac, as `jackwinter10-4598`. `vercel link` wrote `.vercel` and an `.env.local` holding a Vercel OIDC token. Both are git-ignored.
- `public/data` started with two runs from this Mac's home connection. The first pinned Lightpanda 1.0.1 and Obscura v0.2.4 so the release diff had something to compare; the second ran the pins in `engines.json`. Each run records its origin, `home` or `data-centre`.
- Kitesurf is not in any run. Its README warns against opening untrusted sites with a local Kitesurf, and hosting it needs a Cloudflare Workers Paid plan. The runner drives it only when `KITESURF_ENDPOINT` is set.
- On Jack's go-ahead, the `Survey` workflow runs nightly at 03:17 UTC as a `data-centre` run, commits it to `main`, and Vercel deploys it. A dispatched run on 19 November (`e1cdc06`) completed with all three engines and reached https://agentcanuse.com.
- Two things broke on the way there. Chromium would not start on GitHub's Ubuntu runners until the workflow lifted Ubuntu's restriction on unprivileged user namespaces, which keeps Chrome's sandbox on. And a survey's push conflicted with a concurrent change to `index.json`, so the index is now rebuilt from the run files before each push. A run that loses an engine other than an unconfigured Kitesurf now fails instead of publishing a partial leaderboard.
- On 19 November the site list grew from 30 to 124. Candidates were dropped when their `robots.txt` refused `agentcanuse` (seven) or Chromium could not read them (twelve). Phrases were checked against a Chromium visit; the 19 sites that block Chromium list only their name. The first 124-site run, from home, is `acc498c`: 26 sites separated the engines.
- Only the latest run keeps its WebP thumbnails, and only for sites where the engines disagreed, since the site shows no others; saving a run prunes the rest. The working tree stays near 1 MB of data, but each run still adds about 0.9 MB of thumbnails to Git history, roughly 330 MB a year. Shrinking history would mean rewriting it or moving thumbnails to object storage; neither has been done.
- A `Watch releases` workflow checks Lightpanda's and Obscura's latest stable GitHub releases every six hours. On a new release it commits the pin to `engines.json` and dispatches a survey. On 19 November it was exercised on a throwaway branch pinned to Obscura v0.2.6: it committed `chore: pin obscura v0.2.7` and started a survey on `main`. The branch was deleted afterwards.
- The first survey after pruning was added failed to push, because pruning left tracked changes that stopped `git pull --rebase`. The commit step now restores `public/data` before pulling and reruns `npm run tidy`; run `e2c7fc4` then saved, pruned and deployed.
- Engine builds download into `.cache/engines`, which Git ignores. On this Mac it held Chromium headless shell 158.0.8127.36, Lightpanda 1.0.1 and 1.0.4, and Obscura v0.2.4 and v0.2.7.
- Port 4319 on this Mac is held by an SSH tunnel. Don't use it for a preview server.
- `docs/demo.gif` was made with a throwaway recorder outside the repository: headless Chromium driving `vite preview`, frames encoded with gifenc. Nothing in the repository regenerates it.

## Showcase

- Idea: Cloudflare open-sourced its Kitesurf agent browser on [13 November 2026](https://blog.cloudflare.com/kitesurf-open-source/), and every comparison of agent browser engines so far has been a one-off, for example [Lightpanda's own](https://lightpanda.io/blog/posts/benchmarking-lightpanda-for-agents) and [an independent one](https://jacar.es/en/lightpanda-vs-obscura-headless-browser-benchmark/), neither dated on the page. [Help Net Security](https://www.helpnetsecurity.com/?p=391308) covered self-hosting Kitesurf in November 2026.
- Demo: `../agentcanuse/docs/demo.gif`, about 25 seconds, at the top of the README.
- Status: ready to post. The repository is public, the README shows the demo and how to run it, and the site is live at https://agentcanuse.com.
