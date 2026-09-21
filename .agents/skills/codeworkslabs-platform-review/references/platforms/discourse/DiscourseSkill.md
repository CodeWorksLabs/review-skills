# Discourse extension review

Status: CodeWorksLabs-maintained platform guidance. It is not an official Discourse or CDCK policy and grants no approval.

Use this reference for Discourse plugins, themes, theme components, mixed extensions, and integration repositories. Apply it through the CodeWorksLabs wrapper rather than as an independent disposition system.

## Classify the extension

Identify the target before applying checks:

- Rails plugin;
- theme;
- theme component;
- plugin containing substantial theme assets;
- integration repository;
- exact release artifact; or
- development branch or working tree.

Mixed repositories require every applicable profile. Do not force plugin-only requirements onto theme components or ignore frontend lifecycle because a Rails plugin owns the entrypoint.

## Shared Discourse expectations

The extension should provide a coherent capability and use supported Discourse extension mechanisms. A narrow product is acceptable. Overlap with Core is not itself a defect.

Inspect:

- accurate metadata, enablement settings, compatibility declarations, dependencies, licenses, release artifacts, installation and support guidance;
- input validation, URL and protocol restrictions, output escaping, imported configuration bounds, unknown keys, and denial-of-service limits;
- privacy, secure-category and protected-upload behavior, administrator control, outbound data, telemetry, retention, logging, and operational transparency;
- user-facing feedback, errors, empty states, keyboard operation, focus, screen readers, responsive layouts, RTL, color schemes, and reduced motion where applicable;
- current supported APIs and deliberate compatibility branches rather than direct Core modification or brittle undocumented internals;
- exact release identity, generated assets, repository hygiene, prerelease labeling, demos, screenshots, compatibility claims, and distribution rights.

Do not infer a defect merely because code is AI-assisted, minimal, unconventional, supports a narrow version range, or uses an older version it explicitly supports.

## Plugin profile

For a Rails plugin, trace material flows across routes, controllers, Guardian or equivalent authorization, serializers, models, queries, custom fields, plugin stores, jobs, webhooks, migrations, settings, and frontend consumers.

Verify proportionately:

- every privileged route enforces authorization server-side;
- CSRF, API authentication, rate limits, user impersonation, trust levels, category security, private messages, deleted content, and uploads preserve Discourse boundaries;
- migrations are bounded, safe on populated databases, compatible with rolling operation where claimed, and paired with an honest recovery or rollback boundary;
- persistence choices fit the data, preserve identities, constrain queries and pagination, and do not rely on unsafe raw SQL or unbounded loading;
- Sidekiq and scheduled work are idempotent, retryable, observable, and safe across restart, disablement, upgrade, and partial completion;
- credentials remain server-side, redacted, rotatable, scoped, and absent from client settings, logs, reports, artifacts, and URLs;
- disablement stops active behavior; removal and retained data are predictable and documented;
- multisite behavior is deliberate when the plugin can run in multisite installations.

## Theme and theme-component profile

For themes and theme components, inspect supported Plugin API methods, outlets, connectors, modifiers, initializers, settings and object schemas, templates, styles, assets, uploads, icons, and component lifecycle.

Verify proportionately:

- setup and teardown clean up listeners, observers, subscriptions, timers, and DOM state;
- settings have safe defaults, types, bounds, translations, unknown-key behavior, and complete visible labels;
- CSS is scoped and resilient across Foundation, Horizon, mobile, desktop, light, dark, RTL, long content, missing assets, and supported browser modes;
- keyboard traversal, activation, dismissal, expanded state, accessible names, focus movement and return work in actual interaction, not only static markup;
- attachment, detachment, native update, pinning, rollback, disablement, and removal preserve the intended configuration and do not leave active remnants;
- normal application, classic comments embed, and full-app embed behavior are tested where the extension can affect them;
- uploads, header icons, SVG sprites, CSP, asset URLs, and cache behavior use supported mechanisms.

Human screen-reader conclusions require human assistive-technology evidence. Static markup or an automated tree alone is not sufficient.

## Administration and APIs

Administrator features should behave as native Discourse administration. Inspect access control, routes, navigation, settings, labels, responsive layout, loading, errors, cancellation, destructive confirmations, feedback, and focus.

For HTTP APIs and webhooks, document authentication, authorization, versioning, request and response schemas, limits, error codes, idempotency, replay behavior, compatibility, and deprecation. A controller inheriting from an admin controller is useful evidence but does not replace tracing all exposed actions.

## Synchronization and external publication

For integrations that publish or synchronize Discourse content, answer with evidence:

1. What content is eligible, and who enables or changes eligibility?
2. Which permission and visibility checks run before content leaves Discourse?
3. What identifies source content, its revision, destination content, and the connection?
4. Are create, update, retry, restart, and reconciliation idempotent and duplicate-safe?
5. What happens after timeout with unknown remote outcome, remote success/local failure, or local success/remote failure?
6. How are stale claims, leases, partial deployments, incompatible adapters, and credential rotation recovered?
7. How are deletion, unpublication, disablement, and destination isolation represented?
8. Can administrators preview, observe, retry, cancel, and resolve attention without editing the database?
9. Do static build/deploy steps preserve the same transaction and acknowledgement boundary?
10. Are publication state, revisions, failures, queues, and next actions understandable in the UI?

Treat undocumented assumptions as unresolved evidence. Trace high-risk flows end to end rather than reviewing isolated functions.

## Verification

Use the extension's documented commands and current Discourse tooling appropriate to its claimed support. Depending on the profile, verify applicable formatting, lint, types, locales, QUnit, RSpec, system tests, plugin CI, theme checks, packaging, and installation.

For integrated or release readiness, record exact Discourse Core identity and exercise the exact candidate artifact. Test representative clean install, upgrade from supported prior state, rollback or recovery, return to current, enable/disable, restart, migration, browser interaction, and supported-version boundaries.

A workflow definition is not execution evidence. Lint is not behavioral testing. Installation success does not prove compatibility, upgrade safety, accessibility, or external-service correctness.

## Authoritative sources

When current behavior matters, consult the Discourse version the extension claims to support and prefer authoritative sources:

- Discourse Core repository and developer documentation;
- official plugin skeleton and maintained examples;
- current Plugin API source and documentation;
- official Meta Discourse developer guidance.

State when a conclusion relies on current `main` rather than the claimed release line.
