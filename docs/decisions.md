# Decisions log

Newest first. One entry per decision: date, decision, reason.

| Date | Decision | Reason |
| --- | --- | --- |
| 2026-11-12 | English only for the first release, with direction-aware (RTL-ready) layouts | Simplest launch; an RTL language can be added later without layout rework |
| 2026-11-12 | pnpm for `apps/admin` | Already assumed in the commands; used by Payload's docs and templates; fast, strict installs |
| 2026-11-12 | go_router for Flutter routing | Maintained by the Flutter team; one route table with redirects for auth state and deep links; no code generation |
| 2026-11-12 | Riverpod for Flutter state management | `AsyncValue` models loading, data and error states directly; easy to test with overrides; independent of the widget tree |
| 2026-11-12 | `main` protected on GitHub: PR required with 0 approvals, linear history, no force pushes or deletion, admins included | Enforces the git workflow on the server, not just by convention; 0 approvals because a solo maintainer cannot approve their own PR |
| 2026-11-12 | Public GitHub repo `academy-app` under the generic name "Academy App" | Branch protection on GitHub's free plan needs a public repo; a generic name keeps the business name out of public code |
| 2026-11-12 | Squash-merge PRs only; Conventional Commits; `type/short-description` branches | One clean commit per PR and a readable, linear history |
| 2026-11-12 | No AI attribution in commits, PRs or comments; enforced by settings and a commit-msg hook | Clean, professional history |
| 2026-11-12 | Start with two agents (implementer, reviewer) and four skills | Prove the loop first; add more only when needed |
| 2026-11-12 | Specs and plans are files in the repo | Agents work from files, not chat history, which keeps context small and work repeatable |
| 2026-11 | Flutter + Payload CMS + Supabase | Fits the feature set; backend stays portable |
| 2026-11 | Single theme config for all branding | Restyle the app without code changes |
| 2026-11 | Location modelled as data | A second location needs no code change |
