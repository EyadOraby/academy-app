---
name: payload-supabase
description: Conventions for the Payload CMS back-office and the Supabase Postgres database in apps/admin, covering collections, access control and migrations. Use when writing or reviewing backend or admin code.
---

# Payload and Supabase conventions

## Collections
- One file per collection in `apps/admin/src/collections`. Slugs are plural kebab-case.
- Every collection declares explicit `access` for create, read, update and delete. Never rely on defaults.
- Location is a collection. Anything that belongs to a place (classes, schedules, coaches) holds a relationship to it.
- Put validation in field `validate` functions and business rules in hooks, not in the mobile app alone.

## Access control
- Define roles once (for example admin, staff, coach, member) and reuse shared access helpers.
- Members can read and change only their own records. Test this for every collection that holds personal data.
- Anything that changes money, memberships or roles is admin or staff only.

## Database
- Schema changes go through Payload migrations committed to the repo. Never edit the production schema by hand.
- Run every migration against a staging project before production.
- Do not expose the Supabase service-role key to the mobile app or any client bundle.

## API use from mobile
- The mobile app talks to the Payload API. It does not query Postgres directly.
- Paginate every list endpoint. Never fetch unbounded lists.

## Environments
- Separate Supabase projects for development, staging and production.
- All keys and URLs come from git-ignored environment files, with a committed `.env.example` listing names only.

## Code
- TypeScript strict mode. No `any` without a comment explaining why.
- Run lint, type check and tests before every commit.
