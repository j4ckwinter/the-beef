# Code style

Follow the repository you are editing. Its formatter, linter, `tsconfig`, and `AGENTS.md` or `CLAUDE.md` override this file.

## TypeScript

Leave `strict` on when that repo already enables it. Use extra flags such as `noUncheckedIndexedAccess`, `exactOptionalPropertyTypes`, and `verbatimModuleSyntax` only where that repo's tsconfig already sets them.

Keep a package ESM when it sets `"type": "module"`. Use `.js` extensions on local imports only in a repo that already does, because that choice belongs to how that package is built.

## Formatting

Run the repo's formatter. Do not pick a new quote style, indent, or line ending for it. Preserve LF where the repo already does.

## Shape of a change

Match the names, folders, and patterns already next to the edit. Keep the current module boundaries. Read that repo's agent file before moving code across one.

Line limits, dependency bans, and folder layouts are local. Do not copy a number or a ban from one repo into another that does not use it.

For a comment cleanup, follow `~/repos/pancake-stack/skills/pancake/references/comment-cleanup.md` in the pancake-stack checkout. Leave comments that record a constraint the code cannot show.

Spelling follows the file you are editing. Do not mass-correct a repo from British spelling to American, or the other way.
