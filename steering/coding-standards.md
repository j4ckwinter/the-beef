# Coding standards

These are Jack's standards for code in any language. They apply in full to his own projects. In a repository that has its own conventions, such as a team codebase or an upstream project, that repository's instructions and existing style come first. Apply these standards where they do not conflict, and raise a conflict that matters instead of choosing silently.

## Give every decision one owner

- Each decision the software makes is made in one place: what an input means, what happens next, how a thing is stored or shown. Put new code with the owner of the decision it makes.
- Keep a short table of decisions and the files that own them in the project's contributor instructions. Update it in the same change that moves or adds an owner.
- State each fact, threshold, and rule once, and give it a name. Refer to it from everywhere else.
- Do not merge code only because it looks alike. Wait until a third case shows the cases are the same thing and would change together.

## Keep the core pure

- Separate deciding from doing. Code that decides takes values and returns values. Code that touches the clock, randomness, files, the network, a database, or the screen sits at the edges and passes its results inward.
- Pass time and randomness in, so any behaviour can be reproduced in a test from its inputs.
- Point dependencies toward the core. The core does not import the user interface, the framework, or a vendor's library. An adapter at the edge does.

## Write clean code

- Name things for what they mean to the caller or the domain. Rename before reaching for a comment.
- Keep a function short enough to read in one pass, and give it one job. Split it when its name needs "and".
- Make the simplest change that meets the outcome. Add an abstraction only when it removes real duplication or protects an invariant that exists today.
- Keep state narrowly owned. Prefer values and pure functions.
- Give a function what it uses, not the whole object it came from. Keep interfaces small enough that every caller uses all of them.
- Choose types that cannot hold an invalid state, where the language allows it.
- Arrange code so that adding a case touches one place. Prefer exhaustive matches with no catch-all branch, so the compiler or type checker lists what a new case needs.
- Give a number that tunes behaviour a name and one home.
- Delete code that nothing calls. Do not leave commented-out code, debug switches, or options added for a future that has not arrived.
- Handle a failure where something can be done about it. Do not swallow an error the user or the caller needs to know about.

## Keep each file to one responsibility

- A file or module holds one responsibility, and its name says which. When it gains a second reason to change, split it before adding more.
- Treat about 300 lines as a prompt to look, not a limit. A long file that does one thing can stay. A short file that does three cannot.
- Split along the owners table. Give a new type or module a file of its own name.
- Widen visibility only for what the new file needs. If a split would expose most of a type's internals, the pieces are not separate, so leave them together.
- Make a split its own commit with no behaviour change. Prove it: the existing tests pass unedited, alongside any stronger before-and-after comparison the project has.

## Leave comments out

Write code that needs no comments. Expect a handful in a whole repository, not a handful per file.

- When something needs explaining, change the code until it does not: name the condition, extract and name the function, or choose a clearer type.
- Put a convention that many files share, such as units, sign conventions, or the meaning of a field, in the project's contributor instructions, not in a comment beside each use.
- A comment may stay only when it stops a reader from making a plausible wrong fix and nothing in the code can carry the reason.
- That rules out comments that describe what code does, documentation comments that restate a name, narration in tests, section banners, commented-out code, and TODO notes.
- These are not commentary and stay where they are required: licence headers, directives that tools read, and reference documentation for an interface the project publishes to others.
- When a change makes a comment untrue, fix or delete it in the same commit. Do not sweep comments out of code you are not otherwise changing unless Jack asks for a cleanup.

## Test behaviour

- Add or update a test with every change to behaviour. Name the test for the behaviour it checks.
- Test through the surface callers use. A test that knows the internals breaks when the code is tidied.
- Keep tests deterministic. No real clock, network, or sleeping to wait for something.
- When a new test passes the first time, break the code briefly to confirm the test can fail.
- Never weaken an assertion or skip a test to get a pass.

## Shape commits well

Whether to commit, and when, follows the project's instructions and the task. When you do commit:

- Make one logical change per commit. Keep a refactor separate from the behaviour change it enables, and a fix separate from an unrelated feature.
- Commit only work that passes its checks.
- Follow the repository's message convention. Where it has none, use Conventional Commits: `type(scope): summary`, with an imperative summary under 72 characters and a body that says why when the summary does not.
- Do not add `Co-Authored-By` trailers or any other line crediting an AI tool, in commit messages or pull request descriptions.
- Stage files by name after reading the status. Keep build output and secrets out of the repository.
- Do not amend or rebase commits that have been pushed.

## Start a new project with these

A session that starts inside a project reads this file only when the host loads Jack's user-level instructions, which the `the-beef` README describes. Other people and other hosts never read it. When setting up a new project of Jack's, write its contributor instructions so the project stands alone:

- the commands that build and check it;
- its owners table;
- these standards, in a short form that keeps the rules most likely to matter there;
- the conventions its code relies on;
- whether committing is expected, and which actions need Jack's request.

The project's own instructions govern that project from then on. Bring a lesson back here only when it would hold in any codebase.
