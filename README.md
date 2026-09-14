# Agent Skills

Reusable Codex skills for planning, implementing, and shipping OpenSpec changes.

## Skills

| Skill | Purpose |
| --- | --- |
| [`openspec-plan-draft`](skills/openspec-plan-draft/SKILL.md) | Create and publish an OpenSpec proposal for review, then stop before implementation. |
| [`openspec-execution-loop`](skills/openspec-execution-loop/SKILL.md) | Apply, validate, review, and archive an approved OpenSpec change. |
| [`shepherd-merge-and-release`](skills/shepherd-merge-and-release/SKILL.md) | Merge an approved change, verify post-merge CI, and complete its release when applicable. |

Each skill is defined by the `SKILL.md` file in its directory. Use a skill when its name matches the task, and follow its required invariants before starting.
