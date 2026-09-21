---
name: statamic-submission-readiness
description: Prepare or assess a Statamic add-on or starter kit for Marketplace submission using the official Statamic marketplace-review skill plus CodeProjects engineering evidence. Use for submission readiness, listing parity, distributable-artifact checks, or pre-submission review; do not use it as a substitute for implementation or ordinary code review.
---

# Statamic submission readiness

Use one evidence set to produce two distinct reports:

1. a complete internal readiness report supporting the CodeProjects decision to submit; and
2. a concise Statamic-facing readiness report following the tone and reporting rules in the official `marketplace-review` skill.

This skill adds internal release discipline. It does not modify, narrow, reinterpret, or claim equivalence to Statamic's official skill or public policy.

## Required sources

Before substantive work:

- Read `.agents/skills/marketplace-review/SKILL.md` completely.
- When browsing is available, read the current [Statamic Marketplace Submission Guidelines](https://statamic.com/marketplace/submission-guidelines) and record any difference from the vendored policy revision.
- Read `references/statamic-marketplace-review-source.md` to verify the vendored skill's upstream identity.
- When performing, commissioning, coordinating, summarizing, accepting, gating, or relying on a code review, read and follow the complete controlling Code Review Doctrine identified by the applicable `AGENTS.md`.

If the live policy and vendored skill differ materially, do not silently merge or reinterpret them. Record the difference, follow the current public policy for Marketplace readiness, preserve the upstream skill unchanged, and route a vendored-skill refresh as a separate exact change.

## Authority boundary

Installing or invoking this skill grants no authority to edit code, correct findings, install into a site, clear data, migrate customer content, commit, tag, push, publish, submit, contact Statamic, change a listing, deploy a demo, or exercise real external services.

Use only the execution authority expressly granted for the task. A Marketplace-readiness assessment does not grant marketplace approval or product, release, deployment, publication, or risk acceptance.

## Candidate and artifact identity

Identify the exact product before assessing readiness:

- repository, branch, commit, tree, staged and relevant untracked state;
- product type: Statamic add-on or starter kit;
- declared version and supported Statamic, Laravel, PHP, Node, and database versions where applicable;
- exact tagged or proposed release artifact, including member inventory, byte count, and SHA-256;
- installation, update, rollback, and uninstall instructions supplied to customers;
- demos, screenshots, listing copy, documentation, support route, licensing, pricing, and external-service requirements that make claims about that release.

The working checkout, a live demo, and the distributable artifact are different evidence surfaces. Do not let success in one stand in for another.

## Internal readiness work

Build the internal evidence needed for the applicable product rather than producing ceremony for its own sake.

### Engineering evidence

- Carry forward no code-review disposition to changed bytes without the Code Review Doctrine's required identity and impact handling.
- Trace authorization, validation, escaping, credentials, external requests, migrations, persistence, retry and failure behavior proportionate to the product.
- Verify that no secret, internal-only path, unpublished feature, hidden tracking, development residue, or unsupported claim enters the distributable artifact.

### Installation and lifecycle evidence

When authorized, test the exact customer artifact in isolated fresh sites using the documented procedure. Never use a clear-site operation or destructive migration against an existing site.

For supported configurations that materially differ, cover the relevant matrix rather than assuming equivalence. For DiscussionBridge's Statamic add-on, treat Flat, DB, and SSG as distinct exercised profiles even when they share add-on code. Verify as applicable:

- fresh installation and required asset/config publication;
- configuration with missing, valid, and invalid credentials;
- authoritative publishing hooks and duplicate-prevention behavior;
- Flat and database-backed persistence;
- SSG preparation, bounded queue draining, fail-closed build behavior, and static-output credential exclusion;
- update preservation for customer content, configuration, mappings, and operational state;
- rollback and uninstall boundaries, including what is deliberately retained;
- supported PHP, Laravel, Statamic, Node, database, and SSG combinations claimed by the release.

### Product and Marketplace evidence

Apply all applicable numbered rules from the official skill. Also reconcile:

- native Statamic extension points and Core/Pro edition boundaries;
- CP/editor workflows, permissions, labels, defaults, empty states, errors, keyboard use, focus, mobile layout, long content, and missing assets;
- redistribution rights and attribution for code, fonts, imagery, icons, fixtures, and demo content;
- README, installation/configuration guidance, changelog, compatibility claims, support route, screenshots, pricing, paid dependencies, listing copy, and live demo against the exact artifact;
- limitations and breaking changes appropriate to an Alpha, Beta, or experimental release.

Absence of proof is not automatically a violation. Mark uncertainty honestly and identify the smallest useful way to resolve it.

## Two-report contract

Both reports must derive from the same candidate and evidence ledger. They serve different readers and neither may contradict the other.

### Internal readiness report

Lead with whether the exact artifact is ready for Phil's submission decision. Include:

- candidate and artifact identity;
- included and excluded scope;
- evidence freshly observed, replayed, supplied, historical, inferred, unavailable, or not applicable;
- applicable-rule coverage sufficient to show what was actually assessed;
- grouped required corrections, uncertain concerns, and optional improvements;
- installation, upgrade, rollback, compatibility, security, licensing, documentation, demo, listing, and support evidence;
- every material limitation and remaining human decision;
- exact next gate and actions not authorized.

When this report includes or relies on code-review work, its disposition and supporting artifacts must follow the controlling Code Review Doctrine exactly. Marketplace readiness never upgrades an incomplete engineering review.

### Statamic-facing readiness report

Write the separate concise report using the official skill's `Creator-facing response` section. For a straightforward product, aim for roughly 200–400 words. Preserve:

- a specific, evidence-backed overall impression;
- the most important required changes or checks in plain language;
- genuinely useful finishing checks only;
- the exact reviewed release and material limits.

Do not expose internal control machinery, secrets, protected infrastructure, irrelevant chronology, or a rule-by-rule matrix. Do not soften, omit, or contradict an internal blocker. Do not send this report to Statamic unless Phil explicitly authorizes that communication.

## Completion boundary

Submission-ready means only that the exact artifact has sufficient engineering and Marketplace evidence for Phil to make the submission decision. It does not predict or guarantee Statamic approval.

If a material artifact, installation result, compatibility claim, licensing fact, live-policy check, documentation surface, demo, or listing claim remains unresolved, state the exact limitation. Do not turn uncertainty into a defect or present incomplete work as submission-ready.
