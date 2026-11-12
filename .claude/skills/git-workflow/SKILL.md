---
name: git-workflow
description: Branch naming, commit message format, pull request and merge rules for this repo. Use before creating a branch, committing, opening a PR or merging.
---

# Git workflow

## Branches
- `main` is protected. Never commit or push to it directly.
- Branch from an up-to-date `main`: `type/short-description`, lowercase kebab-case.
- Types: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `ci`.
- Examples: `feat/class-booking`, `fix/login-token-refresh`, `chore/ci-setup`.
- One feature or fix per branch. Delete the branch after merge.

## Commits
Format: `type(scope): summary`
- Summary: imperative, lowercase, no full stop, 72 characters or fewer.
- Scope: the area touched, such as `booking`, `auth`, `theme`, `admin`, `ci`.
- One logical change per commit. Add a body only when the reason is not obvious; wrap it at 72 characters and explain why, not what.
- Examples:
  - `feat(booking): add class schedule screen`
  - `fix(auth): refresh token before it expires`
  - `chore(ci): run flutter analyze on pull requests`

## No AI attribution
Never add `Co-Authored-By`, `Generated with`, tool names, emojis or any mention of Claude or AI to a commit message, PR title, PR body or code comment. The `commit-msg` hook rejects such commits. If attribution appears anyway, amend the commit before pushing.

## Pull requests
- Title uses the commit format, because it becomes the squash commit on `main`.
- Fill in the PR template: what changed, how it was tested, the checklist.
- Keep PRs small: one spec task or one tightly related group.
- All checks must pass before merge.

## Merging
- Squash merge only, so `main` has one clean commit per PR and a linear history.
- Rebase the branch on `main` to resolve conflicts. Do not merge `main` into the branch.
- Never force-push to `main`. Force-push to your own branch only after a rebase.

## First-time setup per clone
`git config core.hooksPath .githooks`
