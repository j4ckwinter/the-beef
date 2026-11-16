# jackwinter on this Mac

[jackwinter](https://github.com/j4ckwinter/jackwinter) is Jack's planned minimal portfolio. It is meant to replace [Winterbot](winterbot.md) as his main site, with a single page in the style of [maxkatz.me](https://maxkatz.me/). Its checkout is `../jackwinter`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../jackwinter/AGENTS.md) and [README](../../jackwinter/README.md).

## The state of the checkout

Checked on 16 November 2026.

- Jack chose Astro with Tailwind. The page has a header, bio, GitHub activity grid, experience, education, skills and projects. The roles, skills, email, LinkedIn and CV were copied from Winterbot's plain portfolio; the bio and project blurbs are drafts Jack has not reviewed.
- `main` is at `1886863` and level with `origin/main`. `703b17e` redesigned the page after the reference site (icon links, a GitHub tile grid, an experience timeline that morphs into a list with View Transitions, expandable skills); `1886863` softened dark-mode text, gave education its own section, widened skills from Jack's repos and sorted projects by stars. GitHub Actions passed and Vercel reported a successful deploy on both.
- Star counts and contributions are fetched at build time. The activity strip needs a `GITHUB_TOKEN`; without one, or when GitHub fails, the build leaves that data out and warns.

## How it is deployed

Checked on 16 November 2026.

- Jack imported the repository into the Vercel project `jackwinter` from the dashboard. The CLI is not installed on the Mac and the checkout has no `.vercel` folder.
- It is served at [www.jackwinter.xyz](https://www.jackwinter.xyz/); `jackwinter.xyz` redirects there with a 308. GitHub showed a successful `Vercel` status on `18f2071`.
- Vercel holds `GITHUB_TOKEN`, a fine-grained token Jack made with read-only access to public repositories. The live page showed 2,114 contributions, matching GitHub's API that day, and brain-cache's 11 stars. When the token expires, the activity strip disappears until it is replaced.
- Treat a push to `main` as a deploy of the public site. The numbers only change when the site rebuilds; no scheduled rebuild exists.

## The reference site

Checked on 16 November 2026 by fetching `https://maxkatz.me/`.

- One page: a header with name, title and icon links (X, GitHub, LinkedIn, email, résumé PDF); a casual lowercase bio with "Book a call" and message buttons; a yearly activity strip; Experience; Skills grouped by area; Projects with GitHub star counts. Experience and Skills have "See more" toggles.
- Its response headers report `Server: Vercel` and `x-powered-by: Next.js`. The HTML loads `_next` assets and references Geist and Tailwind-style classes.

## How it relates to the other projects

- It is meant to take over from Winterbot as the front door, and links to Winterbot as a project. Winterbot still serves `winterbyte.vercel.app`, and nothing redirects from it yet.
- It presents Pancake Stack, `brain-cache`, Pancake UI, Elvis and Winterbot. Their links live in `src/content/projects.ts`.
