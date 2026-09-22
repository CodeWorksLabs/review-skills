# Discourse review core provenance

Status: CodeWorksLabs-maintained public review core. It is not official Discourse, CDCK, Marketplace, or Meta policy and grants no approval.

## Active files

- `DiscourseSkill.md` is the complete working human-readable skill, evolved from the originating Discourse review-design task.
- `DiscourseSkill.json` is the canonical machine-readable core, evolved from that task's structured improvement artifact.

Current ruleset: `0.1.0` (`community-draft`).

Current active identities:

- `DiscourseSkill.md`: 38,205 bytes; 1,159 lines; SHA-256 `e80e8de9c18eff28ba4992c3fdfcaf91a58be649ba12be52ad2880c731d5c127`.
- `DiscourseSkill.json`: 110,249 bytes; 1,370 lines; SHA-256 `8048da5e9df1bfaf161f7e6b6df56af93029e88704d1033f9a095adb4745c2da`.

## Originating identities

- `sources/discourse/DiscourseSkill.original.md`: 35,715 bytes; SHA-256 `94a355d6c52d8e8330886be4d8ae6f7a28281fad80d919fdac1e17b4688149c8`.
- `sources/discourse/DiscourseSkill.improved.json`: 107,283 bytes; SHA-256 `4d58939019c4ec71be4410e35b4fbbff5ab5b0431f6a34ebd40fc74fc1cc6c84`.

The canonical JSON retains the original Markdown SHA-256 in its lineage and states its transformation: the original rules are preserved and augmented with artifact routing, review modes, evidence thresholds, release policies, version coverage, and a machine-readable report contract.

## Maintenance rule

Treat the JSON and Markdown as one active platform package. A change must identify which requirement changes, preserve or intentionally supersede its counterpart, refresh both recorded identities, and explain any changed behavior. Do not replace either file with an abbreviated summary.

The exact originating copies remain under `sources/discourse/` so later maintenance can distinguish original bytes from deliberate evolution of the active working package.
