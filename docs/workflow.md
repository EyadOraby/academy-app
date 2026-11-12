# Workflow

Every feature follows the same steps. Each step produces a file the next one reads, so no step depends on chat history.

| Step | Who | Output |
| --- | --- | --- |
| 1. Spec | Eyad, planned in Claude chat | `specs/NNN-name.md` |
| 2. Plan | Claude Code (plan mode) | `plans/NNN-name.md` |
| 3. Approve | Eyad | Plan marked approved |
| 4. Implement | `implementer` agent, one task per session | Commits on a feature branch |
| 5. Test | `implementer` runs the suite; CI repeats it | Passing checks |
| 6. Review | `reviewer` agent | `PASS` or `CHANGES REQUIRED` |
| 7. Merge | Eyad | Squash-merged PR |

## Rules
- A failure at step 5 or 6 returns to step 4 with the failure output attached.
- Two failed rounds on the same task mean the spec or plan is wrong. Go back to step 1 or 2 instead of retrying.
- Auth, payments, access rules and personal data are read by Eyad before merge.

## Keeping it efficient
- One task per session; start fresh for the next task.
- Give an agent the task, the files it names and the relevant skill, not the whole repo.
- Ask for diffs and short reports, not full rewrites or long explanations.
- Keep `CLAUDE.md` short. Put detail in skills, which load only when needed.

## Growing the workflow
Start with two agents and four skills. Add a planner or tester agent, or a new skill, only when a repeated problem shows the need. Record the reason in `docs/decisions.md`.
