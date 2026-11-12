# Decisions log

Newest first. One entry per decision: date, decision, reason.

| Date | Decision | Reason |
| --- | --- | --- |
| 2026-11-12 | Squash-merge PRs only; Conventional Commits; `type/short-description` branches | One clean commit per PR and a readable, linear history |
| 2026-11-12 | No AI attribution in commits, PRs or comments; enforced by settings and a commit-msg hook | Clean, professional history |
| 2026-11-12 | Start with two agents (implementer, reviewer) and four skills | Prove the loop first; add more only when needed |
| 2026-11-12 | Specs and plans are files in the repo | Agents work from files, not chat history, which keeps context small and work repeatable |
| 2026-11 | Flutter + Payload CMS + Supabase | Fits the feature set; backend stays portable |
| 2026-11 | Single theme config for all branding | Restyle the app without code changes |
| 2026-11 | Location modelled as data | A second location needs no code change |
