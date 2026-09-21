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
- `.agents/skills/codeworkslabs-platform-review/references/platforms/` — platform-specific guidance selected by the wrapper.
- `sources/` — preserved non-controlling source and design material used to develop the maintained guidance.
- `published-reviews/` — public review examples or reports, each with an explicit status and candidate identity.

The vendored Statamic skill remains unchanged from its official source. CodeWorksLabs additions live outside that file.

## Public-by-default boundary

Review methods and ordinary product reports should be public. Do not publish credentials, protected infrastructure details, private client material, unpublished proprietary source, active exploit instructions, or coordinated-disclosure material. Publish a sanitized report after the sensitive condition is corrected or disclosure is coordinated.

## Status

The initial Discourse material is under active development. Historical source artifacts are preserved for traceability but are not controlling instructions. A product review is valid only under the exact authority, candidate identity, scope, evidence, and disposition requirements applicable to that review.
