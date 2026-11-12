# Academy App — project rules

Read this file at the start of every session. Keep it short; detail lives in `docs/` and in skills.

## What this is
A martial arts academy app: a Flutter mobile app for members and a Payload CMS back-office for staff, on Supabase Postgres.

## Stack
- Mobile: Flutter (Dart), in `apps/mobile`, with Riverpod for state management and go_router for routing
- Back-office and API: Payload CMS on Next.js (TypeScript), in `apps/admin`, using pnpm
- Database and storage: Supabase (Postgres)
- CI: GitHub Actions

## Repo layout
```
apps/mobile      Flutter app
apps/admin       Payload CMS + Next.js
docs/            Brief, workflow, decisions
specs/           One spec per feature (source of truth for what to build)
plans/           One task plan per spec
.claude/         Agents, skills, settings
```

## Design constraints (always apply)
- Theming: every colour, font and logo comes from one theme config. No hard-coded colours or fonts in widgets.
- Locations: the academy has one location today. Model location as data, so a second one is a new record, not a code change.
- Languages: English only for the first release, but RTL-ready. Build every layout direction-aware (start/end, never left/right), so adding an RTL language needs no layout rework.
- Scope: build only what the current spec says. No extra features.

## How work is done
Follow `docs/workflow.md`: spec, plan, approval, implement, test, review, merge.
- Never start coding without an approved plan in `plans/`.
- One task per session. Touch only the files the task names.
- Never edit a test just to make it pass.
- No new dependency without Eyad's approval.

## Git (non-negotiable, full rules in the git-workflow skill)
- Never commit to `main`. Work on `type/short-description` branches and merge by squash PR.
- Commit messages follow Conventional Commits: `type(scope): summary`.
- Never add AI attribution of any kind to commits, PR titles, PR bodies or code comments. No "Co-Authored-By", no "Generated with", no mention of Claude or any AI tool.

## Security (full rules in the security-rules skill)
- Auth, payments, access rules and members' personal data are reviewed by Eyad personally before merge. Flag these PRs clearly.
- No secrets in the repo. Use environment files that are git-ignored.

## Commands
Fill in once the apps are scaffolded:
- Mobile: `flutter analyze`, `flutter test`
- Admin: `pnpm lint`, `pnpm typecheck`, `pnpm test`
