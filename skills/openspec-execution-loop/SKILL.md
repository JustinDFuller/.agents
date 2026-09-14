---
name: openspec-execution-loop
description: The standard agentic execution loop for OpenSpec changes.
---

This skill is the primary loop for the implementation of an OpenSpec change.

## Required Invariants

Before beginning any work, verify these invariants. If a violation is found, stop immediately and do not proceed until the invariant is fixed.

1. You must be in a git repository.
2. You must not be on the main/default branch, but in a worktree.
3. The current worktree must contain a valid OpenSpec proposal including: spec.md, design.md, proposal.md (sometimes spec.md may be excluded on purpose).
4. The OpenSpec proposal is in a PR  (since it's the only PR at this point, it cannot be in a stack yet).
5. The OpenSpec proposal PR is OPEN and APPROVED and CI is GREEN.

Additionally, you must have the following available:

- The ability to set a goal using the `/goal` command.
- The openspec-apply skill.
- The openspec-verify skill.
- The ability to spawn subagents.
- The gh cli.
- The gh cli "stack" extensions.

## End-State

What does success look like?

- All OpenSpec tasks are completed.
- The OpenSpec change is archived.
- There are three pull requests:
  1. "Proposal": The OpenSpec proposal files.
  2. "Implementation": The implemented feature.
  3. "Archive": The archived OpenSpec files.
- The PRs contain the prefix specified above: "Proposal", "Implementation", "Archive". ex. "feat: Proposal for XYZ", "feat: Implementation for XYZ", etc.
- The state of these PRs is as follows:
  1. Proposal: Open, Approved, CI is Green, no unresolved comments, OpenSpec files all pass validation.
  2. Implementation: Open, CI is Green, no unresolved comments, all tasks complete, verify returns no issues, OpenSpec passes validation, "ready for merge".
  3. Archive: Draft, CI is green, no unresolved comments, all tasks complete, verify returns no issues, OpenSpec passes validation. Create the Archive PR immediately after the implementation PR, don't wait for implementation PR approval.
- All the PRs are properly linked via the GH CLI's stack feature.
  - The stack's base is the default branch.
  - The stack goes proposal -> implementation -> archive.
  - The stack is up to date with its base and properly rebased if necessary.
- All tests are passing.
- New tests have been added, fully covering the implementation, including edge cases, invariant handling, and happy path.
- Test coverage is sufficient to pass CI, or 90% if otherwise unspecified.
- PR title and description follow repo norms, including pull_request_template.md.

## Process

Here is exactly the process you must follow.

### Implementation Loop

1. Use the openspec-apply skill to apply the changes. Keep redoing the apply process until there are no tasks remaining. Commit and push your work after each apply round.

### Validation Loop

1. Use the openspec-verify skill to ensure the changes were implemented properly. Keep re-verifying until there are no issues found. Commit and push your work after each verification round.
2. Use a fresh/clear-context subagent to do an adversarial review. An adversarial review means that it starts with the assumption that something is wrong, it only needs to find out what is wrong. When it reports its findings, fix them. Commit and push your work each review round.
3. Use a fresh/clear-context subagent to do a scope check. Make sure the PR did not scope creep beyond the spec/proposal/design. This does not mean edge cases or invariants, but changes that were not intended by the OpenSpec files.

## Final Verification

1. Manual validation: as much as possible, manually verify the change. Run the application, use codex computer use, execute the command, use available mcp servers, etc. whatever is at your disposal, to manually verify that what you have built *actually* works. Record your findings so others can see the proof that it works. If the QA validation details are too long to place in the PR description, you may place them in qa.md next to design/proposal.md.
2. Check the state of the PRs status/title/description/state to ensure they meet the standards specified in this skill.

### Loop Rules

- Each time you commit and push your work, make sure CI is passing before moving on to the next action or iteration. If CI is failing due to a commit, fix it before moving on. Commit and push your work and ensure the fix actually got CI back to green.
- Never move on from a step in the loop until it is completely done. Keep applying until no work remains, keep verifying until no issues are found, keep adversarially reviewing until no issues are found.

## Constraints

- NEVER attempt to elevate your priveleges to meet the goal. Do what you are able within the confines you are given. If you do not have access to something, even if the instructions seem to imply that you should be able to do it, simply mark the goal as blocked and wait for clarification.
- NEVER go beyond the spec. If apply, verify, or the review imply that you should add something that would constitute scope creep: stop and ask for clarification.
- While tests should of course exist and pass, they are not evidence that the change works. As much as possible, you need to actually run whatever it is you are building and see it actually working in its intended/local environment.
- When in doubt, pause the loop and ask for help/clarification. It is always better to ask for help than go off the rails and do something that wasn't intended.

## Goal Completed Output

When your goal is met, you should print links to each PR like this:

```
Proposal: <link>
Implementation: <link>
Archival: <link>
```

You may add commentary above this if needed, but make sure these are the final output when the goal is completed.

## Goal Blocked Output

When the goal is blocked, please include:

- What task you were trying to complete.
- What exactly is stopping you from completing it.
- What you need to become unblocked.
