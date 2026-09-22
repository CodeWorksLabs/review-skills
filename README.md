# CodeWorksLabs Review Skills

Public, evidence-based review guidance for software built with or without coding agents.

This repository contains one CodeWorksLabs review wrapper and platform-specific review sources. The wrapper supplies the shared identity, evidence, authority, execution, and reporting discipline. It loads only the platform guidance relevant to the product under review.

```text
CodeWorksLabs wrapper
├── Discourse platform guidance
├── Statamic's official marketplace-review skill
└── future platform guidance
```

Authorship method is not a proxy for software quality. Reviews evaluate the exact product, artifact, behavior, evidence, and lifecycle. AI assistance may be disclosed honestly without treating it as either proof of quality or proof of deficiency.

## Repository layout

- `.agents/skills/codeworkslabs-platform-review/SKILL.md` — the single reusable wrapper.
- `.agents/skills/codeworkslabs-platform-review/references/platforms/` — complete platform-specific working skills and structured review cores selected by the wrapper.
- `sources/` — preserved non-controlling source and design material used to develop the maintained guidance.
- `published-reviews/` — public review examples or reports, each with an explicit status and candidate identity.
- `CONTRIBUTING.md` — the public contribution and platform-authority boundary.

The Discourse package contains the complete working Markdown skill and its canonical versioned `DiscourseSkill.json` core. The vendored Statamic skill remains unchanged from its official source. CodeWorksLabs additions live outside that file.

## Versioning

The Discourse package separates JSON schema evolution from review-policy evolution:

- `format_version` identifies the machine-readable schema;
- `ruleset_version` identifies substantive review guidance;
- Git tags use `discourse-skill-vMAJOR.MINOR.PATCH`;
- `DiscourseSkill.json` and `DiscourseSkill.md` are stable current paths;
- immutable tags and commits identify historical releases.

Changes to one active representation must reconcile the other and refresh the recorded identities in `PROVENANCE.md`. The originating artifacts under `sources/` remain unchanged.

## Public-by-default boundary

Review methods and ordinary product reports should be public. Do not publish credentials, protected infrastructure details, private client material, unpublished proprietary source, active exploit instructions, or coordinated-disclosure material. Publish a sanitized report after the sensitive condition is corrected or disclosure is coordinated.

## Status

The Discourse core is active CodeWorksLabs-maintained public guidance and is intended to improve through internal use and open community scrutiny. Historical source artifacts remain preserved for traceability but are not separate controlling instructions. A product review is valid only under the exact authority, candidate identity, scope, evidence, and disposition requirements applicable to that review.
