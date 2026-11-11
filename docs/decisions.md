# Decisions

Newest first.

## 2026-11-11 — Treat native store delivery as an explicit lifecycle

Flutter and native projects need a reusable release contract that works before and after first launch. TestFlight, App Review, Play testing, and Play production remain separate destinations, and metadata sync, build, upload, processing, distribution, review attachment, submission, rollout, verification, and reconciliation remain separate stages. Automation reuses existing project scripts, selects exact platform versions/builds, fails closed on ambiguous state, and manages signing resources without creating disposable Apple certificates on every run.

## 2026-10-28 — Make enterprise readiness conditional and multi-track

Enterprise, regulated, public-sector, security-sensitive, and managed-device products may need E2EE, SSO/SCIM, MDM, formal security assessment, compliance evidence, contractual support, and lengthy procurement. For plausibly affected products, the skill asks one screening question, then activates only confirmed tracks. A no answer skips the phase; an unknown answer does not add every capability. Technical launch and contracted-customer readiness remain separate states, and no repository evidence is treated as certification or legal approval.

## 2026-10-27 — Maintain a canonical architecture document

Every project-launch lifecycle keeps one current architecture description with Mermaid diagrams where they improve understanding. Architecture documents the confirmed system; the checklist tracks remaining work; decisions explain why; active status states what is happening now.

## 2026-10-27 — Treat project setup as a repeatable lifecycle

The skill may run throughout development. Each run reconciles the repository with the operating record and asks only about newly added or removed capabilities. Services such as Neon are introduced only when the current plan requires them.

## 2026-10-27 — Use `www` as the default public website host

Generated public website URLs use `https://www.example.com` unless the user or existing repository specifies another canonical host or a different subdomain such as `app` or `api`.

## 2026-10-27 — Companion skills require user consent

The skill may offer security-audit, improving-code-quality, and web-presence-audit when applicable. A missing companion skill is installed only after the user agrees in the current session.

## 2026-10-27 — Keep this package markdown-only

The skill ships instructions, references, and templates without runtime dependencies, executable scripts, install hooks, or telemetry. This keeps distribution and security review straightforward.
