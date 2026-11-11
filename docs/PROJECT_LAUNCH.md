# Project launch

Shape: existing markdown-only Agent Skill repository
Mode: documentation and readiness audit
Updated: 2026-11-11

Assumptions:

- `SKILL.md` remains the authoritative workflow.
- The package continues to have no runtime dependencies, executable scripts, hosted services, or vendor accounts.
- Publication target is skills.sh from the public `jstgermain/project-launch` repository.
- Application phases such as web, database, authentication, native clients, payments, and cloud infrastructure do not apply to this repository itself.

## Repository and foundation

- [x] Root `SKILL.md`, `README.md`, `LICENSE`, `CHANGELOG.md`, and `.gitignore` exist
- [x] Skill name matches the repository directory
- [x] Package is markdown-only and has no runtime dependencies or install hooks
- [x] Examples are generic and contain no source-project identity
- [x] README repository tree includes every shipped reference and documentation file
- [x] Version `1.4.0` is consistent across skill metadata and release notes

## Project memory

- [x] Initialize or verify project memory
- [x] `CLAUDE.md` points to the authoritative workflow and operating record
- [x] `docs/now.md` contains only active work
- [x] `docs/decisions.md` is the single durable decision log
- [x] `docs/notes.md` is the single reusable-gotcha log
- [x] Documentation roles are indexed in `docs/README.md`

## Architecture documentation

- [x] `docs/ARCHITECTURE.md` describes the current package, workflow, phase routing, trust boundaries, and documentation ownership
- [x] Mermaid diagrams show system context, repository structure, lifecycle flow, phase routing, and safety boundaries
- [x] Deliberate omissions explain why no application services belong in this repository
- [ ] [AUTOMATABLE] Render or parse-check Mermaid diagrams with an available safe validator
- [x] README, architecture, decisions, status, notes, and checklist describe the same current package and lifecycle

## Skill behavior

- [x] New and existing project modes are distinct
- [x] Later runs reconcile scope changes instead of repeating the original interview
- [x] Services are set up only when the current plan needs them
- [x] Neon is conditional on a new relational-data need and absence of an established database
- [x] Companion skills are offered only when applicable and installed only with consent
- [x] Public website URLs default to `www` with explicit exceptions
- [x] Human, external-console, verification, automatable, manual, and blocked work can be distinguished
- [x] Architecture documentation is now part of memory and lifecycle reconciliation
- [x] Architecture-document synchronization is included in conceptual regression checks
- [x] Enterprise readiness activates only from a buyer, threat, contractual, regulatory, or managed-device requirement
- [x] Plausibly affected products get one screening question; a no answer skips the phase and an unknown answer does not add every capability
- [x] Technical security findings are separated from evidence, legal commitments, and procurement status
- [x] Flutter is a first-class architecture choice with target-specific platform and release checks
- [x] Existing Flutter clients stay Flutter and are not rewritten as separate native clients

## Native store automation behavior

- [x] TestFlight, App Review, Play testing, and Play production are explicit destinations
- [x] Release intent records exact platforms, versions/builds, notes, groups/tracks, and requested mutations
- [x] Metadata sync, build, upload, processing, testing distribution, review attachment, submission, rollout, verification, and reconciliation are independently invokable stages
- [x] Exact platform/version/build or version-code selection is required before store mutation
- [x] Apple certificate cleanup classifies resources and preserves distribution, Developer ID, personal, and unknown certificates
- [x] Google Play edit, track promotion, staged rollout, policy readiness, and verification paths are distinct
- [x] CI retries inspect remote state before creating another version, certificate, profile, edit, or review request
- [x] In-progress store mutations use non-cancelling release concurrency

## Enterprise readiness behavior

- [x] E2EE is distinguished from TLS and encryption at rest
- [x] E2EE planning includes protected content, metadata, keys, recovery, sharing, search, support, backups, and cryptographic review
- [x] SSO planning covers tenant configuration, domain ownership, role mapping, enforcement, break-glass access, and representative-provider testing
- [x] SCIM planning covers users/groups, stable identifiers, idempotency, deprovisioning, reconciliation, and privilege mapping
- [x] MDM planning applies only to managed mobile/desktop clients and requires representative managed-device verification
- [x] Compliance evidence records scope, owner, artifact, collection method, period, cadence, and reviewer
- [x] Contractual support separates SLOs from approved SLAs and requires human approval
- [x] Procurement tracks questionnaires, agreements, insurance/business materials, accessibility, onboarding, and approvals without storing confidential buyer files publicly
- [x] Technical production readiness and contracted-customer readiness are reported separately

## Documentation quality

- [x] Every relative Markdown link resolves
- [x] Frontmatter name, version, and 665-character description pass local checks and the reference validator
- [x] Markdown code fences and trailing whitespace checks pass across all Markdown files
- [x] `SKILL.md` owns workflow while references deepen non-conflicting phases
- [x] The template demonstrates architecture documentation and tells target repositories to remove irrelevant sections

## Validation and security

- [x] `skills-ref validate .` reports `Valid skill: .`
- [x] `npx skills add . --list` validates the local path and discovers exactly one `project-launch` skill
- [x] Secret-like value, private-key, credential, and env-file scan has no findings
- [x] Private-name, customer-data, and developer-specific absolute-path scan has no findings
- [x] Suspicious download/execute, shell-pipe, obfuscation, destructive-command, and telemetry scan has no findings
- [x] Repository remains markdown-only with no dependencies or generated package artifacts
- [ ] [NEEDS VERIFICATION] Run the publication platform's remote reputation and security checks after the public repository is indexed

## Scenario regression review

- [x] New marketing-only website omits auth, database, native, and store work
- [x] Existing Next.js application preserves its framework, router, UI library, and package manager
- [x] New SaaS with admin adds accounts, relational data, server-side admin authorization, and only applicable infrastructure
- [x] Existing web app missing production infrastructure adds environment, deployment, monitoring, domain, and rollback work without rescaffolding
- [x] New iOS-only application omits Android, web, database, StoreKit, and push unless required
- [x] New Android-only application omits iOS, web, database, Play Billing, Firebase, and Google Cloud unless required
- [x] New Flutter client uses only selected targets and does not also scaffold SwiftUI and Compose product clients
- [x] Existing Flutter client separates shared Dart checks from each platform runner, signing path, and store release
- [x] Web plus iOS plus Android separates web payments from store billing and uses one justified backend
- [x] Existing mobile app with partial store setup keeps console state as external or needs verification
- [x] Existing project with a non-default database preserves that database and migration tool
- [x] Mature repository integrates with its established status and memory system
- [x] Later scope change adds Neon only when relational persistence becomes necessary
- [x] Architecture update changes diagrams, decisions, active status, and checklist together
- [x] New enterprise SaaS includes only confirmed E2EE, identity, evidence, support, and procurement requirements
- [x] Existing SaaS entering procurement preserves its architecture and separates reusable product gaps from buyer-specific paperwork
- [x] A product using TLS without a protected-content threat model and key lifecycle is not marked E2EE
- [x] A selected SSO/SCIM provider without tested tenant lifecycle remains partially complete
- [x] A policy set without dated operating evidence is not marked audit-ready

## Publication

- [x] Public installation target is `jstgermain/project-launch`; the source remote and visibility are verified before publication
- [x] Final content review finds generic examples, no private source-project identity, and no machine-specific path
- [ ] [NEEDS USER ACTION] Publish or push the reviewed release when ready
- [ ] [NEEDS VERIFICATION] Confirm skills.sh indexing and all platform security/reputation checks pass

## Post-publication maintenance

- [ ] [MANUAL] Re-run this checklist when project shape, defaults, supported platforms, or publication requirements change
- [ ] [MANUAL] Keep `CHANGELOG.md`, version metadata, architecture diagrams, and operating record aligned for every release
- [ ] [MANUAL] Re-evaluate policy-sensitive App Store and Google Play guidance before changing release rules
