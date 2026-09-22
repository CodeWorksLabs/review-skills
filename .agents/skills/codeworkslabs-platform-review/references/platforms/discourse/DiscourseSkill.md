---
name: discourse-extension-review
description: Review Discourse plugins, themes, and theme components for supported integration, correctness, security, compatibility, lifecycle safety, accessibility, documentation, and release readiness. Use for static audits, integrated verification, or release review of a Discourse extension.
metadata:
  ruleset-version: 0.1.1
  structured-core: DiscourseSkill.json
---

# Discourse Extension Review

Review the Discourse extension against the rules in this skill and the complete structured core in `DiscourseSkill.json`. The Markdown and JSON are one active platform package; neither may be replaced by a summary.

The goal is to determine whether the plugin is a well-behaved Discourse extension that an administrator can install, configure, update, operate, and remove without unreasonable risk to the forum or its data.

This is an evidence-based engineering review.

Do not approve a plugin merely because its tests pass, its code looks conventional, an automated scanner is clean, or it works on the author's development instance.

Do not reject a plugin because it uses AI-generated code, is small, is experimental, or supports only a limited range of Discourse versions.

Evaluate the product that actually ships.

## Review principles

For every finding:

1. Cite the exact file and line, class, method, route, setting, migration, test, or observable behavior that supports the finding.
2. Explain the concrete effect on a Discourse site.
3. Identify the applicable numbered rule.
4. Distinguish a required correction from an optional improvement.
5. Do not speculate where evidence is missing.
6. Mark anything you could not verify as `Not verified`.
7. Prefer reproducible evidence over stylistic preference.

Do not modify the plugin unless explicitly asked to fix findings.

Do not claim that this review constitutes approval by Discourse, Discourse.org, CDCK, a marketplace, a hosting provider, or any other organization.

Do not describe this review as a comprehensive security audit.

# Review scope

Inspect, when present:

- `plugin.rb`
- `README.md`
- `LICENSE`
- `CHANGELOG.md` or equivalent release history
- `config/settings.yml`
- `config/locales/`
- `app/`
- `lib/`
- `db/migrate/`
- `jobs/`
- `services/`
- `serializers/`
- `controllers/`
- `models/`
- `assets/javascripts/`
- `assets/stylesheets/`
- `admin/`
- `test/`
- `spec/`
- `package.json`
- lockfiles
- CI workflows
- Docker or installation scripts
- external-service integrations
- generated assets included in the release
- the exact tagged/archive release when available

Also inspect plugin dependencies and any documented minimum or maximum Discourse version.

If reviewing a working tree, identify untracked files relevant to the plugin before declaring the review complete.

# Version coverage and isolated installations

For release readiness, select targets from Discourse's current official support data and test the exact candidate in an independently identified installation or isolated container for every materially distinct release line the extension claims to support.

The September 2026 matrix that established this method was:

1. **Current development head — Discourse `main`.** Tests forward compatibility against an exact commit from Discourse's active development branch. This can reveal upcoming breakage but does not represent a released production version.
2. **Current monthly release — Discourse 2026.9.** Tests the newest supported production release line against an exact `release/2026.9` commit or release tag.
3. **Previous supported monthly release — Discourse 2026.8.** Tests compatibility with the immediately preceding monthly release while it remains within Discourse's published support window.
4. **Maintained ESR coverage — Discourse 2026.7.** Tests every materially distinct 2026.7 ESR target the extension claims to support, using exact maintained branch, tag, patch, or compatibility-target identities. ESR coverage must not be inferred from success on `main` or a newer monthly release.

Treat those numbers as the dated example, not a permanent list. Before each review, refresh the actual target versions and support status from Discourse's authoritative release data.

For every target:

- use an independently identified installation or isolated container;
- install or mount the same exact candidate artifact;
- record the Discourse branch, commit, release identity, extension identity, toolchain, commands, environment, and complete results;
- do not infer compatibility for one release line from another.

Use a separate clean-install and lifecycle environment when those claims are in scope. Use a staging-like environment for native update, tag pinning, rollback or recovery, and return-to-current verification. If a claimed release line is not exercised, narrow the compatibility claim or mark it `Not verified`.

For the recommended five-slot local topology, isolation rules, candidate handling, evidence manifest, resource model, and lifecycle sequence, read [LOCAL_TEST_MATRIX.md](LOCAL_TEST_MATRIX.md) when integrated or release-readiness verification is authorized.

# 01 — Provide a clear and legitimate Discourse capability

The plugin should add a coherent capability, integration, administrative workflow, or user experience.

Its purpose must be identifiable from the shipped code and documentation.

## Acceptable

- Integrating Discourse with an external publishing platform.
- Adding moderation or administrative workflows.
- Extending topic, post, category, user, group, notification, search, or authentication behavior for a defined use case.
- Providing a substantial UI or workflow that cannot reasonably be represented as a theme-only customization.

## Requires attention

- A plugin whose advertised functionality is largely absent from the release.
- Multiple nominally different plugins that contain effectively the same implementation with superficial branding changes.
- A plugin whose primary purpose could be fulfilled entirely through documented configuration but instead patches core behavior unnecessarily.
- Functionality unrelated to the stated purpose that materially expands privilege, data collection, or attack surface.

Do not require complexity for its own sake. A narrow plugin can be excellent.

# 02 — Integrate through supported Discourse extension points

The plugin must behave as a Discourse plugin rather than as a private fork of Discourse.

Prefer supported plugin APIs, plugin registration mechanisms, serializers, callbacks, event hooks, outlets, service APIs, site settings, and other documented extension points.

## Acceptable

- A conventional `plugin.rb` manifest and initializer.
- Supported server-side plugin APIs.
- Supported JavaScript plugin APIs and API initializers.
- Plugin-owned models, services, jobs, controllers, serializers, and migrations.
- Explicitly registered assets and functionality.
- Carefully scoped reopenings or extensions where Discourse provides no appropriate higher-level API and compatibility is handled deliberately.

## Required correction

- Modifying files in Discourse core as part of normal installation.
- Requiring administrators to patch core files manually.
- Monkey patches that silently replace substantial core behavior without necessity or compatibility safeguards.
- Depending on undocumented implementation details when a supported API exists.
- Copying a core component into the plugin and allowing it to drift solely to change a small behavior that has a supported extension mechanism.

When lower-level integration is genuinely necessary, verify that the reason is documented and covered by compatibility tests.

# 03 — Respect Discourse's data model and lifecycle

Plugin-owned data must integrate safely with Discourse's Rails application and lifecycle.

Review:

- ActiveRecord models
- associations
- validations
- callbacks
- custom fields
- plugin stores
- uploads
- topic/post/category/user relationships
- deletion behavior
- anonymization implications
- multisite behavior where applicable
- backup and restore behavior where applicable

## Required correction

Flag demonstrated cases such as:

- orphaned records created by normal deletion flows;
- destructive callbacks with unintended scope;
- IDs or relationships assumed to exist without validation;
- global state used where site-specific state is required;
- plugin data stored in ephemeral filesystem locations without documentation;
- direct database manipulation that bypasses necessary application invariants;
- user-generated data that cannot be associated with its owning site or principal when that relationship matters.

Do not require a database table merely because one could be used. Discourse-supported custom fields or plugin stores may be appropriate for small amounts of data.

# 04 — Make migrations safe and reversible in practice

Database migrations receive heightened scrutiny because they execute during deployment and can affect the entire forum.

Inspect every migration.

Verify:

- new tables and indexes are sensibly scoped;
- large-table operations consider production impact;
- migrations do not assume an empty site;
- migrations tolerate realistic existing data;
- data transformations are deliberate;
- destructive changes have an upgrade strategy;
- uniqueness constraints match application behavior;
- rollback assumptions are realistic;
- migrations do not depend on application code that may later change incompatibly.

## Required correction

Examples include:

- dropping populated columns or tables without an explicit migration strategy;
- rewriting large core tables synchronously without considering deployment impact;
- unbounded data migrations likely to lock or exhaust a production database;
- creating inconsistent records when rerun or partially completed;
- migration logic dependent on external APIs;
- silently deleting user or plugin data during an ordinary update.

A migration need not be technically reversible if reversing it would be unsafe or meaningless, but irreversible behavior must be deliberate and appropriately documented.

# 05 — Enforce authorization on the server

Never rely on hidden UI, JavaScript checks, or route visibility as authorization.

For every privileged operation, identify:

- the authenticated principal;
- the required permission;
- where the server enforces that permission;
- the affected resource;
- whether resource ownership or site role is checked.

Pay particular attention to:

- admin routes;
- moderator actions;
- group-restricted actions;
- category-restricted operations;
- API endpoints;
- bulk operations;
- background jobs initiated by users;
- webhook configuration;
- secret rotation;
- external publication or synchronization actions.

## Required correction

- An admin-looking endpoint without an admin server-side check.
- A moderator action callable by ordinary users.
- An object fetched by user-supplied ID without verifying access to that object.
- Authorization performed only in Ember code.
- A background job accepting an untrusted identifier and performing privileged work without rechecking its authority.

# 06 — Validate inputs and encode outputs appropriately

Treat parameters, uploaded files, imported data, remote responses, webhook bodies, rendered HTML, Markdown-derived content, and stored external content according to their trust boundary.

Review for:

- parameter validation;
- strong parameters or equivalent filtering;
- URL validation;
- path handling;
- HTML safety;
- SQL construction;
- shell invocation;
- SSRF exposure;
- deserialization;
- file uploads;
- MIME assumptions;
- external identifiers;
- pagination and resource bounds.

## Required correction

Examples include:

- interpolating user input into SQL;
- passing untrusted input to a shell;
- marking untrusted HTML safe without sanitization;
- arbitrary server-side URL fetching without an appropriate trust model;
- constructing filesystem paths from untrusted values without containment;
- accepting a remote payload as authoritative without validating the expected schema.

Report the concrete exploitable or correctness path. Do not flag generic keywords without context.

# 07 — Handle credentials and external services safely

Plugins that communicate with another service must make that relationship explicit.

Review:

- API tokens;
- webhook secrets;
- OAuth credentials;
- connection secrets;
- signing keys;
- administrator-supplied URLs;
- outbound requests;
- inbound webhook authentication;
- retry policy;
- timeout behavior;
- logging;
- secret rotation;
- failure modes.

## Acceptable

- Secrets entered through an appropriate administrative/configuration mechanism.
- Environment-backed secrets where appropriate.
- Credentials excluded from source control.
- Signed or authenticated inbound requests.
- Bounded network timeouts.
- Errors that preserve diagnostic value without exposing credentials.

## Required correction

- Hard-coded production credentials.
- Tokens committed to the repository.
- Secrets returned through ordinary serializers or rendered into pages.
- Full authorization headers or secret values written to logs.
- Unauthenticated inbound operations capable of changing site state.
- External calls without reasonable timeouts.
- Silent transmission of forum or user data unrelated to the documented feature.

Document what data leaves the Discourse instance and why.

# 08 — Preserve privacy and administrator control

A plugin should not unexpectedly expand the audience for private Discourse data.

Review behavior involving:

- private messages;
- staff-only content;
- secure categories;
- group-restricted topics;
- deleted or hidden content;
- email addresses;
- IP addresses;
- user profile fields;
- authentication data;
- API keys;
- uploaded files;
- logs;
- analytics;
- third-party services.

## Required correction

- Sending private content to a third party without the feature requiring it and without administrator awareness.
- Publishing restricted category content through a public integration.
- Leaking staff-only fields through serializers.
- Tracking users through a third party without disclosure where disclosure is appropriate.
- Retaining secrets or sensitive payloads in ordinary diagnostic logs.

For content bridges and syndication plugins, explicitly trace the authorization boundary between source content and every destination.

# 09 — Use background work appropriately

Potentially slow, retryable, scheduled, or external work should not unnecessarily block web requests.

Inspect Sidekiq jobs, scheduled jobs, event-driven jobs, and external synchronization flows.

Verify:

- jobs are idempotent where retries are possible;
- repeated delivery does not corrupt state;
- retry behavior is bounded or deliberate;
- jobs do not silently swallow permanent failures;
- locks or leases do not create permanent dead states;
- external work has timeouts;
- jobs operate on the correct site in multisite environments;
- enqueueing cannot be abused to create unbounded work.

## Required correction

Examples include:

- a request waiting indefinitely on an external service;
- duplicate retries creating duplicate remote objects;
- jobs that assume a record still exists;
- a failed lease or lock that permanently prevents later processing;
- retry loops with no meaningful bound or backoff;
- remote state considered committed before the local transaction is durable, when this can create inconsistency.

# 10 — Make synchronization and distributed operations recoverable

Apply this rule when the plugin synchronizes Discourse with another system.

Treat cross-system publication as a distributed transaction even if no formal transaction protocol is used.

Review:

- idempotency keys;
- revisions;
- acknowledgement state;
- retry semantics;
- partial success;
- stale claims;
- leases;
- conflict handling;
- deletion;
- re-publication;
- credential failures;
- remote outages;
- rollback or reconciliation.

A network call succeeding does not prove that the whole workflow succeeded.

## Required correction

Flag demonstrated states where:

- a crash can permanently lose pending work;
- retries create duplicate remote resources;
- local state records success before the remote operation is durable;
- remote success can occur but never be acknowledged or reconciled locally;
- stale leases cannot recover;
- a failed publication destroys the previously valid representation;
- deletion in one system unpredictably destroys unrelated data in another.

Require an explicit recovery path for realistic partial failures.

# 11 — Build administrator-facing features as native Discourse administration

If the plugin exposes settings or controls to administrators, they should behave like part of Discourse rather than an unrelated embedded application.

Review:

- setting names and descriptions;
- grouping;
- validation;
- enable/disable behavior;
- admin routes;
- loading states;
- success and error feedback;
- destructive-action confirmation;
- accessibility;
- translation;
- responsiveness.

## Required correction

Examples include:

- controls that report success when the server rejected the action;
- critical configuration stored only in browser-local state;
- untranslated user-facing strings where localization is expected;
- destructive operations without adequate confirmation;
- settings that appear to disable the plugin while background behavior continues unexpectedly.

A plugin does not need an admin UI when configuration genuinely belongs elsewhere.

# 12 — Maintain coherent user-facing behavior

For plugins that alter the public or authenticated user interface, test more than the ideal screenshot.

Verify relevant states:

- desktop;
- narrow/mobile viewport;
- keyboard navigation;
- focus behavior;
- long titles or usernames;
- empty state;
- loading state;
- permission denied;
- network failure;
- deleted content;
- missing images or optional fields;
- disabled plugin setting;
- anonymous versus authenticated use.

Visible behavior should fit reasonably within Discourse's existing interaction model unless departure is intentional.

# 13 — Avoid fragile frontend integration

Use current supported Discourse frontend extension mechanisms.

Review:

- API initializers;
- plugin outlets;
- registered transformers or APIs;
- Ember components;
- Glimmer components;
- services;
- route extensions;
- admin frontend code;
- deprecated APIs;
- DOM mutation.

## Required correction

Examples include:

- relying on generated CSS class names as an application API;
- global DOM polling when a plugin API or outlet exists;
- direct mutation of another component's internal DOM structure where a supported API exists;
- using removed or deprecated APIs while claiming support for current Discourse;
- leaking event listeners or timers across route transitions.

Direct DOM work is not automatically wrong. Flag it only where it produces a concrete compatibility or lifecycle risk.

# 14 — Make site settings complete and safe

Inspect `config/settings.yml` and every setting consumer.

Verify:

- defaults are safe;
- names are clear;
- setting types match usage;
- secrets are not exposed through inappropriate settings mechanisms;
- disabled-state behavior is coherent;
- setting changes take effect as documented;
- required settings are validated before performing irreversible or external work.

A plugin-wide enable setting should prevent the plugin's substantive behavior when disabled unless the exception is deliberate and documented.

# 15 — Keep API contracts explicit

For plugin HTTP APIs, webhooks, or external adapter APIs, review the contract as a product surface.

Verify:

- versioning strategy where compatibility matters;
- authentication;
- request schema;
- response schema;
- error format;
- pagination;
- idempotency;
- content type;
- rate/abuse considerations;
- backward compatibility;
- deprecation behavior.

## Required correction

Examples include:

- an endpoint advertised to external consumers whose response shape changes incidentally with an internal serializer;
- returning sensitive model attributes because the complete model was serialized by convenience;
- ambiguous success responses for partially completed operations;
- undocumented destructive behavior.

# 16 — Test the behaviors that can break customer sites

Automated tests should correspond to the plugin's actual risk.

Check for relevant:

- model specs;
- service specs;
- request/controller specs;
- authorization tests;
- job tests;
- migration tests;
- serializer tests;
- frontend acceptance tests;
- admin tests;
- external-service tests using controlled fakes;
- failure-path tests;
- upgrade/regression tests.

Tests should cover consequential negative paths, not only successful creation.

High-risk behavior without meaningful regression tests is a release-readiness concern even when no present bug has been demonstrated.

Distinguish:

- `Defect`: an incorrect behavior demonstrated by evidence.
- `Test gap`: important behavior lacks reasonable automated coverage.

Do not report a test gap as proof that the implementation is broken.

# 17 — Pass the standard Discourse plugin quality checks

When the repository is compatible with the current Discourse plugin tooling, run the checks provided by the plugin itself and the standard Discourse plugin workflow where practical.

Review, where present:

- Ruby tests/specs;
- frontend tests;
- JavaScript/TypeScript lint;
- template/Glimmer checks;
- CSS/SCSS lint;
- formatting;
- type checking;
- plugin CI workflow.

Do not substitute lint for behavioral testing.

If a standard check cannot run because the repository intentionally supports an older Discourse generation, record the supported version and use the matching toolchain where feasible.

# 18 — Ship an installable release

Review the actual release artifact or tagged commit whenever possible.

Verify installation according to the documented instructions.

Check:

- the plugin directory is self-contained;
- `plugin.rb` metadata is accurate;
- dependencies are declared;
- required assets exist;
- production does not depend on the author's local checkout;
- development-only symlinks are absent from the shipped artifact;
- build steps are reproducible;
- required settings are documented;
- restart/rebuild requirements are documented;
- supported Discourse versions are stated honestly.

## Required correction

- absolute local paths;
- references to unpublished local packages;
- missing generated assets required in production;
- undeclared runtime dependencies;
- installation instructions that do not install the submitted release;
- a tagged release whose bytes differ materially from the reviewed source without explanation.

# 19 — Make upgrades safe

A plugin update must preserve the site's valid existing state unless a breaking change is deliberately documented and supported by an explicit migration path.

Test representative upgrades where the plugin stores meaningful data.

Review:

- database migrations;
- renamed settings;
- renamed classes or identifiers;
- serialized data;
- plugin-store keys;
- custom-field names;
- external API revisions;
- background work already in flight;
- removed features;
- changed permissions.

## Required correction

- an update silently loses configuration;
- stored records become unreadable without migration;
- in-flight jobs become permanently invalid;
- a renamed setting resets security-sensitive behavior unexpectedly;
- the plugin requires administrators to delete existing plugin data merely to upgrade normally.

Experimental software may make breaking changes, but those changes still need to be intentional and documented.

# 20 — Handle disablement and removal predictably

Determine what happens when the plugin is disabled or removed.

Disabling the plugin should not leave unexpected active behavior.

Review:

- scheduled jobs;
- external callbacks;
- webhooks;
- routes;
- assets;
- plugin records;
- user-visible remnants;
- remote integrations.

Do not require uninstall to delete user data automatically. Preserving data is often safer.

If permanent cleanup is provided, destructive cleanup must be explicit.

# 21 — Maintain compatibility deliberately

Discourse changes continuously.

The plugin must make a support claim that can be understood and tested.

Look for:

- minimum supported Discourse version;
- tests against an appropriate branch or version;
- deprecated API usage;
- compatibility shims;
- version guards;
- frontend API compatibility;
- Ruby/Rails assumptions;
- database assumptions.

Do not require support for all Discourse versions.

A narrow support window is acceptable when it is clearly stated.

Do not accept a broad compatibility claim solely because installation succeeds.

# 22 — Declare and constrain dependencies

Review Ruby, JavaScript, system, and service dependencies.

Verify:

- they are actually required;
- their licenses permit distribution/use;
- production dependencies are distinguished from development dependencies;
- versions are constrained appropriately;
- abandoned or unusually privileged dependencies receive appropriate scrutiny;
- external SaaS requirements are disclosed.

Do not require exact pinning of every dependency. Evaluate whether the constraint strategy provides reproducible and maintainable behavior.

# 23 — Respect Discourse security boundaries

A plugin must not deliberately bypass security controls provided by Discourse.

Scrutinize behavior involving:

- staff permissions;
- category security;
- secure uploads;
- authentication;
- API scopes;
- user impersonation;
- rate limits;
- CSRF protection;
- content visibility;
- deleted content;
- trust-level restrictions.

## Required correction

Examples include:

- making staff-only information public;
- bypassing category permissions to simplify an integration;
- disabling CSRF checks without an appropriate alternative authentication boundary;
- granting admin-equivalent capability to an ordinary authenticated user;
- exposing protected uploads through a public proxy endpoint.

Overlapping with a built-in Discourse feature is not itself a problem.

# 24 — Do not conceal operational behavior

Administrators should be able to understand significant behavior caused by the plugin.

Document, where applicable:

- external destinations;
- scheduled processing;
- data retention;
- destructive actions;
- API/webhook requirements;
- expected network access;
- generated users or groups;
- database growth;
- logging;
- backup considerations;
- required infrastructure.

Hidden telemetry, undocumented outbound publication, or unexpected modification of forum state is a release blocker.

# 25 — Provide useful documentation and a support path

A production administrator should not have to reverse-engineer the plugin to operate it.

Documentation should cover what is relevant:

- purpose;
- supported Discourse versions;
- installation;
- upgrade;
- configuration;
- required permissions;
- external service setup;
- security model;
- normal operation;
- troubleshooting;
- backup/recovery considerations;
- removal/disablement;
- known limitations;
- breaking changes;
- support channel.

Code comments do not replace operator documentation.

# 26 — Represent the plugin honestly

Documentation, screenshots, topic listings, demos, and release notes must describe the shipped release.

## Required correction

- screenshots of features absent from the release;
- claiming compatibility that was not implemented;
- calling an experimental integration production-ready without describing known constraints;
- failing to disclose a required paid third-party service;
- describing mock UI as completed functionality;
- claiming that an external system remains synchronized when synchronization is only one-way.

# 27 — Have rights to distribute the release

Inspect licenses and included third-party assets where material.

The plugin should have the right to distribute:

- source code;
- copied libraries;
- icons;
- fonts;
- images;
- fixtures;
- demo content;
- generated bundles that contain third-party work.

Required notices must remain intact.

Do not treat the presence of third-party code as a problem by itself.

# 28 — Keep repository and release hygiene appropriate

Check for accidentally shipped development material such as:

- credentials;
- `.env` files;
- database dumps;
- production logs;
- private certificates;
- local absolute paths;
- editor swap files;
- temporary archives;
- test secrets that are actually live;
- customer data;
- large unrelated binaries.

Example and fixture credentials are acceptable when clearly nonfunctional and scoped for testing.

# 29 — Treat experimental and pre-release plugins honestly

Alpha, beta, preview, and experimental plugins are reviewable.

Pre-release status is not itself a defect.

Verify that:

- the release is clearly labeled;
- known limitations are disclosed;
- installation is reproducible;
- migration and data-safety behavior is still responsible;
- breaking-change expectations are stated;
- production suitability is not overstated.

Experimental status never excuses credential exposure, authorization failures, destructive updates, or inability to recover from foreseeable partial failures.

# 30 — Review removal of obsolete compatibility code

Compatibility code can become a source of hidden defects.

When a plugin supports multiple generations of Discourse, determine whether version branches and fallback paths are still reachable and tested.

Do not require immediate removal solely because code is old.

Flag compatibility code when it:

- invokes APIs absent from every claimed supported version;
- changes security behavior inconsistently;
- masks failures;
- prevents current behavior from being tested;
- preserves an obsolete data representation with no migration strategy.

# Discourse-specific high-risk review

Apply a deeper pass when the plugin contains any of the following:

- authentication or SSO;
- admin impersonation;
- publishing/syndication;
- inbound webhooks;
- outbound webhooks;
- private-message processing;
- secure-category access;
- background synchronization;
- remote command execution;
- shell execution;
- arbitrary URL fetching;
- upload processing;
- payment functionality;
- user provisioning;
- automated moderation;
- deletion or archival;
- large data migrations;
- direct database SQL;
- encryption or secret management.

For these areas, trace the complete flow rather than reviewing isolated functions.

# External publication checklist

For a plugin that publishes Discourse content to another platform, explicitly answer:

1. Which Discourse content is eligible?
2. Who enables publication?
3. Which permissions are checked before content becomes eligible?
4. Can private or staff content ever enter the publication queue?
5. What immutable or revisioned identity identifies the source content?
6. What identifies the destination resource?
7. Is publication idempotent?
8. What happens after a timeout with an unknown remote result?
9. What happens after remote success and local failure?
10. What happens after local success and remote failure?
11. How are stale claims or leases recovered?
12. How is deletion represented?
13. How is a previously published item disabled?
14. Can credentials be rotated without losing work?
15. Can a destination be disabled without affecting other destinations?
16. How is an incompatible adapter version handled?
17. How is a partially completed deployment reconciled?
18. Are publication revisions observable to an operator?
19. Can an administrator retry or recover without editing the database?
20. Does an external build/deploy step preserve the same transaction boundary?

If any answer depends on undocumented assumptions, record that explicitly.

# Suggested mechanical review

Use the repository's own commands first.

Where applicable, run:

```text
git status --short
git diff --check
```

Then use the plugin's documented test and lint commands.

If the plugin follows the current Discourse plugin skeleton, inspect its package scripts and CI workflow rather than inventing substitute commands.

Also search deliberately for high-risk constructs. Example categories:

```text
credentials and secrets
shell/process execution
raw SQL
HTML-safe rendering
skip_before_action / disabled CSRF
external HTTP
File / IO / Pathname
eval / instance_eval / class_eval
deserialize / YAML load
admin-only routes
guardian checks
scheduled jobs
migrations
plugin store
custom fields
secure uploads
user and category serializers
```

A grep match is an investigation lead, not a finding.

# Release verification

When release readiness is part of the request, verify the exact release candidate.

Record:

- commit;
- tag;
- plugin version;
- archive hash when available;
- declared Discourse compatibility;
- test commands executed;
- test results;
- checks not executed;
- environment limitations;
- outstanding required findings.

Prefer testing installation from the same tagged/archive artifact that users receive.

# Finding severity

Use severity to communicate operational impact, not drama.

## Critical

Use for demonstrated behavior likely to allow severe site compromise, secret compromise, broad unauthorized access, or destructive loss affecting production data.

## High

Use for significant authorization failures, exposure of private content, dangerous migration behavior, serious secret handling defects, or synchronization defects capable of substantial persistent corruption.

## Medium

Use for concrete correctness, compatibility, recoverability, privacy, accessibility, or operational problems that materially affect normal installations but do not meet High severity.

## Low

Use for limited-scope defects with a real but modest operational effect.

## Info

Use for non-blocking observations, documentation gaps of minor consequence, maintainability notes, or optional hardening.

Do not inflate severity because a finding appears security-related.

# Confidence

For each finding, use:

- `High`: directly demonstrated in code, tests, or runtime behavior.
- `Medium`: strongly supported but an important runtime condition has not been verified.
- `Low`: plausible concern requiring verification.

Do not present Low-confidence speculation as a required correction unless the uncertainty itself is the defect.

# Required review output

Produce the report in this order.

## 1. Review scope

Include:

- plugin name;
- plugin version;
- commit/tag if known;
- Discourse versions claimed;
- files or artifact reviewed;
- commands actually executed;
- important areas not tested.

## 2. Summary

State:

- number of Critical findings;
- number of High findings;
- number of Medium findings;
- number of Low findings;
- number of Info findings;
- number of unverified material concerns.

Do not issue marketplace approval.

## 3. Required findings

For each:

```text
### [Severity] Rule NN — Short finding title

Evidence:
- path/to/file.rb:123
- path/to/spec.rb:45

Observed:
Describe exactly what the implementation does.

Impact:
Describe the concrete consequence to a Discourse installation.

Required change:
State what property must be corrected. When useful, suggest a compatible implementation direction without unnecessarily prescribing one exact design.

Verification:
State how the correction should be tested.

Confidence:
High | Medium | Low
```

Order findings by severity, then by rule number.

## 4. Test and verification gaps

List material behaviors you could not establish.

Do not turn absence of evidence into a defect automatically.

## 5. Optional improvements

Keep non-blocking recommendations separate from required findings.

## 6. Rule matrix

Report each applicable rule as:

- `Pass`
- `Finding`
- `Not verified`
- `Not applicable`

Example:

```text
01 Clear capability — Pass
02 Native integration — Pass
03 Data lifecycle — Pass
04 Migration safety — Not applicable
05 Server authorization — Finding
...
```

A `Pass` means the reviewed evidence did not reveal a violation within the inspected scope. It does not guarantee absence of defects.

# Review outcome language

Use factual outcome language only.

Good:

- `No required findings were identified in the reviewed scope.`
- `Three required corrections were identified.`
- `Release readiness remains unverified because upgrade testing was not performed.`
- `The plugin passed the repository's automated test suite in the tested environment.`

Do not say:

- `Discourse approved`
- `Marketplace approved`
- `Officially safe`
- `Secure`
- `Production certified`
- `Guaranteed compatible`

# After fixes

When asked to review a corrected version:

1. Recheck every previous finding against the new code.
2. Verify the regression test where appropriate.
3. Check whether the correction introduced adjacent defects.
4. Rerun affected test/lint suites.
5. Do not mark a finding resolved solely because its original lines changed.
6. Preserve a short resolution note mapping the old finding to the evidence that now resolves it.

# Authoritative references

When current Discourse behavior is material to a finding, consult current official Discourse documentation and source rather than relying only on remembered framework conventions.

Useful authoritative sources include:

- Discourse core documentation.
- The Discourse core repository.
- The official Discourse plugin skeleton.
- Current Plugin API documentation/source.
- Official Meta Discourse developer documentation.
- Official examples maintained by Discourse.
- Discourse's current `versions.json` support data.
- Official release-channel documentation and `release/YYYY.M` branches.
- Official `d-compat/YYYY.M` plugin and theme compatibility guidance.

Prefer the behavior of the Discourse version actually claimed by the plugin when that differs from current `main`.

# Final constraint

This skill assists with technical review.

It does not:

- submit a plugin;
- grant marketplace or community approval;
- certify security;
- establish legal compliance;
- establish license ownership;
- replace human review;
- prove compatibility with versions that were not tested.

Anything important that was not tested must remain clearly marked as unverified.
