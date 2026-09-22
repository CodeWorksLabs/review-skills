# Discourse review core provenance

Status: CodeWorksLabs-maintained public review core. It is not official Discourse, CDCK, Marketplace, or Meta policy and grants no approval.

## Active files

- `DiscourseSkill.md` is the complete working human-readable skill, evolved from the originating Discourse review-design task.
- `DiscourseSkill.json` is the canonical machine-readable core, evolved from that task's structured improvement artifact.

Current ruleset: `0.1.2` (`community-draft`).

Current active identities:

- `DiscourseSkill.md`: 40,901 bytes; 1,172 lines; SHA-256 `78786b92d15bcbf95fb81c920c3aa9f0fd802c41f4e6b7605d2655d9c72dc268`.
- `DiscourseSkill.json`: 113,754 bytes; 1,427 lines; SHA-256 `21cf151b91d355443259727ed1346c0666fcb78354b71722f1f5abf6c038ceb6`.
- `LOCAL_TEST_MATRIX.md`: 5,517 bytes; 88 lines; SHA-256 `5f39f9a366520c6566e0a8ac9c05c209763bbf1abb72b3a140667e373089ba05`.

## Originating identities

- `sources/discourse/DiscourseSkill.original.md`: 35,715 bytes; SHA-256 `94a355d6c52d8e8330886be4d8ae6f7a28281fad80d919fdac1e17b4688149c8`.
- `sources/discourse/DiscourseSkill.improved.json`: 107,283 bytes; SHA-256 `4d58939019c4ec71be4410e35b4fbbff5ab5b0431f6a34ebd40fc74fc1cc6c84`.

The canonical JSON retains the original Markdown SHA-256 in its lineage and states its transformation: the original rules are preserved and augmented with artifact routing, review modes, evidence thresholds, release policies, version coverage, and a machine-readable report contract.

## Maintenance rule

Treat the JSON and Markdown as one active platform package. A change must identify which requirement changes, preserve or intentionally supersede its counterpart, refresh both recorded identities, and explain any changed behavior. Do not replace either file with an abbreviated summary.

The exact originating copies remain under `sources/discourse/` so later maintenance can distinguish original bytes from deliberate evolution of the active working package.
