# Local Discourse test matrix

Use this topology when integrated or release-readiness verification requires independent Discourse release targets. It defines the evidence environment; it does not authorize installing software, modifying a candidate, or running external services.

## Finite execution plan

Before execution, agree one finite plan with the owner. Record:

- the exact candidate, claimed compatibility targets and authorized actions;
- the existing repository suites and applicable protocol checks, with their commands or procedures and expected case discovery;
- the setup, execution and results-review phases, with concrete time budgets, repair/retry limits and stopping points;
- which human procedures are deferred and which evidence will establish completion.

Use the supported repository checks first. A missing result or Not verified row is a coverage status, not automatic authority to invent test cases. New cases, additional environments beyond the agreed matrix, expanded coverage and additional review work require owner approval. Routine work within the approved plan does not need command-by-command permission.

These controls do not waive required review methods or coverage. If required work cannot be completed within the approved plan, report the gap and seek direction; do not silently narrow the requirement or claim completion. An explicit stop instruction takes precedence over an unfinished plan.

## Necessity before invention

Use existing supported workflows and established runners. Before adding support code, a launcher, guard or diagnostic helper, identify the observed blocker, why the existing supported tools cannot handle it, and the original approved requirement the smallest proposed addition will immediately enable. Record this reasoning in the existing work record; do not turn routine authorized repairs into another approval questionnaire.

Verify environmental facts before relying on them, including the actual helper API, service account, process ownership, port state and evidence-capture behavior. Do not build speculative guards or claim outcomes from assumed environment details. A missing result alone does not justify new machinery.

## Execution before further preparation

After a permitted repair, immediately exercise the original blocked path before preparing another variant, derivative runner or future execution packet. Confirm that execution actually reaches the repaired operation and capture its result; preparation, successful startup or a failure before that operation does not establish that the repair works.

Demonstrate the supported procedure's startup, readiness, actual check, evidence capture and shutdown/preservation path in one representative environment before multiplying that procedure across environments. This establishes runner suitability only, not product acceptance or verification of the remaining targets. If the blocked path still fails, retain the result and apply the agreed repair/retry stopping limits; do not accumulate unexercised repairs.

## Separately authorized infrastructure work

An observed infrastructure dependency is not authority to develop a replacement runner, diagnostic framework, guard system or coordination layer inside the verification assignment. If the supported workflow cannot proceed without substantial infrastructure development, stop the affected path, identify the dependency and the required check it blocks, and obtain separate owner authorization for a bounded infrastructure scope, budget and completion criterion before doing that work.

Small necessary repairs may proceed only within the existing authorized repair scope and budget, subject to the necessity and execution controls above. Separate infrastructure authorization does not authorize product changes, expand the verification requirements or reset its retry budget. Keep unfinished verification in the separate status record while the dependency is unresolved.

## Working setup before matrix execution

Use a short, budgeted setup check before long matrix jobs. Establish one working native baseline first, then check each target's own readiness before its full jobs. This does not transfer runtime acceptance between targets or permit shared mutable state.

Within the authorized setup scope, establish:

- exact candidate, Core, toolchain and owned service/database identities;
- usable dependencies/assets, a ready native server, browser launch/connection and execution through the supported test framework;
- the native installation/import path needed by the planned job, including public Git transport where applicable;
- valid external fixture APIs, locators, inputs, expectations and observation methods.

Check actual in-test viewport dimensions rather than treating an outer-window resize request as a measurement. Match embed parent/child schemes and CSP, use native file-locator semantics, and respect the product's documented normalization. A setup check is not a new product test suite or release acceptance.

Do not launch dependent long jobs while their setup is known to fail. Repairs must stay within the approved external-harness scope and repair budget; a setup failure does not authorize product changes, a new framework or an expanding diagnostic campaign.

## Time budgets and failure stops

Record startup/compilation, browser connection, native assertions and whole-job limits separately. Base the overall job allowance on the suite size and trustworthy observed durations, including cold startup. Do not reuse a fixed cutoff across targets without checking whether the declared suite can finish within it. Earlier timing may inform a budget, but does not supply acceptance evidence for a new target.

Keep native assertions and their limits unchanged unless a specific change is authorized and recorded. Do not increase assertion timeouts to hide a failure. An outer deadline reached before the suite finishes means incomplete execution, not a compatibility defect or successful completion.

Use only the agreed number of repair/retry attempts within the agreed time budget. When either is exhausted, stop the affected lane, preserve its evidence and owned state, and promptly report the failed operation, established cause or unknown cause, completed outcomes and coverage left open. Do not continually reset the budget by naming another harness, diagnostic or continuation. Other independent work may proceed only within its existing authority and budget; a commission-wide stop ends it too.

## Results and separate status record

Distinguish:

- a passed product assertion;
- a failed product assertion;
- a setup, transport, compiler, launcher or harness operation failure;
- a case not executed, or an outcome not established.

Report test cases, named procedure groups and individual assertions using their own denominators. A process exit of zero is not proof that every expected case ran. Use Unreached only when control-flow evidence establishes that the check was not reached; otherwise retain Unknown. Preserve original failures and their source/deadlines rather than replacing them with a later green narrative.

Maintain unfinished coverage in a separate verification status record, linked to the candidate, target, existing requirement and supporting result. Keep current observations distinct from historical appendices. That record is not a work queue, scope expansion or authorization to resume after a stop. Deferred human procedures remain deferred; do not repeatedly request availability or substitute automated output for human evidence.

## Results review and closure

Plan the required independent results review as part of the agreed work. Reconcile actual outcomes and material new evidence without creating a continuing chain of report revisions or reviews. This does not waive an applicable doctrine or a separately commissioned review-method audit.

At closure, preserve raw results and original failures, identify incomplete requirements, and record export and owned-service shutdown/preservation outcomes. Missing shutdown confirmation is not evidence that a service is still running. Confirm exact owned targets before any stop or cleanup; never delete evidence or disturb unrelated services to make the record look clean.

Provide one current handoff linking the correction list, verification status and retained evidence. Writing that handoff does not itself establish acceptance or authorize further execution.

## Five test slots

| Slot | Purpose | Typical Core target |
|---|---|---|
| `main` | Forward-compatibility detection | Exact commit from Discourse `main` |
| `current-monthly` | Current production release behavior | Exact current `release/YYYY.M` commit or tag |
| `previous-monthly` | Previous monthly release while still supported and claimed | Exact preceding supported `release/YYYY.M` commit or tag |
| `esr` | Maintained ESR behavior claimed by the extension | Exact maintained ESR branch, tag, patch, or compatibility target |
| `lifecycle` | Clean install, native update, rollback or recovery, and return to candidate | Exact sequence of immutable Core and extension identities required by the lifecycle claim |

The September 2026 example maps these slots to `main`, 2026.9, 2026.8, claimed 2026.7 ESR targets, and a separate lifecycle environment. Refresh the actual supported targets from Discourse's authoritative release data before every review.

If an extension claims multiple materially distinct ESR or monthly lines, add isolated targets or reprovision a slot from a verified clean baseline. Never collapse claimed release lines merely to keep the slot count at five.

## Isolation model

Each compatibility slot must have its own:

- Discourse source root and exact Core checkout;
- PostgreSQL state;
- Redis state;
- container and persistent-volume identities;
- port or local hostname;
- fixture or baseline identity;
- execution and reset record.

The slots may share immutable Docker images, dependency caches, and Git objects. They must not share mutable database, Redis, uploads, generated assets, or runtime state.

On Windows, keep the Discourse source roots inside the WSL Linux filesystem rather than under `/mnt/c`. Discourse's Docker development flow documents this requirement. Distinct workspace-folder names also allow Dev Container PostgreSQL, Redis, and Node volumes to remain independently named.

## Candidate handling

Create one immutable candidate archive or exact commit identity before matrix execution. Install or mount that same candidate in every slot. Do not test one release from a mutable working checkout and another from a different archive while describing them as one candidate.

Record for every slot:

- Core branch, commit, release tag, and support role;
- extension repository, commit, tree, tag, version, archive inventory, byte count, and SHA-256 as applicable;
- container image and volume identities;
- Ruby, Node.js, package-manager, browser, PostgreSQL, and Redis versions that affect the result;
- commands, start and finish times, complete results, residue, and unexecuted checks.

## Resource model

Define all five slots, but normally run only the target under test. Starting every Rails, PostgreSQL, Redis, Ember, and browser stack concurrently wastes resources and increases port and process confusion without improving ordinary matrix evidence.

Run targets serially unless a test specifically requires concurrency across Discourse instances. Shut down a slot after its evidence is sealed; preserve or discard its state according to the declared reset policy.

## Control interface

Use one matrix manifest and a small deterministic control surface equivalent to:

- `up <target>` — verify identity, then start one slot;
- `test <target>` — execute the declared checks and capture evidence;
- `down <target>` — stop the slot without silently destroying evidence;
- `reset <target>` — restore the documented clean baseline after confirming the exact target.

The manifest should record slot name, source root, Core ref and commit, port or hostname, container and volume identities, fixture identity, candidate identity, current state, and last verified reset.

Do not make manual container names, ports, databases, or candidate copies the source of truth.

## Lifecycle slot

Keep lifecycle evidence separate from compatibility smoke tests. The lifecycle slot must support a deliberate sequence such as:

1. restore the exact supported prior state;
2. install or update to the candidate;
3. verify data, settings, behavior, jobs, and generated assets;
4. perform the claimed rollback or recovery;
5. verify the restored state;
6. return to the candidate and verify it again.

Use snapshots or backups whose identities are recorded. Do not call reinstalling an empty site an upgrade or rollback test.

## Safe local services

Use local fixtures and non-production services. Do not place production credentials, real outbound mail, live webhooks, customer data, or provider mutation authority in the matrix. Use MailHog or an equivalent local mail sink when mail behavior matters.

## Authoritative setup sources

- Discourse Docker development setup: https://github.com/discourse/discourse/blob/main/docs/developer-guides/docs/02-development-environments/03-docker-setup.md
- Discourse Dev Container configuration: https://github.com/discourse/discourse/blob/main/.devcontainer/devcontainer.json
- Discourse release support data: https://github.com/discourse/discourse/blob/main/versions.json
- Discourse version-compatibility guidance: https://github.com/discourse/discourse/blob/main/docs/developer-guides/docs/03-code-internals/05-version-compatibility.md
