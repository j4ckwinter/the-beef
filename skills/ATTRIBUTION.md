# Attribution

These workflows are copied from [j4ckwinter/pancake-stack](https://github.com/j4ckwinter/pancake-stack) at `e4f206169dd6e4db83e8b4c08c36b9bbf0d9c8da` so this home repo can run without that checkout.

The source tree had no `LICENSE` file at that commit. This copy is here because Jack asked for the workflows in the home repo. It does not add a license.

Folder layout matches the source `skills/` tree, including each `SKILL.md`, `references/`, and `agents/openai.yaml`. Plugin manifests (`plugin.json`, marketplace files) stay in pancake-stack. They were not copied.

Relative links between these files are unchanged. One path pointed outside the tree and was rewritten: `skills/setup/SKILL.md` now links to the configuration note at that pancake-stack commit, and to `~/repos/pancake-stack/docs/configuration.md` after that repo is cloned.

`$pancake-stack:<skill>` and `/pancake-stack:<skill>` in the text are the plugin names in the source repo. In this repo, read `skills/<skill>/SKILL.md` for the same workflow.
