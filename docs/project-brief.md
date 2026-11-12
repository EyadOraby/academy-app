# Project brief

## Product
A mobile app for a martial arts academy's members, with a back-office for staff to manage the academy.

## Technical decisions
- Flutter mobile app; Payload CMS (Next.js) back-office; Supabase Postgres.
- Hosting is kept portable so the backend can move to another provider later.
- Single location today, modelled as data so more can be added from the back-office.
- All branding comes from one theme config: colours, fonts and logo.

## Delivery phases
- Phase 1, Core App: the core member and staff features, including merchandise.
- Phase 2, Payments and Extras: card payments and the additional features.
- Optional extras: a website and an online shop.

The feature list for each phase lives in the specs. Add a spec before building anything.

## Sources of truth
- What to build: `specs/`
- How it is built: `CLAUDE.md`, `docs/workflow.md`, the skills in `.claude/skills/`
- Why a choice was made: `docs/decisions.md`
