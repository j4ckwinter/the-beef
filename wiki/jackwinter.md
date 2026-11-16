# jackwinter on this Mac

`jackwinter` is Jack's planned minimal portfolio. It is meant to replace [Winterbot](winterbot.md) as his main site, with a single page in the style of [maxkatz.me](https://maxkatz.me/). Its checkout is `../jackwinter`, relative to this repository's root. This page describes the Mac.

The project owns its own facts. Read its [contributor instructions](../../jackwinter/AGENTS.md) and [README](../../jackwinter/README.md).

## The state of the checkout

Checked on 16 November 2026.

- Created that day as a local Git repository on `main`, with one commit holding the README and `AGENTS.md`. No stack is chosen and nothing is built.
- It has no remote. `j4ckwinter/jackwinter` did not exist on GitHub. Creating it, pushing and deploying need Jack's request.

## The reference site

Checked on 16 November 2026 by fetching `https://maxkatz.me/`.

- One page: a header with name, title and icon links (X, GitHub, LinkedIn, email, résumé PDF); a casual lowercase bio with "Book a call" and message buttons; a yearly activity strip; Experience; Skills grouped by area; Projects with GitHub star counts. Experience and Skills have "See more" toggles.
- Its response headers report `Server: Vercel` and `x-powered-by: Next.js`. The HTML loads `_next` assets and references Geist and Tailwind-style classes.

## How it relates to the other projects

- It will take over from Winterbot as the front door. Whether Winterbot's Vercel domain moves or stays has not been decided.
- Which projects it presents has not been decided. Winterbot presents Pancake Stack and `brain-cache`.
