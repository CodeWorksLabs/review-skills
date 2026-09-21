---
name: codeworkslabs-platform-review
description: Review a software product or release using CodeWorksLabs evidence discipline plus the applicable platform-specific guidance. Use for internal readiness, platform submission, public technical review, or release assessment; do not use it to infer mutation, publication, submission, deployment, or acceptance authority.
---

# CodeWorksLabs platform review

Review the exact product and candidate against shared CodeWorksLabs requirements and the selected platform guidance. Evaluate software behavior and evidence, not whether a human or coding agent typed particular lines.

## Select the platform source

Identify the product's platform before substantive review and load only the applicable platform material:

- Discourse plugin, theme, theme component, or integration: read [references/platforms/discourse/DiscourseSkill.md](references/platforms/discourse/DiscourseSkill.md).
- Statamic add-on or starter kit: read the complete official [references/platforms/statamic/marketplace-review/SKILL.md](references/platforms/statamic/marketplace-review/SKILL.md), then read [references/platforms/statamic/UPSTREAM-PROVENANCE.md](references/platforms/statamic/UPSTREAM-PROVENANCE.md). When internet access is available, compare the live Statamic policy and skill to the recorded upstream identity.
- A product spanning multiple platforms: load every materially applicable platform source and distinguish each platform's evidence.
- A platform without maintained guidance: apply this wrapper, identify the missing platform-specific coverage, and do not invent an official platform policy.

The platform source adds specialized analysis. It never narrows an applicable controlling organizational doctrine or the user's exact review instruction.

## Authority

Review authority is read-only unless the user expressly authorizes a bounded execution profile. Reviewing, finding a defect, possessing mutation-capable tools, or being asked to continue does not authorize edits, commits, pushes, installations, deployments, submissions, provider actions, messages, or acceptance.

Before mutation or external execution, confirm that the exact actor, action class, and target are within authority. Stop on ambiguity that would materially change external or user-owned state.

## Identify the candidate

Record, as applicable:

- repository and product type;
- branch, commit, tree, tag, declared version, dirty state, staged state, and relevant untracked files;
- exact archive or package inventory, byte count, and SHA-256;
- active consumer, installed runtime, generated artifact, demo, documentation, listing, and release identities;
- claimed platform, framework, runtime, database, browser, and dependency support;
- included scope, excluded scope, freeze state, queued changes, and replacement or supersession history.

The working checkout, tagged artifact, installed product, generated output, and public demo are separate evidence surfaces. Success in one does not establish another.

## Declare the review mode

Use the review type and execution profile required by the applicable controlling doctrine or request. At minimum, distinguish:

- static inspection;
- repository verification using local automated checks;
- installed or integrated verification;
- exact release-artifact readiness;
- focused correction closure or specialist scope.

Do not imply that a lower-evidence mode established a higher-evidence conclusion. A focused result is not a complete product or release review.

## Evidence discipline

For every material claim, distinguish independently observed, independently replayed, supplied but not replayed, historical, inferred, unavailable, and not applicable evidence. Record the source, executing actor when known, time, candidate association, command or procedure, and relevant output identity.

Use the repository's own supported checks first. A workflow file, test count, manifest, clean status, persuasive report, or successful build does not substitute for inspecting the behavior it claims to cover. Missing evidence is not automatically a defect, but it limits the conclusion.

Reconcile contradictory evidence by exact candidate, date, environment, and behavioral scope. Newer narration does not silently supersede older evidence. A changed candidate requires explicit impact analysis and fresh evidence where affected.

## Shared review coverage

Apply proportionately to the product:

- supported extension points and native platform behavior;
- authorization, validation, output encoding, privacy, credentials, and external requests;
- persistence, migrations, identity, concurrency, idempotency, retries, failure, recovery, and rollback;
- dependencies, supply chain, generated and packaged artifacts, active consumers, and installation;
- administration, editor and user experience, accessibility, responsive behavior, empty/error states, and truthful operator feedback;
- compatibility, update, disablement, removal, retained data, documentation, support, licensing, distribution rights, demos, listings, and release claims;
- behavior across supported editions, storage modes, themes, runtimes, and platform versions when they materially differ.

Inspect realistic unhappy paths and boundaries rather than only the demo path. Do not demand complexity, unrelated features, fashionable styling, universal compatibility, or exhaustive proof that the product does not claim.

## AI-assistance transparency

Disclose AI or coding-agent assistance when the product owner or publication venue requires it or when CodeWorksLabs chooses to do so publicly. Do not infer authorship from style, use authorship as a quality score, or label a defect as AI-caused without direct evidence.

Human responsibility remains explicit: the candidate owner is accountable for reviewing, testing, representing, maintaining, and supporting the shipped product. Automated review is evidence, not approval or a replacement for accountable acceptance.

## Reporting

Produce two reports when platform submission or public publication is in scope:

1. an internal report sufficient for the authorized CodeWorksLabs decision, following every applicable controlling review doctrine; and
2. a concise platform- or creator-facing report using the selected platform's required tone and content.

Both reports must derive from the same candidate and evidence ledger and must not contradict each other. Keep required corrections, unresolved verification, and optional improvements distinct. Do not expose internal control machinery, secrets, protected infrastructure, or irrelevant chronology in the external report.

A report must identify its candidate, scope, evidence level, material limitations, findings, and next gate. Do not claim platform approval, comprehensive security certification, legal clearance, guaranteed compatibility, release acceptance, deployment acceptance, or product-risk acceptance.

## Public reports and sensitive findings

Public is the default for reusable methods and non-sensitive completed reports. Keep unresolved exploit details, credentials, private client information, protected infrastructure, and coordinated-disclosure evidence private. A sanitized public report may follow correction or coordinated disclosure.

Historical drafts and design inputs must be labeled non-controlling. Never present an exploratory assessment as a current disposition.
