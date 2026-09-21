# Brand Navigation Discourse Review

**Repository:** [codeWorksLabs/brand-navigation](https://github.com/codeWorksLabs/brand-navigation)  
**Rubric:** `DiscourseSkill.md` only  
**Review date:** 2026-09-21

## 1. Review scope

Reviewed `codeWorksLabs/brand-navigation` using only `DiscourseSkill.md` as the
evaluation rubric.

- Target: `main`
- Commit: `f87fa98ceccab92285bbc40fc28a817ec09cf4d0`
- Version context: unreleased `main`, 11 documentation-only commits after
  `v1.0.0-rc.1`
- Artifact: Discourse theme component, not a Rails plugin
- Reviewed: runtime/admin code, settings, locales, styles, tests, CI,
  dependencies, release and migration procedures, security documentation,
  license, tags, and history
- Locally executed:
  - `pnpm install --frozen-lockfile` — passed
  - `pnpm test:config` — 24/24 passed
  - `pnpm lint` — passed all template, formatting, type, CSS, and JavaScript
    checks
  - `git diff --check` — passed
- Not locally executed:
  - Discourse frontend, backend, and Ruby system suites because this environment
    lacks Discourse core and Ruby
  - Live installation, upgrade, disablement, and rollback on a Discourse
    instance

The repository remained clean after verification.

## 2. Summary

| Classification | Count |
|---|---:|
| Critical | 0 |
| High | 0 |
| Medium | 0 |
| Low | 0 |
| Info | 0 |
| Material concerns not fully verified | 5 |

No required correctness, security, privacy, compatibility, or release-hygiene
findings were identified in the reviewed scope.

The implementation uses normal theme-component extension points, constrains
imported configuration, rejects unsafe URLs, cleans up browser resources,
documents its compatibility evidence, and distinguishes prerelease evidence
from stable-release readiness.

**Confidence:** Moderate-high for static implementation and repository quality;
moderate for production readiness because several manual and integrated
verification gates remain open.

## 3. Required findings

No required findings identified.

In particular:

- No unsupported monkey-patching or direct core modification was found.
- No custom server endpoints, migrations, background jobs, database access, or
  credential handling exist.
- No unsafe HTML insertion, dynamic code execution, or external data
  transmission was found.
- Imported URLs are restricted to root-relative or credential-free HTTPS URLs
  in
  [`configuration-bundle.js`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/javascripts/discourse/lib/configuration-bundle.js#L384-L417).
- Import sizes and collection cardinalities are bounded in
  [`configuration-bundle.js`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/javascripts/discourse/lib/configuration-bundle.js#L3-L8).
- Administrator changes use Discourse's authenticated theme settings endpoint
  in
  [`brand-navigation-admin.js`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/javascripts/discourse/lib/brand-navigation-admin.js#L44-L49).
- External `_blank` links receive `noopener noreferrer` in
  [`brand-navigation.js`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/javascripts/discourse/lib/brand-navigation.js#L27-L30).
- Document listeners and the sprite observer are cleaned up during teardown.
- Embed exclusion uses Discourse's embed-mode API rather than page-shape
  heuristics.
- The release candidate is explicitly represented as a prerelease rather than
  a stable release.

## 4. Test and verification gaps

These are unverified areas, not confirmed defects.

### 4.1 Exact-checkout Discourse-integrated tests

The official Discourse frontend, backend, or Ruby system suites could not be
independently executed in this environment. The repository records passing
official workflow runs on implementation-equivalent commits, and the changes
after `v1.0.0-rc.1` are documentation-only.

### 4.2 Classic comments embed acceptance

Browser/runtime evidence exists, but the project deliberately retains a final
human confirmation gate for an allowed external embed host in
[`docs/TESTING.md`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/docs/TESTING.md#L505-L513).

### 4.3 Complete RTL acceptance

RTL runtime evidence exists, but a complete desktop/mobile human pass covering
focus, responsive modes, themes, and embeds remains open in
[`docs/TESTING.md`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/docs/TESTING.md#L514-L516).

### 4.4 Complete screen-reader acceptance

Partial iPhone VoiceOver evidence is recorded, but expanded-state announcement,
dismissal, focus return, responsive controls, and other scenarios remain
incomplete in
[`docs/TESTING.md`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/docs/TESTING.md#L517-L521).

### 4.5 Full rollback exercise

The pin-and-return rollback procedure remains explicitly provisional because
the complete workflow has not been recorded on staging. See
[`docs/MIGRATION.md`](https://github.com/codeWorksLabs/brand-navigation/blob/f87fa98ceccab92285bbc40fc28a817ec09cf4d0/docs/MIGRATION.md#L131-L133).

## 5. Optional improvements

- Complete and record the three remaining `v1.0.0` manual acceptance gates
  before labeling a stable release.
- Execute and record the complete staging pin-and-return rollback workflow.
- Add a compact support table explicitly distinguishing:
  - minimum supported Discourse release;
  - currently tested releases;
  - maintained `d-compat/*` branches.
- Consider replacing the five-setting administrator component signature with a
  stronger explicit marker if Discourse exposes a stable mechanism. The current
  matcher fails closed for incomplete signatures, but an unrelated component
  with the same five setting names could theoretically be mistaken for Brand
  Navigation.
- Remove or reconcile the apparently unused top-level `description` validation
  in `configuration-bundle.js` so validation and `settings.yml` cannot drift
  over time.

## 6. Rule matrix

| Rule | Status | Basis |
|---|---|---|
| 01 — Clear and legitimate capability | Pass | Purpose and administrator/user behavior are clearly documented. |
| 02 — Supported extension points | Pass | Uses theme outlets, initializers, `api.headerIcons`, and Discourse embed mode. |
| 03 — Data model and lifecycle | Not applicable | No plugin models or persistent application data; configuration uses native theme settings. |
| 04 — Safe migrations | Not applicable | No database migrations. |
| 05 — Server authorization | Not applicable | No custom server endpoints; privileged writes use Discourse's existing admin endpoint. |
| 06 — Input validation/output encoding | Pass | Strict schemas, unknown-key rejection, safe URLs, bounded sizes, and normal template escaping. |
| 07 — Credentials/external services | Not applicable | No credentials, secrets, OAuth, or external service integration. |
| 08 — Privacy/admin control | Pass | No analytics or data export to third parties; behavior is controlled through native settings. |
| 09 — Background work | Not applicable | No jobs, schedules, or asynchronous server workers. |
| 10 — Distributed-operation recovery | Not applicable | No synchronization or distributed external operations. |
| 11 — Native administration | Pass | Administration is integrated into the theme component settings interface. |
| 12 — Coherent user behavior | Not verified | Keyboard and responsive coverage is substantial, but final RTL and assistive-technology gates remain open. |
| 13 — Robust frontend integration | Pass | Supported hooks, embed guards, lifecycle cleanup, and no DOM polling or core replacement found. |
| 14 — Complete and safe settings | Pass | Settings have types, defaults, constrained enums, translations, and validation. |
| 15 — Explicit API contracts | Not applicable | No public HTTP API or webhook contract. |
| 16 — Tests for site-breaking behavior | Pass | Configuration, visibility, URLs, import/export, accessibility behavior, limits, and admin persistence have focused tests. |
| 17 — Standard Discourse checks | Not verified | Local lint passed and historical official runs are recorded, but the integrated suite was not rerun here. |
| 18 — Installable release | Not verified | Installation evidence exists for tagged and compatibility refs, but exact HEAD was not independently installed. |
| 19 — Safe upgrades | Not verified | Native update evidence exists; the complete rollback workflow remains provisional. |
| 20 — Predictable disablement/removal | Pass | Native disable/detach behavior is documented; no jobs or private persistent data survive disablement. |
| 21 — Deliberate compatibility | Pass | Exact tested builds and maintained compatibility branches are recorded. |
| 22 — Constrained dependencies | Pass | Frozen pnpm lockfile, pinned toolchain, and no runtime external dependencies. |
| 23 — Security boundaries | Pass | No authentication bypass, unsafe HTML, arbitrary protocols, or privilege-boundary modifications found. |
| 24 — Operational transparency | Pass | Import/export, compatibility, update, embed, and rollback behavior are documented. |
| 25 — Documentation/support path | Pass | README, user guide, testing, migration, release, security, and support guidance are present. |
| 26 — Honest representation | Pass | Evidence limitations and incomplete manual gates are disclosed explicitly. |
| 27 — Distribution rights | Pass | GPL-2.0-or-later licensing and project attribution are present. |
| 28 — Repository/release hygiene | Pass | Clean checkout, focused source tree, pinned CI, lockfile, changelog, and no generated artifacts committed. |
| 29 — Honest prerelease treatment | Pass | `v1.0.0-rc.1` is explicitly a prerelease; `v1.0.0` remains reserved. |
| 30 — Obsolete compatibility removal | Not applicable | No obsolete compatibility shim was identified in the reviewed runtime source. |

## Overall conclusion

The inspected implementation presents no required findings under
`DiscourseSkill.md`, but stable-release readiness remains contingent on the
documented manual accessibility, embed, and rollback verification gates.
