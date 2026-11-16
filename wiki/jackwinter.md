# jackwinter on this Mac

[jackwinter](https://github.com/j4ckwinter/jackwinter) is Jack's planned minimal portfolio. It is meant to replace [Winterbot](winterbot.md) as his main site, with a single page in the style of [maxkatz.me](https://maxkatz.me/). Its checkout is `../jackwinter`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../jackwinter/AGENTS.md) and [README](../../jackwinter/README.md).

## The state of the checkout

Checked on 16 November 2026.

- Jack chose Astro with Tailwind. The scaffold renders a header from `src/content/profile.ts`; `npm run check` and `npm run build` passed on the Mac with Node 26.13.0.
- `main` is at `49f8bdf` and level with `origin/main`. The public GitHub repository `j4ckwinter/jackwinter` was created that day at Jack's request.
- It has no Vercel project, no CI workflow and no tests. Deploying needs Jack's request.

## The reference site

Checked on 16 November 2026 by fetching `https://maxkatz.me/`.

- One page: a header with name, title and icon links (X, GitHub, LinkedIn, email, résumé PDF); a casual lowercase bio with "Book a call" and message buttons; a yearly activity strip; Experience; Skills grouped by area; Projects with GitHub star counts. Experience and Skills have "See more" toggles.
- Its response headers report `Server: Vercel` and `x-powered-by: Next.js`. The HTML loads `_next` assets and references Geist and Tailwind-style classes.

## How it relates to the other projects

- It will take over from Winterbot as the front door. Whether Winterbot's Vercel domain moves or stays has not been decided.
- Which projects it presents has not been decided. Winterbot presents Pancake Stack and `brain-cache`.
