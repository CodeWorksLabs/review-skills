# Changelog

## discourse-skill-v0.1.2 — 2026-09-22

- Split the candidate file census into shared, plugin, theme, and theme-component inventories.
- Corrected theme JavaScript discovery to the documented root `javascripts/` tree rather than plugin-style `assets/javascripts/` or `javascripts/discourse/` assumptions.
- Added the documented theme/component roots: `about.json`, root `settings.yml`, `locales/`, `common/`, `desktop/`, `mobile/`, `stylesheets/`, and `assets/`.
- Added full-theme checklist routing and required hybrid candidates to receive every applicable inventory.
- Clarified that optional directories are discovery prompts, while misplaced, unreachable, untracked, ignored, packaged, installed, and generated files require explicit reconciliation.

## discourse-skill-v0.1.1 — 2026-09-21

- Added a five-slot local Discourse matrix plan for `main`, current monthly, previous supported monthly, maintained ESR, and lifecycle verification.
- Required independent mutable state per slot while permitting shared immutable images, dependency caches, and Git objects.
- Defined serialized operation, immutable candidate handling, a matrix manifest, deterministic controls, and a separate lifecycle sequence.

## discourse-skill-v0.1.0 — 2026-09-21

- Established `DiscourseSkill.json` as the canonical structured Discourse review core.
- Established the complete `DiscourseSkill.md` as its human-readable working companion.
- Added ruleset and schema version separation.
- Added an isolated installation or container for every claimed materially distinct Discourse release line.
- Recorded the September 2026 example matrix: `main`, 2026.9, 2026.8, and claimed maintained 2026.7 ESR targets.
- Preserved the originating Markdown, structured JSON, design report, and review examples unchanged under `sources/` and `published-reviews/`.
