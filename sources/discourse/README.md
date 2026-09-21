# Discourse design sources

These files preserve the complete output package supplied by the separate Discourse review-design task:

- `DiscourseSkill.original.md` — its original human-readable draft;
- `DiscourseSkill.improved.json` — its structured improvement intermediate;
- `discourse-skill-improvements-report.md` — its analysis and recommended architecture.

They are design provenance, not active review instructions. The maintained Discourse guidance distilled from that work lives at `.agents/skills/codeworkslabs-platform-review/references/platforms/discourse/DiscourseSkill.md`.

The structured JSON is retained because it contains useful requirement mappings and routing metadata, but agents must not treat it as a second controlling skill.
