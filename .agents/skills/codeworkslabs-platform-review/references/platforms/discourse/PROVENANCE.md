# Discourse review core provenance

Status: CodeWorksLabs-maintained public review core. It is not official Discourse, CDCK, Marketplace, or Meta policy and grants no approval.

## Active files

- `DiscourseSkill.md` is the complete working Markdown skill supplied by the originating Discourse review-design task.
- `DiscourseSkill.improved.json` is that task's complete structured improvement artifact and the active machine-readable core.

Exact originating identities:

- `DiscourseSkill.md`: 35,715 bytes; SHA-256 `94a355d6c52d8e8330886be4d8ae6f7a28281fad80d919fdac1e17b4688149c8`.
- `DiscourseSkill.improved.json`: 107,283 bytes; SHA-256 `4d58939019c4ec71be4410e35b4fbbff5ab5b0431f6a34ebd40fc74fc1cc6c84`.

The JSON records the Markdown SHA-256 in its lineage and states its transformation: the original rules are preserved and augmented with artifact routing, review modes, evidence thresholds, release policies, and a machine-readable report contract.

## Maintenance rule

Treat the JSON and Markdown as one active platform package. A change must identify which requirement changes, preserve or intentionally supersede its counterpart, refresh both recorded identities, and explain any changed behavior. Do not replace either file with an abbreviated summary.

The exact originating copies remain under `sources/discourse/` so later maintenance can distinguish original bytes from deliberate evolution of the active working package.
