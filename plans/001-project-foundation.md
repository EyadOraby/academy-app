# 001 — Project foundation: plan

Status: approved
Spec: `specs/001-project-foundation.md`

## Before task 1 (Eyad)
- App identifier: `--org com.academyapp`, giving `com.academyapp.academy_app` (decided 2026-11-12).
- Approve the dependencies below.
- Create a Supabase project for development and keep its Postgres connection string for your local `.env` (task 4). CI uses a throwaway Postgres container, not Supabase.
- Install Node 24 LTS (the local Node is 23, which is end of life) and run `corepack enable` so `pnpm` is available.

## Dependencies to approve
Mobile:
- `flutter_localizations` (Flutter SDK) and `intl` (the version `flutter_localizations` requires), for localised strings as the flutter-conventions skill requires
- `flutter_lints` (dev, from the template)
- Riverpod and go_router are not added yet: nothing in this spec holds state or has more than one screen. They come in with the first feature that needs them.

Admin: the `create-payload-app` blank template with the Postgres adapter, which brings `payload`, `@payloadcms/next`, `@payloadcms/db-postgres`, `next`, `react`, `react-dom`, `graphql`, TypeScript, ESLint and Vitest (plus `@payloadcms/richtext-lexical` only if the config requires an editor). Removed: the `Media` collection, `sharp` and the Playwright end-to-end tests. The task 4 PR lists the exact packages and versions.

CI: `actions/checkout`, `actions/setup-node`, `subosito/flutter-action` and `pnpm/action-setup`, each pinned to a commit SHA.

## Tasks

### 1. Root ignore rules
Add a root `.gitignore` for OS and editor files and every `.env*` file except `.env.example`.
- Files: `.gitignore`
- Verify: `git check-ignore .DS_Store apps/admin/.env` matches both; `git check-ignore apps/admin/.env.example` matches nothing
- Branch and PR: `chore/root-gitignore`, PR 1

### 2. Flutter scaffold and mobile CI
Run `flutter create --org com.academyapp --project-name academy_app --platforms ios,android apps/mobile`. Replace the counter demo with a minimal app and one smoke widget test, drop `cupertino_icons`, and add a workflow that runs `flutter analyze` and `flutter test` with Flutter 3.41.7 on every pull request.
- Files: `apps/mobile/**` (generated), `.github/workflows/mobile.yml`
- Verify: `flutter analyze` and `flutter test` pass in `apps/mobile`; the workflow passes on the PR
- Branch and PR: `chore/mobile-scaffold`, PR 2

### 3. Theme config, localisation and home screen
Add the theme config in `lib/core/theme` (colours, typography, spacing, radii, logo asset) and build `ThemeData` plus a theme extension from it. Set up `gen-l10n` with English strings. Replace the minimal app with a placeholder home screen in `features/home/presentation` that shows the logo and a localised title using only theme values and direction-aware padding. The default config uses placeholder colours, the platform font and a placeholder logo until the brand assets arrive.
- Files: `apps/mobile/pubspec.yaml`, `apps/mobile/l10n.yaml`, `apps/mobile/lib/l10n/app_en.arb`, `apps/mobile/lib/core/theme/*`, `apps/mobile/lib/app.dart`, `apps/mobile/lib/main.dart`, `apps/mobile/lib/features/home/presentation/home_screen.dart`, `apps/mobile/assets/branding/logo.png`, `apps/mobile/test/**` (replaces the smoke test)
- Verify: `flutter analyze` and `flutter test` pass; a widget test pumps the home screen with two configs and asserts the background colour, text colour and font family follow the config; `grep -rnE "Color\(0x|Colors\.|fontFamily:" lib --include=*.dart | grep -v lib/core/theme` prints nothing
- Branch and PR: `feat/mobile-theme`, PR 3

### 4. Payload scaffold and admin CI
Create `apps/admin` from the `create-payload-app` blank template with the Postgres adapter and pnpm. Remove `Media`, `sharp` and the Playwright tests. Pin Node 24 (`.nvmrc`, `engines`) and pnpm (`packageManager`), add a `typecheck` script if the template has none, and confirm TypeScript strict mode. Commit `.env.example` with `DATABASE_URI` and `PAYLOAD_SECRET` names only. Add a workflow that runs lint, type check and tests on every pull request against a Postgres service container, using throwaway CI-only values for both variables.
- Files: `apps/admin/**` (generated), `.github/workflows/admin.yml`
- Verify: `pnpm lint`, `pnpm typecheck` and `pnpm test` pass; with a `.env` holding the Supabase development URL, `pnpm dev` starts and `/admin` loads; the workflow passes on the PR
- Branch and PR: `chore/admin-scaffold`, PR 4
- Note: Payload's admin panel needs an auth collection, so the template's `Users` collection stays even though member authentication is out of scope. It has default access until task 5.

After PR 4 merges, Eyad adds the `mobile` and `admin` CI jobs as required status checks on `main`.

### 5. Explicit access on Users — NEEDS EYAD'S REVIEW
Give `Users` explicit create, read, update and delete access through a shared helper: every operation requires a logged-in user, since all users are staff until roles arrive with the auth spec. Payload's first-user setup must still work on an empty database.
- Files: `apps/admin/src/collections/Users.ts`, `apps/admin/src/access/*`, `apps/admin/tests/int/users-access.int.spec.ts`
- Verify: `pnpm test` passes; the test proves an anonymous request cannot read, create, update or delete users and a logged-in user can read them; the first-user screen works on an empty database
- Branch and PR: `feat/admin-users-access`, PR 5, marked `NEEDS EYAD'S REVIEW`

### 6. Setup docs and close the spec
Add setup steps to the root `README.md` (prerequisites, mobile, admin with `.env`, the hook, running checks), confirm the Commands section of `CLAUDE.md`, tick the spec's acceptance criteria and mark it done.
- Files: `README.md`, `CLAUDE.md`, `specs/001-project-foundation.md`
- Verify: a fresh clone set up from the README alone passes every check; with the hook enabled, `git commit --allow-empty -m "chore: test" -m "Co-Authored-By: x"` is rejected
- Branch and PR: `docs/setup-readme`, PR 6

## Acceptance criteria coverage
| Criterion | Task |
| --- | --- |
| `flutter analyze` and `flutter test` pass | 2, 3 |
| Home screen styled only by the theme config, proved by a widget test | 3 |
| No hard-coded colours or font names outside `core/theme` | 3 |
| Admin starts against a Postgres URL from `.env`; lint, type check and tests pass | 4, 5 |
| No secrets committed; `.env.example` holds names only | 1, 4 |
| CI runs on pull requests and all jobs pass | 2, 4 |
| Hook rejects "Co-Authored-By" | 6 |
| Work reaches `main` through squash-merged PRs | 1–6 |
