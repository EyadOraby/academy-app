---
name: flutter-conventions
description: Flutter and Dart conventions for apps/mobile, covering structure, theming, state, errors and tests. Use when writing or reviewing Flutter code.
---

# Flutter conventions

## Structure
Feature-first folders under `apps/mobile/lib`:
```
core/        theme, routing, networking, shared widgets, utilities
features/<name>/data          API clients, models, repositories
features/<name>/domain        entities and business rules (when needed)
features/<name>/presentation  screens, widgets, state
```
A feature never imports another feature's `data` or `presentation` folder. Share through `core/`.

## Theming
- One theme config in `core/theme` defines colours, typography, spacing, radii and the logo.
- Widgets read from `Theme.of(context)` or the theme extensions. No hex colours, font names or magic spacing numbers in widgets.
- Swapping the config must restyle the whole app with no other code change.

## State and logic
- Use the state management package recorded in `CLAUDE.md`. Do not introduce a second one.
- Keep widgets free of business logic and network calls.
- Model loading, success, empty and error states explicitly for every screen that loads data.

## Code
- `const` constructors wherever possible. Small widgets over long build methods.
- No `print`; use the project logger. No `dynamic` unless unavoidable. No ignored lints without a comment explaining why.
- All user-facing text goes through localisation, never inline strings.
- Handle errors at the repository boundary and return typed failures.

## Tests
- Unit tests for repositories and business rules.
- Widget tests for each screen's main states.
- Run `flutter analyze` and `flutter test` before every commit.
