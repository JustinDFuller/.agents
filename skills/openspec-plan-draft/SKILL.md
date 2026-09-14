---
name: openspec-plan-draft
description: The standard process for drafting an OpenSpec change.
---

This skill tells you how to propose and record an OpenSpec change.

## Required Invariants

Before beginning any work, verify these invariants. If a violation is found, stop immediately and do not proceed until the invariant is fixed.

1. You must be in a git repository.
2. You must not be on the main/default branch, but in a worktree.
3. You must be in a session that has run openspec-explore to work out how to implement something.

Additionally, you must have the following available:

- The openspec-propose skill.
- The gh cli.
- The gh cli "stack" extensions.

## Process

1. Use the openspec-propose skill to properly generate openspec files such as spec.md, design.md, and proposal.md.
2. Commit all the OpenSpec files for this change.
3. Push the commit to the remote branch.
4. Open a draft PR.
5. Make sure CI is green.
6. Make sure OpenSpec is valid.
7. Once done, mark the PR ready for review.
8. Print a link to the PR so I can go review it.

## Requirements

- Ensure the PR title follows repo requirements.
- Ensure the PR description follows pull_request_description.md if applicable.
- Ensure all the OpenSpec change files are checked in and available in the draft PR.
- Do not proceed to implementation. Stop and wait for me to review the change.
- The PR title starts with "Proposal". This does not override other required prefixes, such as "feat:" etc. But should be the first part of the title. Ex. "feat: Proposal for XYZ."

A user running this skill constitutes permission to follow this process. So long as the invariants are met, do not ask for clarification or permission - create the openspec change with openspec-propose, then commit, push and open a draft PR.

## Output

When you are done, you MUST output the following:

- Branch name
- Files created <spec, proposal, design>
- PR Link <link>

These should be printed clearly at the end of your output so the reviewer can quickly see what you did and click the link to review the PR. If you want to add any commentary above those required items, that is fine, but they must be above and not below, and must be concise.
