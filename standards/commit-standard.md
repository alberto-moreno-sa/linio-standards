# Linio Commit Standards
There are many ways to handle committing. This document's purpose is to narrowly define how they are handled at Linio.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## Commit Contents
A commit SHOULD be a specific set of related changes. Commits MUST be able to be reverted without causing other problems.

## Messages
A commit message MUST be in the past tense, and in the form of a complete sentence (including punctuation). If you need to include more information, you MUST use a secondary message, also known as the "body". While there is no limit to the title message (first), you MUST not go beyond a single sentence, and it SHOULD follow proper English grammar.

An example is `Removed deprecated actions in SomeController.`

The reason for this is the commit history MUST be usable, but does not REQUIRED to be used, as a changelog. Messages such as `Merge`, `Updated SomeClass.`, etc., do not describe what was changed.

### Issue Prefix
If the project you are working on is using a project management software (e.g. Jira), the commits MAY be prefixed with the issue related to it. An example is `[PROJ-1234] Added cart items to customer session.`. It is up to your project lead to determine if this prefix MUST be used or not.

## When to Commit?
### Frequency
You SHOULD be committing frequently. This does not mean you need to commit every 5 minutes. Simply think of it as a way to save completed code. If you don't commit it, it cannot be reverted if you break something.

### End of Day
You MUST commit and push all of your changes before you leave for the end of the day. If something happens to your laptop or you, the company should not lose access to any changes that were in progress. If you have a work in progress commit, you MUST prefix your commit message with `[WIP]`. An example is `[WIP] Added delete action to UserController.`.

## Can it be merged?
A branch SHOULD NOT be merged unless all tests pass. If a test fails, but falls out of the scope of the branch, it should be discussed with the team lead as to whether or not to fix it inside the current branch.

## How do I merge?
You SHOULD submit a pull request if you are at the stage where your code is completed, you have reviewed it yourself, and all tests pass. If you do need to have an open discussion about something in progress, you MUST prefix the pull request with `[WIP]`.

You MUST put the issue prefix in the pull request title though (e.g. `[PROJ-1234] Added cart items to customer session.`)

## Prefix Reference
- [WIP] - Work in Progress (e.g. `[WIP] Added delete action to UserController.`)
- [ISSUE] - Issue related to the commit (e.g. `[PROJ-1234] Added cart items to customer session.`)
