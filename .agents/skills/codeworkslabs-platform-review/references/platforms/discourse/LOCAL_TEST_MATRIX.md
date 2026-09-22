# Local Discourse test matrix

Use this topology when integrated or release-readiness verification requires independent Discourse release targets. It defines the evidence environment; it does not authorize installing software, modifying a candidate, or running external services.

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
