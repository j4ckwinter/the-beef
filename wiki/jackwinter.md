# jackwinter on this Mac

[jackwinter](https://github.com/j4ckwinter/jackwinter) is Jack's planned minimal portfolio. It is meant to replace [Winterbot](winterbot.md) as his main site, with a single page in the style of [maxkatz.me](https://maxkatz.me/). Its checkout is `../jackwinter`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../jackwinter/AGENTS.md) and [README](../../jackwinter/README.md).

## The state of the checkout

Checked on 17 November 2026.

- Jack chose Astro with Tailwind. The page has a header, bio, GitHub activity grid, experience, education, skills and projects. The roles, skills, email, LinkedIn and CV were copied from Winterbot's plain portfolio; the bio and project blurbs are drafts Jack has not reviewed.
- `main` is at `b28fca8` and level with `origin/main`. Beyond the redesign it has agent pages, latest commits under Activity, theme-coloured company logos, a share card, structured data, robots, a sitemap, a 404 page, tile tooltips with a streak and busiest-day line, a clickable timeline with role durations, project versions, linkable headings, a print stylesheet, relative commit dates, a light/dark toggle, a download cv button with its size, a QR code on the printed page, an apple touch icon, a footer date taken from the last commit to `src` or `public` and linked to it (Vercel builds can read the git history; checked 17 November 2026), heading links that copy themselves, a console note, a high-contrast palette, balanced headings, machine-readable role dates, tooltips that stay after a tap, and a KTO case study at `/work/kto` with its own share card, reading time, section links that follow the reader, metrics linked to their sections, published and updated dates, print styles and a glide from its role. GitHub Actions and Vercel passed on the latest release.
- `public/Jack-Winter-CV.pdf` is a copy of `~/Documents/Jack Winter CV.pdf` as of 16 November 2026. When Jack updates that file, copy it in again.
- Star counts and contributions are fetched at build time. The activity strip needs a `GITHUB_TOKEN`; without one, or when GitHub fails, the build leaves that data out and warns.

## How it is deployed

Checked on 16 November 2026.

- Jack imported the repository into the Vercel project `jackwinter` from the dashboard. The CLI is not installed on the Mac and the checkout has no `.vercel` folder.
- It is served at [www.jackwinter.xyz](https://www.jackwinter.xyz/); `jackwinter.xyz` redirects there with a 308. GitHub showed a successful `Vercel` status on `18f2071`.
- Vercel holds `GITHUB_TOKEN`, a fine-grained token Jack made with read-only access to public repositories. The live page showed 2,114 contributions, matching GitHub's API that day, and brain-cache's 11 stars. When the token expires, the activity strip disappears until it is replaced.
- Treat a push to `main` as a deploy of the public site. The GitHub data only changes when the site rebuilds. `.github/workflows/rebuild.yml` calls a Vercel deploy hook every morning at 05:00 UTC. The hook is stored as the `VERCEL_DEPLOY_HOOK` repository secret, set on 16 November 2026; a manual run that day succeeded and the live page's ETag changed, confirming a rebuild.

## The reference site

Checked on 16 November 2026 by fetching `https://maxkatz.me/`.

- One page: a header with name, title and icon links (X, GitHub, LinkedIn, email, résumé PDF); a casual lowercase bio with "Book a call" and message buttons; a yearly activity strip; Experience; Skills grouped by area; Projects with GitHub star counts. Experience and Skills have "See more" toggles.
- Its response headers report `Server: Vercel` and `x-powered-by: Next.js`. The HTML loads `_next` assets and references Geist and Tailwind-style classes.

- A weekly link check (`.github/workflows/links.yml`) passed on 16 November 2026. npmjs.com and LinkedIn refuse automated checkers, so npm links are checked through the registry and LinkedIn's 999 status counts as a pass.
- Vercel Web Analytics was enabled on 16 November 2026. The insights route only appeared after a new deployment, so after toggling analytics, trigger one (the rebuild workflow is enough).
- `vercel.json` redirects Winter Town's old paths (`/portfolio`, `/places/*`); `/work/kto` is now a real page on this site. The redirects take effect for old links once Jack moves `winterbyte.vercel.app` from the winterbot project to this one with a redirect to `www.jackwinter.xyz`; that move had not been made on 17 November 2026.

## How it relates to the other projects

- It is meant to take over from Winterbot as the front door, and links to Winterbot as a project. Winterbot still serves `winterbyte.vercel.app`, and nothing redirects from it yet.
- It presents Pancake Stack, `brain-cache`, Pancake UI, Elvis and Winterbot. Their links live in `src/content/projects.ts`.
