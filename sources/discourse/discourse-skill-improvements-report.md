# Discourse Review Skill Improvements Report

**Subject:** Improvements to the current `DiscourseSkill.md`  
**Current skill name:** `discourse-plugin-review`  
**Report date:** 2026-09-21

## Executive summary

The current `DiscourseSkill.md` has strong Discourse-specific technical coverage,
clear evidence requirements, useful severity definitions, and appropriately
cautious outcome language. Its principal weaknesses are structural:

1. It assumes the reviewed artifact is a Rails plugin, although Discourse theme
   components require a materially different review.
2. It combines static analysis, integrated runtime testing, and release-readiness
   verification without requiring the reviewer to declare which level was
   performed.
3. It does not define sufficiently precise evidence thresholds for `Pass`,
   `Finding`, `Not verified`, and `Not applicable` on each rule.
4. At more than 1,100 lines, it loads substantial plugin-only guidance even when
   the target is a theme component.
5. It lacks a deterministic artifact and evidence collection step.

The recommended design is one umbrella `discourse-extension-review` skill with
shared rules and separately routed plugin and theme-component profiles. This
preserves consistent severity, reporting, and release standards without forcing
irrelevant plugin rules onto theme-component reviews.

## 1. Introduce explicit extension classification

Every review should begin by classifying the target as one of:

- Rails plugin
- Theme
- Theme component
- Plugin containing theme assets
- Connector or integration repository
- Exact release artifact
- Development branch or working tree

The reviewer should record both the artifact type and the evidence supporting
the classification. Ambiguous or mixed repositories should load every relevant
profile.

This classification should occur before the numbered rules are applied. It
prevents plugin-only requirements—such as migrations, controllers, and
background jobs—from obscuring the important frontend and lifecycle risks in a
theme component.

## 2. Use one skill with distinct review profiles

Plugins and theme components need distinct review profiles, but they should not
normally be maintained as two completely independent skills. Their shared
review principles, severity model, evidence rules, release identity checks, and
report format would otherwise drift apart.

Recommended package structure:

```text
discourse-extension-review/
├── SKILL.md
├── references/
│   ├── shared-rules.md
│   ├── plugin-review.md
│   ├── theme-component-review.md
│   ├── verification-matrix.md
│   ├── release-readiness.md
│   ├── severity-and-status.md
│   └── report-format.md
└── scripts/
    └── collect-review-evidence.py
```

The main `SKILL.md` should classify the repository, select the review mode, load
only the applicable references, and enforce the common output contract.

Two separate top-level skills should be considered only if automatic routing
repeatedly misclassifies targets or if users consistently invoke plugin and
theme-component reviews as completely separate products.

## 3. Plugin and theme-component applicability

| Review area | Plugin | Theme component |
|---|---:|---:|
| `plugin.rb` and enabled-site setting | Required | Not applicable |
| Rails models, controllers, and serializers | Often applicable | Not applicable |
| Server authorization | Critical | Usually not applicable |
| Database migrations | Often applicable | Not applicable |
| Background jobs and webhooks | Sometimes applicable | Not applicable |
| Plugin API and outlets | Applicable | Critical |
| Theme settings and object schemas | Sometimes applicable | Critical |
| Ember/Glimmer lifecycle | Applicable | Critical |
| CSS and theme compatibility | Applicable | Critical |
| Accessibility and responsive behavior | Applicable | Critical |
| Theme attachment and detachment | Not applicable | Critical |
| Foundation and Horizon compatibility | Sometimes applicable | Critical |
| Discourse plugin test suite | Required | Not applicable |
| Discourse theme workflow | Sometimes applicable | Required |

### Shared rules

Both profiles should retain requirements for:

- A clear and legitimate capability
- Supported Discourse integration points
- Input, output, and URL validation
- Privacy and administrator control
- Dependency constraints
- Compatibility claims
- Testing evidence
- Documentation and support paths
- Licensing and distribution rights
- Exact release identity
- Honest experimental and prerelease representation

### Plugin-specific rules

The plugin profile should emphasize:

- Server-side authorization
- Routes and API contracts
- Models, serializers, and query behavior
- Database migrations and rollback safety
- Background jobs and retry behavior
- Synchronization and distributed recovery
- Credentials and external services
- Multisite behavior
- Enablement, disablement, uninstall, and retained-data lifecycle

### Theme-component-specific rules

The theme-component profile should emphasize:

- Supported outlets, connectors, modifiers, and Plugin API usage
- Theme setting and object-schema validation
- Ember/Glimmer setup and teardown
- Event-listener, observer, and subscription cleanup
- Responsive modes and mobile navigation
- Keyboard operation and focus management
- Screen-reader behavior
- RTL and logical layout
- Foundation and Horizon compatibility
- Embed-mode exclusion
- Attachment, detachment, and native theme updates
- CSS leakage and selector stability
- Upload and asset behavior
- Header icon and SVG sprite integration

## 4. Require a declared review mode

The skill currently combines several kinds of review. Each report should declare
one of the following modes:

- **Static review:** Source, configuration, tests, dependencies, and
  documentation are inspected.
- **Repository verification:** Static review plus locally available lint and
  test commands.
- **Integrated verification:** The extension is installed in Discourse and its
  runtime/system behavior is exercised.
- **Release-readiness review:** The exact release artifact is installed, tested
  across supported versions, upgraded, and rolled back.
- **Focused review:** A clearly bounded security, compatibility, migration,
  accessibility, or other specialist review.

A local Discourse installation should be required for integrated and
release-readiness modes. It should not be a universal prerequisite for a static
review, provided the report clearly marks runtime conclusions as unverified.

Example scope statement:

> Review mode: Repository verification. Runtime installation, native update,
> and rollback conclusions remain unverified.

## 5. Strengthen status definitions

Use deterministic status definitions:

- **Pass:** The rule is applicable, the important implementation or execution
  paths were inspected or exercised at the evidence level required by the
  selected review mode, and no violation was found.
- **Finding:** Direct evidence demonstrates a violation of the rule.
- **Not verified:** The rule is applicable, but a required artifact,
  environment, execution path, or external condition was unavailable.
- **Not applicable:** The capability is absent, and the reviewer established
  that its absence makes the rule irrelevant.

The report must keep these dimensions separate:

- Rule status
- Finding severity
- Confidence
- Release-blocking status

A low-confidence concern is not automatically a finding. A high-confidence
observation is not necessarily severe. A `Not verified` release gate can block
a release-readiness conclusion without being a defect.

## 6. Define evidence thresholds for important rules

Each applicable rule should state the minimum evidence necessary for `Pass`.

Examples:

- Standard quality checks cannot fully pass merely because workflow files
  exist; an applicable successful execution must be recorded.
- Installability requires installing the exact reviewed artifact.
- Upgrade safety requires upgrading from a supported prior release.
- Rollback safety requires an actual rollback or a clearly bounded conclusion
  that rollback was not verified.
- Keyboard behavior requires interaction testing, not markup inspection alone.
- Human screen-reader claims cannot be established solely from an automated
  accessibility tree.
- Version compatibility requires execution against the claimed versions, not
  merely an absence of obviously incompatible code.

This would make the distinction between static confidence and release-readiness
evidence much more consistent.

## 7. Require exact artifact identity

Every review should record:

- Repository URL
- Artifact type
- Branch
- Commit
- Tree hash
- Tag
- Declared version
- Archive hash, when applicable
- Dirty and untracked state
- Latest published release
- Changes between the reviewed source and the published tag
- Whether those changes affect runtime code, tests, packaging, or only
  documentation

When reviewing a release, installation testing should use the same tag or
archive that users receive.

When reviewing a later branch, the report should not silently transfer release
evidence from an older artifact. It should establish whether the relevant
runtime tree is identical.

## 8. Add evidence-reconciliation rules

Repository documentation frequently contains historical statements that appear
to conflict with newer evidence. The skill should require the reviewer to:

1. Identify contradictory or overlapping evidence.
2. Compare dates, commits, trees, environments, and tested behaviors.
3. Determine whether later evidence actually supersedes earlier evidence.
4. Preserve narrower limitations that remain unresolved.
5. Mark unresolved contradictions as `Not verified`.

The newest statement should not automatically win. It must describe the same or
an implementation-equivalent artifact and the same behavior.

## 9. Add a verification matrix

The skill should distinguish static, automated, and runtime evidence:

| Claim | Static evidence | Automated execution | Runtime/manual evidence |
|---|---|---|---|
| Installs successfully | Metadata and packaging appear complete | Packaging validation | Clean installation of exact artifact |
| Upgrade is safe | Migration and compatibility inspection | Upgrade/migration tests | Upgrade from supported prior release |
| Rollback is safe | Reversibility analysis | Down-migration or compatibility tests | Staging rollback and recovery |
| Accessible | Semantic markup inspection | QUnit or accessibility automation | Keyboard and human screen-reader pass |
| Version compatible | API and dependency inspection | Supported-version matrix | Representative browser smoke test |
| Embed safe | Embed guard inspection | Component tests | Real external embed fixture |

The selected review mode determines which evidence levels are required. Missing
evidence must remain visible rather than being inferred from lower-level checks.

## 10. Clarify release blockers

Suggested release-readiness rules:

- Any Critical or High required finding blocks a positive release-readiness
  conclusion.
- A Medium finding blocks release readiness when it affects installation,
  authorization, private data, upgrades, rollback, or the extension's primary
  advertised behavior.
- Unverified installation or upgrade behavior prevents a positive
  release-readiness conclusion.
- Unverified rollback must be disclosed and may block stable release when the
  update changes persistent data or configuration formats.
- Open manual accessibility testing does not automatically prove a defect, but
  advertised accessibility must remain unverified.
- Experimental releases may retain documented limitations when they are
  represented honestly and do not create unreasonable site risk.

## 11. Improve rule-specific precision

The following rules would benefit from more explicit profile-specific criteria:

- **Supported integration:** Distinguish stable Plugin API methods, outlets,
  connectors, value transformers, internal Ember component targets, and direct
  core modification.
- **Authorization:** Explain that use of an existing Discourse administrator
  endpoint does not itself create a new server authorization surface.
- **Validation:** Cover imported configuration bundles, URL schemes,
  object-setting size limits, unknown keys, diagnostic escaping, and denial-of-
  service bounds.
- **User-facing behavior:** Define keyboard, focus, screen-reader, responsive,
  RTL, color-scheme, and reduced-motion expectations.
- **Standard checks:** Separate the plugin test workflow from the theme-component
  workflow.
- **Installability:** Separate repository metadata inspection from a clean
  installation exercise.
- **Upgrade safety:** Separate forward update, rollback, and return-to-current
  verification.
- **Disablement/removal:** Distinguish disabling, detaching, uninstalling, and
  deleting retained configuration.
- **Compatibility:** Require clear separation of `known working`, `tested`,
  `supported`, and `minimum supported` versions.

## 12. Add deterministic evidence collection

A read-only helper such as `scripts/collect-review-evidence.py` could record:

- Git remote, branch, commit, tag, tree, and dirty state
- Commits and changed paths since the latest tag
- Plugin or theme metadata
- Settings and locale files
- Dependency manifests and lockfiles
- Migrations, routes, controllers, serializers, jobs, and models
- JavaScript initializers, connectors, outlets, modifiers, and components
- Test files and CI workflows
- Available Ruby, Node.js, package-manager, and browser versions
- Candidate release archives

The script should produce an evidence manifest rather than conclusions. Rule
applicability and findings still require engineering judgment.

## 13. Improve the report contract

Every report should include:

1. Review mode
2. Artifact type
3. Exact source identity
4. Claimed compatibility
5. Evidence levels reached
6. Commands and environments actually used
7. Overall confidence
8. Required findings
9. Unverified release blockers
10. Non-blocking verification gaps
11. Optional improvements
12. Rule matrix with evidence references
13. Release-readiness disposition, when requested

Each rule-matrix entry should cite a concise basis rather than reporting status
alone.

An optional machine-readable companion could use records such as:

```json
{
  "rule": "19",
  "status": "not_verified",
  "severity": null,
  "confidence": "medium",
  "release_blocking": true,
  "evidence": ["docs/MIGRATION.md:131"],
  "reason": "Complete pin-and-return rollback was not executed."
}
```

## 14. Package it as a discoverable Codex skill

If this is intended to be a reusable Codex skill rather than a standalone
rubric, it should be stored as:

```text
discourse-extension-review/SKILL.md
```

The current standalone filename `DiscourseSkill.md` is useful as a document but
does not follow the standard discoverable skill-package structure.

The frontmatter should also reflect the broader scope. For example:

```yaml
---
name: discourse-extension-review
description: Review Discourse plugins, themes, and theme components for supported integration, correctness, security, compatibility, lifecycle safety, accessibility, documentation, and release readiness. Use for static audits, integrated verification, or release review of a Discourse extension.
---
```

## Recommended implementation order

1. Rename and package the skill as `discourse-extension-review`.
2. Add artifact classification and review-mode selection to the entrypoint.
3. Separate plugin and theme-component rules into routed references.
4. Define rule-status and evidence thresholds.
5. Add exact source-identity and evidence-reconciliation procedures.
6. Add the verification and release-blocker matrices.
7. Update the report contract.
8. Add and test a read-only evidence collector.
9. Forward-test the revised skill independently on:
   - one conventional Rails plugin;
   - one theme component;
   - one plugin with substantial frontend assets;
   - one intentionally incomplete release candidate.

## Conclusion

Plugins and theme components should receive different technical reviews, but
the best maintainable design is one umbrella Discourse extension review skill
with separate profiles. The shared package should retain one severity model,
one evidence vocabulary, one release standard, and one report contract.

The three most important changes are:

1. Classify plugin versus theme component before applying rules.
2. Declare whether the review is static, integrated, or release-focused.
3. Define the exact evidence required to move every applicable rule from
   `Not verified` to `Pass`.

These changes would produce shorter, more relevant reviews while making their
conclusions more reproducible and defensible.
