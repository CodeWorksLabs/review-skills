---
name: marketplace-review
description: Review a Statamic starter kit or add-on before marketplace submission against eleven numbered submission standards. Report evidence, uncertainty, impact, and required changes without granting approval.
---

# Statamic marketplace review

Policy revision: 2026-09-14.
Canonical public policy: https://statamic.com/marketplace/submission-guidelines

Review the product in the current repository against the applicable rules below. These are requirements for free and paid products; small, focused products are welcome. AI tools are allowed. The creator remains responsible for personally reviewing code, refining design, testing the release, and maintaining the product. Evaluate the finished work, not the tools used to create it.

## Review boundaries

Determine whether the product is a starter kit or add-on from Composer metadata, its service provider, starter-kit manifest, and README. Inspect working-tree status and identify the release or commit under review. Respect the product’s purpose, supported versions, and framework.

Read the public policy when browsing is available and note any revision difference from this copy. Follow its current requirements; if unavailable, use this bundled revision and state that the live policy was not checked. Never silently invent or renumber rules.

Inspect the implementation and the distributed artifact rather than relying on README claims. Run installation checks only in an isolated fresh site when authorized. Never run clear-site installation or destructive migrations against an existing site. Do not change files unless asked for fixes. Do not publish, submit, reject, commit, or contact anyone as part of the review. Avoid real external-service calls without authorization, and never reproduce secrets in the report.

## Evidence and applicability

During the review, distinguish verified findings, needs attention, not checked, and not applicable for each applicable rule. Keep this coverage tracking out of the final response unless requested. A missing piece of evidence is not proof of a violation. Understand why a requirement does not apply without making the creator read an explanation for every unrelated requirement. A present field or URL proves presence only, not correctness, working behavior, licensing rights, or installation success.

Do not infer AI use, human authorship, or personal review from code style or appearance. Do not treat generic aesthetics as evidence of copying. Compare to an identified source or related product only when comparison evidence is available and cite it. State the limits of the comparison; never claim to have searched the entire marketplace.

Reviewers must identify specific shortcomings. “Looks AI-generated,” “feels generic,” or “isn’t our style” is insufficient feedback on its own. Minimalism, unusual aesthetics, and low prices are not rejection reasons.

## Rule 01: Offer substantial original value

Applies to: All products.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-01

Your product must contribute a distinct design, capability, or workflow. Cosmetic variants belong within one product.

- Acceptable: Two podcast kits with substantially different designs and publishing experiences. Bringing your own original design from another platform to Statamic with a thoughtfully built native implementation. An integration that makes a specific service work naturally in Statamic. Multiple color schemes bundled with one kit.
- Not acceptable: Selling the same kit repeatedly with different names, colors, images, or industry labels. Lightly reskinning a purchased template or another creator’s kit.
- Exception or boundary: Shared libraries, frameworks, and foundations are fine. Neither overlapping audiences nor familiar design patterns alone demonstrate duplication. Converting someone else’s finished template to Statamic does not, by itself, establish substantial original value.

## Rule 02: Use Statamic’s native capabilities appropriately

Applies to: Starter kits & add-on integrations.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-02

Starter kits must model content in Statamic. Add-ons must integrate through supported extension points.

- Acceptable: Navigation managed through Navigations or an appropriate collection-driven menu; shared settings in Globals; content images in asset fields; entries in Collections; collection mounting where the site structure calls for it.
- Not acceptable: Hard-coded editable menus, footer details, or article lists. URLs that break when an entry moves. Modifying Statamic core files to make an add-on work.
- Exception or boundary: Decorative assets and fixed utility links may remain in templates. Products do not need to use features unrelated to their purpose.

## Rule 03: Make content editable and components reusable

Applies to: Starter kits & content-editing add-ons.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-03

Routine editing must work without editing code, including HTML stored in a textarea. Shared structures should have a maintainable implementation.

- Acceptable: Clearly labeled blueprints; appropriate field types; reusable fields and partials; editors can add, remove, and reorder the content the product promises to support.
- Not acceptable: An entire site stored in one HTML field; a menu that requires editing HTML in Globals; duplicated headers that must be edited separately; adding a testimonial requires changing a template; empty optional fields leave broken markup.
- Exception or boundary: A kit does not need a universal page builder. A focused editing model is welcome. Moving markup into an editable field does not make it structured content.

## Rule 04: Deliver deliberate, consistent design

Applies to: Products with a visible interface.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-04

Visible interfaces must demonstrate coherent typography, hierarchy, spacing, imagery, and interaction design.

- Acceptable: A restrained blog kit with excellent typography and consistent layouts. An expressive design whose visual choices remain coherent across pages and states.
- Not acceptable: A polished homepage paired with unfinished inner pages; clashing component styles; illegible text over images; arbitrary spacing; controls that look interactive but are not.
- Exception or boundary: Minimal and unconventional designs are welcome, and a low price does not count against your product. Make deliberate visual choices and carry them consistently through the whole experience.

## Rule 05: Work beyond the demo’s happy path

Applies to: Products with a visible interface.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-05

Interfaces must work with realistic content, small screens, and keyboard navigation.

- Acceptable: Menus usable by keyboard; labeled forms; visible focus; readable contrast; long titles wrapping correctly; useful empty and error states.
- Not acceptable: A mobile menu that cannot close; hover-only controls; clipped headings; unreadable contrast; missing images breaking layouts; a form showing success without processing anything.
- Exception or boundary: Test the features actually included. Features needing customer credentials may require setup, but must explain that requirement and handle missing configuration.

## Rule 06: Ship an installable, compatible release

Applies to: All products.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-06

Review the release customers receive, using the installation instructions and compatibility claims supplied with it.

- Acceptable: A tagged release installs into a fresh site with the required blueprints, configuration, dependencies, and production assets. Any required build steps are documented and reproducible.
- Not acceptable: A demo works only in the author’s checkout; missing globals or assets; references to local paths; undeclared dependencies; advertised version support that fails installation.
- Exception or boundary: Add-on updates must preserve existing customer content and configuration. Supporting only older Statamic versions is acceptable when those versions are clearly identified and the product works as documented. Beta and experimental releases must be clearly labeled, disclose limitations and breaking changes, and provide reproducible installation instructions, including any development-version constraints. Age or beta status alone is not a rejection reason; neither excuses broken installation, unsafe behavior, or failure to meet other applicable requirements.

## Rule 07: Protect customer sites and data

Applies to: All products.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-07

Use appropriate authorization, validation, escaping, and secure handling of credentials and external services.

- Acceptable: Server-side permission checks; credentials supplied through configuration; documented external requests; failures handled without exposing secrets or destroying data.
- Not acceptable: Committed API keys; unauthorized access to control-panel actions; hidden tracking; silently sending customer content elsewhere; destructive migrations without an explicit, documented migration process.
- Exception or boundary: A clean automated scan does not establish compliance, and marketplace approval is not a comprehensive security audit.

## Rule 08: Have permission to distribute everything included

Applies to: All products.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-08

Bundled code, fonts, imagery, icons, and demo content must have documented redistribution rights and required attribution.

- Acceptable: Original assets or properly licensed third-party materials, with applicable notices included. Demo-only assets clearly identified as excluded from the download.
- Not acceptable: Redistributing assets without permission; assuming a license to use a template also permits reselling its source; removing required attribution.
- Exception or boundary: Redistribution permission does not make a cosmetic reskin eligible under Rule 01.

## Rule 09: Document the product and provide a support path

Applies to: All products.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-09

Customers must be able to install, configure, use, and maintain the product without guessing.

- Acceptable: Accurate installation instructions, a working example, configuration guidance, dependency disclosures, a changelog, and a functioning support channel. Community support is acceptable when clearly stated.
- Not acceptable: Generic boilerplate documentation; instructions for another product; undocumented paid dependencies; dead support links; advertised support that is not provided.
- Exception or boundary: A welcome dashboard widget is a useful extra, not an approval requirement.

## Rule 10: Represent the shipped product honestly

Applies to: All products.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-10

The listing, screenshots, demo, pricing, and compatibility claims must match the submitted release.

- Acceptable: Screenshots from the actual product; clearly stated inclusions and limitations; disclosed paid services; a working starter-kit demo. Add-ons show relevant screenshots or a concrete usage example.
- Not acceptable: Mockups presented as functioning features; demo capabilities absent from the download; hidden subscription requirements; inaccurate compatibility claims; keyword-stuffed or misleading descriptions.
- Exception or boundary: Starter kits require a working live demo. Add-ons without a visual interface do not need an artificial demo site.

## Rule 11: Respect Statamic’s Core and Pro boundaries

Applies to: Add-ons.
Reference: https://statamic.com/marketplace/submission-guidelines#rule-11

Add-ons whose purpose is to bypass or circumvent Statamic’s Core and Pro feature or licensing restrictions are not eligible for the marketplace.

- Acceptable: Extending Core through supported APIs while respecting its edition limits. Requiring Pro for functionality that depends on Pro features. Integrating with an external service without evading Statamic’s restrictions.
- Not acceptable: Unlocking additional users or forms in Core by disabling or working around edition checks. Giving multiple people separate passwords or identities behind a shared Core user to evade the user limit. Disguising multiple forms as one to evade the form limit. Disabling Pro license checks.
- Exception or boundary: This rule concerns products designed to circumvent edition restrictions. An add-on is not in violation merely because it extends Core or has functionality that overlaps with Pro. Reviewers must identify the restriction being bypassed and the mechanism used; using a supported API does not make deliberate circumvention acceptable.

## Practical checks

- Rules 02–03: Trace primary/footer/mobile menus, logos, content images, site settings, collection routes and mounting, blueprints, fieldsets, and shared partials. Confirm editors can manage the promised content without editing templates or HTML fields. Do not force decorative assets into fields or require an unrelated native feature or universal page builder.
- Rules 04–05: Inspect rendered pages and visible add-on interfaces, including inner pages, keyboard navigation, focus, small screens, forms, long text, missing images, and empty/error states. Source inspection alone cannot verify visual polish or interaction behavior. Give specific observations; do not demand fashionable styling.
- Rule 06: Inspect the tagged artifact and starter-kit export manifest, dependency constraints, production build, configuration, and installation hooks. Follow the documented installation in an isolated site when authorized; verify supported versions actually tested and state untested claims. For add-ons, inspect update paths for content/configuration loss. Assess older-version and experimental releases against their declared support and limitations; do not invent a latest-major requirement or a blanket beta ban.
- Rule 07: Trace server-side authorization, validation, escaping, credentials, external data flows, and migrations. Inspect failure behavior and protect customer data. A clean scanner result is not a complete security review.
- Rules 08–10: Check redistribution evidence, notices, installation/configuration instructions, a working usage example, changelog, support route, price/dependency disclosures, screenshots, and demo against the shipped release. Starter-kit demos must work; nonvisual add-ons can provide a concrete usage example. Flag inaccessible resources as unverified rather than inventing their contents.

- Rule 11: Inspect edition/license checks, authentication, user identities, and form handling when the add-on’s purpose or implementation suggests circumvention. Cite the specific Core/Pro restriction and the code or documented behavior that bypasses it. Do not infer a violation from overlapping features alone, and do not disable licensing or edition checks to test it. Identify a product built around circumvention as an eligibility concern for human review, not an automatic rejection.

## Findings and review outcomes

Every required finding must include:

- Rule number, title, and public anchor link.
- Evidence: file and line, rendered screen, reproduction steps, or comparison source; identify the release/commit where relevant.
- Impact on a customer, editor, developer, or marketplace visitor.
- Required change and how to verify it.
- Whether the issue is a repairable shortcoming or evidence that substantial rework is needed. Uncertain eligibility judgments require human review.

Use “Changes required” for concrete issues addressable within the product. Use “Not eligible in its current form” only as a recommendation for human review supported by evidence of a fundamental problem, such as a cosmetic clone requiring substantial differentiation. Do not imply cosmetic fixes will resolve a fundamental originality issue. Never automatically reject a product or grant approval.

Example repairable finding: Rule 02 — the primary navigation and footer contact details are hard-coded. Move them into suitable Statamic content structures and verify an editor can change them without template edits.

Example fundamental finding: Rule 01 — identified comparison evidence shows the same layouts and content model as the creator’s existing kit, with only colors and photographs changed. These changes belong in the existing product; substantial differentiation is needed before reconsideration.

Separate required fixes, uncertain findings, and optional improvements. A welcome dashboard widget is optional. No numerical score, authorship detector, or guarantee of approval. Fixing findings triggers another review, not automatic acceptance.

## Creator-facing response

Write a short, friendly review that helps the creator decide what to do next. Use plain language and a supportive, proportionate tone. Keep the review thorough underneath; do not turn its output into a compliance checklist. Aim for roughly 200–400 words for a straightforward product, expanding only when actionable findings need more explanation.

Follow this flow, adapting it to the findings:

1. **Start with the overall impression.** If the evidence supports it, say “[Product] looks thoughtfully built” or “This looks in good shape,” followed by one or two specific strengths. If a significant problem exists, explain it plainly instead of offering false reassurance. Scope source-only impressions accordingly.
2. **Explain what to fix or check next.** Lead with the most important action, using a descriptive title such as “Make sure previews cannot expose unpublished content.” Explain the observed behavior, why it matters, and what to do. Include a concise evidence link and the relevant rule link here, rather than leading with policy terminology. Required fixes still need the evidence and verification described above; weave these into readable prose instead of repeating labeled fields. For an uncertain concern, say it is unconfirmed and give a concrete way to check it before recommending a conditional fix.
3. **Offer a few practical finishing checks when needed.** For example, install the release in a fresh site using its documentation, walk through the main editing experience, or compare the listing with the shipped features. Choose checks that address actual gaps in this review. Do not repeat completed checks or invent homework for every rule. Keep optional improvements clearly optional.
4. **Close with a brief scope note.** Name the reviewed release or commit and summarize what was actually checked and any material limits, such as an installation or interface that could not be tested. Mention an unavailable live policy or version mismatch briefly when relevant. Do not list every unverified rule. Never imply runtime checks passed when only source was inspected.

Avoid rule-by-rule tables, scores, “remaining verification” matrices, repeated approval disclaimers, and formal verdicts for ordinary follow-up checks. Do not make originality, licensing, or usability sound suspect simply because exhaustive proof was unavailable. Preserve concrete concerns and important limitations without presenting uncertainty as a defect. A positive assessment is welcome; a guarantee of marketplace approval is not.

Example tone and flow (illustrative, not a finding to reuse):

> **This add-on looks thoughtfully built.** From the source I reviewed, it integrates naturally with Statamic and gives editors clear controls.
>
> There’s one thing I’d check before submitting: **make sure previews cannot expose unpublished content.** The preview handler loads entries by ID, and I didn’t see a publication check. There may be protection elsewhere, so this is not a confirmed bug. [Link the inspected code here.]
>
> Try opening a draft’s preview while logged out. If it reveals unpublished content, protect that endpoint and add a regression test before submitting. This relates to [Rule 07 — Protect customer sites and data](https://statamic.com/marketplace/submission-guidelines#rule-07).
>
> After that, install the release in a fresh site using your documentation and walk through the main editing features.
>
> **Overall, this looks in good shape.** I reviewed the tagged source, but did not run the product. Installation and interface behavior still need a hands-on check.
