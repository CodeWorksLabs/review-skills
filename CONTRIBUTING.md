# Contributing

Contributions that make the review cores more accurate, usable, evidence-based, and faithful to their platforms are welcome.

## Platform authority

CodeWorksLabs maintains this repository. Its Discourse guidance is a public community-review project, not official Discourse, CDCK, Marketplace, or Meta policy. Do not describe a proposed or merged rule as an official platform requirement unless an authoritative platform source establishes that claim.

Official third-party skills, such as Statamic's vendored Marketplace review skill, must remain byte-for-byte unchanged. Propose CodeWorksLabs additions in the outer wrapper or an adjacent maintained platform file.

## Proposing a change

For a platform-rule change, explain:

- the exact requirement being added, corrected, narrowed, or removed;
- the product types and review modes affected;
- the authoritative documentation, source behavior, reproducible defect, or review evidence supporting it;
- whether the change is a platform requirement, a CodeWorksLabs policy, or an optional review technique;
- the effect on existing reports and compatibility claims.

Avoid turning one product's architecture, one historical failure, stylistic preference, or speculative threat into a universal platform rule.

## Discourse core synchronization

The active Discourse package contains a human-readable Markdown skill and a structured JSON core. Treat them as one maintained contract.

A pull request changing either must:

1. identify the affected rule, workflow, profile, evidence threshold, or report field;
2. update the counterpart when behavior changes;
3. preserve unchanged original requirements or state their intentional supersession;
4. refresh provenance identities when source bytes change;
5. validate the outer skill and show that no active requirement disappeared unintentionally.

Formatting-only changes should not rewrite the preserved copies under `sources/`.

## Reports and sensitive material

Public examples must identify their exact candidate and status. Never publish credentials, private client material, protected infrastructure, unresolved exploit details, or coordinated-disclosure evidence. Use a sanitized report after correction or coordinated disclosure.
