# Code style

Follow the repository you are editing. Its formatter, linter, `tsconfig`, and `AGENTS.md` or `CLAUDE.md` override this file.

## TypeScript

`strict` is on in brain-cache, deedspan, fantasy-pancake, pancake-ui, panky, and padel-potato. winterbot extends `astro/tsconfigs/strict`. Leave strict on.

deedspan's root tsconfig also sets `noUncheckedIndexedAccess`, `exactOptionalPropertyTypes`, and `verbatimModuleSyntax`. panky's base tsconfig sets `noUncheckedIndexedAccess` and `verbatimModuleSyntax`, and not `exactOptionalPropertyTypes`. Use those flags only where that repo's tsconfig already sets them.

Packages that set `"type": "module"` stay ESM: brain-cache, deedspan, fantasy-pancake, pancake-ui, panky, and winterbot. brain-cache imports local modules with `.js` extensions because production runs the built JavaScript. Apply that only in repos that already do it.

## Formatting

Run the repo's formatter. Do not pick a new quote style for it.

- deedspan and padel-potato set Prettier `singleQuote: true`. deedspan also sets `trailingComma: "all"`.
- panky formats with Biome 2.6.4, two-space indent, and a small explicit lint preset rather than the recommended preset.
- deedspan's `.editorconfig` is UTF-8, LF, two-space indent, and a final newline. Markdown there does not trim trailing whitespace.
- fantasy-pancake and pancake-ui run Prettier with no config file, so they use Prettier defaults. winterbot uses Prettier with `prettier-plugin-astro` and no quote override. brain-cache has no Prettier or Biome config.
- padel-potato sets Prettier `endOfLine: "lf"`. deedspan's history includes a fix to keep LF on Windows checkouts. Preserve LF where the repo already does.

## Shape of a change

Match the names, folders, and patterns already next to the edit. padel-potato says to inspect existing patterns before adding architecture. brain-cache says to follow existing patterns. fantasy-pancake says to add behaviour to the module that already owns it.

Keep the current module boundaries. fantasy-pancake keeps fetching and persistence out of presentation components, and the model free of React and HTTP. panky keeps `apps/web`, `apps/server`, and `packages/shared` apart, and colocates backend tests with the code they exercise. pancake-ui keeps runtime components in `src/components`, tokens in `src/foundations`, and stories in `src/stories`. Read that repo's agent file before moving code across a boundary.

Line-count rules are local. pancake-ui lints runtime components at 180 lines, excluding comments and blanks, and forbids splitting code only to get under the cap. panky treats files approaching 300 lines as a review trigger, not a limit. Do not copy either number into a repo that does not use it.

Honour a repo's dependency bans. brain-cache's `CLAUDE.md` rules out LangChain, LlamaIndex, the Vercel AI SDK, Postgres, Redis, the old `vectordb` package, and ts-node.

For a comment cleanup, follow `~/repos/pancake-stack/skills/pancake/references/comment-cleanup.md` in the pancake-stack checkout. Leave comments that record a constraint the code cannot show.

Spelling follows the file you are editing. The public portfolio uses British spelling (`specialise`, `optimisation`). Some repo docs use American spelling (`behavior`, `organizing`). Do not mass-correct either.

## Where this came from

Read from the default-branch tips on 12 Nov 2026: brain-cache `c74a144`, pancake-ui `3930bc7`, panky `1853be2`, deedspan `d3a6456`, fantasy-pancake `ef65c97`, winterbot `3138059`, padel-potato `728700e`, plus those repos' tsconfig, ESLint, Prettier, Biome, and EditorConfig files. fpl-radar was not read.
