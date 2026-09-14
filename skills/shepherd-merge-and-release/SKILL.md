---
name: shepherd-merge-and-release
description: The standard agentic process for merging, post-merge validation, and release.
---

This is the post-merge process. Your goal is to make sure all steps after approval are completed successfully and report any issues.

## Required Invariants

- The branch you are in must have an associated PR
- The PR's CI must be passing
- The PR must be approved
- If it is part of the stack, these invariants must apply to the entire stack

Additionally, to complete this, you must have:

- The gh stack cli available
- Ability to connect with gh cli

If any of these invariants do not hold, stop immediately and report the error.

## Process

1. Merge the PR. If it is a stack, merge the stack with the gh stack cli.
2. Watch the CI on the main branch. If it fails, report the error.
3. If a release is possible/needed, do it.
4. Watch the CI for the release. If it fails, report the error.

## Output

You should report:

- If merged successfully
- Status of CI after merge
- If released, put a link to the release
- Status of the release attempt
- If any failures, provide a link to the failed run
- Describe any issues encountered
- Describe any required manual next steps

## Constraints

- You may not (likely don't) have permissions to release, that's OK. Go as far as you can.
- Never try to force a failing release. Take stock of the failure and carefully plan next steps.
- Never try to elevate your permissions. If permissions are block, assumed it is intentional and you aren't wanted to do that action.

