# Changelog

## 1.4.0

- Add first-class Flutter architecture and per-target release planning for mobile, desktop, and web clients
- Add a reusable release-request contract for TestFlight, App Review, Play testing, Play production, and post-launch reconciliation
- Separate metadata sync, build, upload, processing, testing distribution, review attachment, submission, rollout, verification, and reconciliation
- Add Apple certificate lifecycle safeguards, exact-build selection, and TestFlight/App Review verification
- Add Google Play edit, track, promotion, staged-rollout, listing, and policy-readiness guidance
- Add retry-safe CI rules, non-cancelling store-upload concurrency, toolchain pinning, and exact build-number checks

## 1.3.0

- Add conditional enterprise-readiness discovery for enterprise, regulated, public-sector, security-sensitive, and managed-device customers
- Add E2EE threat-model and key-lifecycle planning without confusing TLS or encryption at rest with E2EE
- Add SSO, SCIM, MDM, compliance-evidence, contractual-support, and procurement readiness guidance
- Separate technical security findings from assurance evidence, legal commitments, and buyer approval
- Track long-lead audit and procurement dependencies independently from technical production readiness

## 1.2.0

- Require one canonical architecture document that stays aligned with the current plan and implementation
- Add Mermaid guidance for system, data, environment, and release flows
- Add architecture upkeep to project memory, lifecycle reconciliation, and the launch checklist
- Add this repository's architecture, status, decisions, notes, and comprehensive publication checklist

## 1.1.3

- Add a generic safe-release standard for conditional API dependencies, live health gates, and UI-only releases
- Keep TestFlight, App Review, Play testing, and Play production as explicit destinations
- Require per-release consent and a final App Store Connect recheck before replacing an existing Apple review submission
- Add store artifact, credential, version, and post-upload verification guidance

## 1.0.0

Initial release of `project-launch`.

- Agent Skill for planning, auditing, and bootstrapping a software project without assuming every product needs the same services
- Shape-first workflow for marketing sites, web apps, admin tools, SaaS, APIs, native iOS, native Android, and monorepos
- Living checklist at `docs/PROJECT_LAUNCH.md`, with human and console work labeled separately from in-repo work
- New-project defaults for web (Next.js, TypeScript, pnpm, MUI) and relational data (Neon, Drizzle) that never replace a working stack
- Project memory workflow that integrates with existing instruction and status files
- Release readiness for web, App Store, and Google Play, including store-billing policy flags
- Per-platform store version and review-state guidance, using Apple events where an authenticated backend already exists and pending-only reconciliation for Google Play or static products
- Native launch checks for compact devices, safe areas, legacy Android navigation, scrolling sheets, keyboard avoidance, physical media flows, and resumable setup
- Markdown-only package with no scripts, install hooks, or runtime dependencies
- Public website URLs include `www` unless another host or subdomain is specified
- Optional companion skills: security-audit, improving-code-quality, and web-presence-audit, installed only after the user agrees
- Living plan: services such as Neon are set up only when the current plan needs them, and a later scope change reopens just that decision
