# Brand Navigation Review Gap-Closure Plan

**Repository:** [codeWorksLabs/brand-navigation](https://github.com/codeWorksLabs/brand-navigation)  
**Reviewed commit:** `f87fa98ceccab92285bbc40fc28a817ec09cf4d0`  
**Review rubric:** `DiscourseSkill.md` only  
**Plan date:** 2026-09-21

## Objective

Close the five material verification gaps identified in the Brand Navigation
review and produce sufficient evidence to reconsider Rules 12, 17, 18, and 19
as `Pass`.

A local Discourse installation is required for most of this work. One local
installation alone is not sufficient: the review also requires supported-version
coverage, an external embed fixture, human screen-reader testing, and a complete
update-and-rollback exercise.

## 1. Run the complete Discourse test matrix

Run the official Discourse theme-component workflow, or its equivalent suites,
against the exact reviewed Brand Navigation commit on:

- Current Discourse `main`
- Discourse 2026.9
- Discourse 2026.8
- Each maintained 2026.7 ESR target

The execution must include the applicable lint, locale, frontend QUnit, backend,
and Ruby system-test lanes.

Record:

- Exact Discourse commit for each target
- Brand Navigation commit and ref
- Ruby, Node.js, pnpm, and browser versions
- Commands or workflow run identifiers
- Complete pass/fail results

Successful results would close the current Rule 17 verification gap.

## 2. Verify clean installation and lifecycle behavior

On a clean local Discourse installation:

1. Install Brand Navigation from its documented repository URL.
2. Attach it to Foundation and Horizon.
3. Configure every supported setting type.
4. Test anonymous, authenticated, staff, desktop, and mobile contexts.
5. Disable and re-enable the component.
6. Detach and reattach it to the themes.
7. Remove and reinstall it where appropriate.
8. Confirm that expected settings and normal Discourse behavior remain intact.

This would close most of the Rule 18 installability gap if no defects are found.

## 3. Verify native update and rollback

Use a staging-like Discourse installation and begin at `v1.0.0-rc.1`:

1. Configure representative navigation items, header icons, uploads, colors,
   visibility rules, and responsive behavior.
2. Export a configuration bundle and retain a settings baseline.
3. Update through Discourse's native theme manager to commit
   `f87fa98ceccab92285bbc40fc28a817ec09cf4d0`.
4. Confirm that settings, uploads, rendering, and administrator controls remain
   correct.
5. Pin back to `v1.0.0-rc.1` using the documented procedure.
6. Confirm that the older version operates correctly and retains its expected
   configuration.
7. Return to `main` or the appropriate maintained `d-compat/*` branch.
8. Confirm that the component and configuration recover correctly.
9. Record the exact pin-and-return procedure in the project documentation.

Successful execution would close the current Rule 19 gap and replace the
provisional rollback procedure with verified evidence.

## 4. Complete classic-comments embed acceptance

Configure an allowed embed host and create a real external HTML page using
Discourse's classic comments embed.

Verify that:

- Embedded discussion content renders.
- Reply counts, authors, timestamps, and core interaction controls remain
  available.
- Brand Navigation does not mount or load runtime UI inside the embed.
- No related browser-console or server errors occur.
- Anonymous and authenticated contexts behave correctly where applicable.

Repeat the exclusion checks for full-app embed mode at desktop and mobile
viewports.

A localhost-hosted external page is acceptable if the Discourse instance is
configured to recognize it as an allowed embed host.

## 5. Complete RTL acceptance

Use an RTL locale such as Arabic and verify:

- Desktop and mobile layouts
- Menu, bar, and hidden responsive modes
- Linked-parent and submenu-group behavior
- Submenu alignment and logical positioning
- Keyboard traversal and activation
- Escape dismissal and focus return
- Foundation and Horizon
- Light and dark color schemes
- Normal application pages, classic comments embeds, and full-app embeds

Record screenshots and the computed document direction for each representative
case.

## 6. Complete human screen-reader acceptance

Automated accessibility-tree checks do not close this gate. Conduct controlled
human testing, preferably with both:

- VoiceOver and Safari
- NVDA and Firefox or Chrome

Verify:

- Navigation landmark names
- Link and button accessible names
- Expanded and collapsed state announcements
- Linked-parent and submenu-caret actions
- Keyboard and screen-reader dismissal
- Focus return after closure
- Visible-description associations
- Header icon links
- Mobile and responsive controls
- Embed exclusion

Any incomplete announcement or interaction must be recorded as a result rather
than inferred to pass.

## 7. Evidence package

For every manual or automated run, retain:

- Brand Navigation version, ref, commit, and tree identity
- Discourse version and exact core commit
- Active theme and color scheme
- Browser, operating system, viewport, and device
- Screen-reader name and version where applicable
- Initial configuration and relevant fixtures
- Exact procedure
- Expected and actual results
- Screenshots or recordings where useful
- Browser-console and server errors
- Pass/fail disposition
- Links to every discovered defect and its retest result

## Required environments

| Environment | Purpose |
|---|---|
| Clean local Discourse development instance | Installation, settings, lifecycle, frontend, and system verification |
| Supported-version instances or containers | Current, 2026.9, 2026.8, and maintained 2026.7 ESR coverage |
| Staging-like installation | Native update, tag pinning, rollback, and return-to-current verification |
| Allowed external embed page | Classic comments and full-app embed exclusion |
| RTL browser environment | Complete RTL desktop/mobile acceptance |
| Human assistive-technology environment | VoiceOver and preferably NVDA acceptance |

## Expected rule disposition after successful completion

| Rule | Current status | Potential status | Condition |
|---|---|---|---|
| 12 — Coherent user-facing behavior | Not verified | Pass | Complete RTL and human screen-reader acceptance with clean results |
| 17 — Standard Discourse checks | Not verified | Pass | Full supported-version test matrix passes on the reviewed source |
| 18 — Installable release | Not verified | Pass | Clean installation and lifecycle exercise passes |
| 19 — Safe upgrades | Not verified | Pass | Native update, rollback, and return-to-current exercise passes |

## Completion criterion

The current material verification gaps are closed when every procedure above is
completed against recorded source and environment identities, all results are
retained, and any discovered defect has been corrected and successfully
retested.

Successful completion does not eliminate all possible operational risk. It does
remove the material unverified areas identified in the original review and
provides evidence for a substantially stronger release-readiness conclusion.
