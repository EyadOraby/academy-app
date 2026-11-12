# 001 — Project foundation

Status: draft

## Goal
A clean, working skeleton for both apps with theming, checks and CI in place, so every later feature starts from a reliable base. This spec also proves the workflow end to end.

## In scope
- Flutter app scaffold in `apps/mobile` with the folder structure from the flutter-conventions skill
- Theme config in `core/theme` (colours, typography, spacing, logo) and one placeholder home screen that uses it
- Payload CMS + Next.js scaffold in `apps/admin`, connecting to Postgres through environment variables
- `.gitignore`, `.env.example` files, and a root `README.md` with setup steps
- GitHub Actions: analyse and test the mobile app; lint, type-check and test the admin app, on every pull request
- `commit-msg` hook enabled and documented in the README

## Out of scope
- Any real feature, screen or collection beyond what the scaffolds need
- Authentication
- Deployment

## Acceptance criteria
- [ ] `flutter analyze` and `flutter test` pass in `apps/mobile`
- [ ] The home screen takes all colours and fonts from the theme config; a widget test proves a different config changes them
- [ ] No hard-coded colours or font names exist outside `core/theme`
- [ ] `apps/admin` starts locally against a Postgres URL from `.env`, and lint, type check and tests pass
- [ ] No secrets are committed; `.env.example` lists variable names only
- [ ] CI runs on a pull request and all jobs pass
- [ ] A commit containing "Co-Authored-By" is rejected by the hook
- [ ] The work reaches `main` through squash-merged PRs with Conventional Commit titles

## Notes
Resolve the open decisions in `CLAUDE.md` with Eyad before planning: state management, routing, package manager, languages.
