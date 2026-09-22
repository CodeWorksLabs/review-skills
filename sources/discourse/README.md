# Discourse design sources

These files preserve the complete output package supplied by the separate Discourse review-design task:

- `DiscourseSkill.original.md` — its original human-readable draft;
- `DiscourseSkill.improved.json` — its structured improvement intermediate;
- `discourse-skill-improvements-report.md` — its analysis and recommended architecture.

They are immutable design provenance, not a second active instruction set. Exact working copies of the complete Markdown skill and structured JSON core live under `.agents/skills/codeworkslabs-platform-review/references/platforms/discourse/` and are loaded together by the wrapper.

The source `DiscourseSkill.improved.json` is preserved unchanged. Its active, versioned successor is `DiscourseSkill.json` in the platform package.
