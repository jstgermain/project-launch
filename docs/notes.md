# Notes

- `SKILL.md` is authoritative. References deepen a phase but must not replace or contradict the workflow.
- This repository is markdown-only. A request to add scripts or dependencies should first justify why documentation cannot safely express the behavior.
- The example checklist in `templates/PROJECT_LAUNCH.md` is intentionally broad. Target repositories delete irrelevant sections.
- Public website URLs default to `www`; another explicit canonical host or subdomain stays as written.
- Neon is a conditional default for a new relational-data need, never a baseline dependency.
- Release destinations remain distinct: TestFlight is not App Review, and Play testing is not Play production.
- Store uploads are asynchronous. Verify the exact platform, marketing version, build number or version code, group or track, notes, and review/rollout state after every mutation.
- Apple automatic signing can exhaust certificate quotas when CI creates disposable development certificates. Reuse valid signing resources and revoke only expired or clearly automation-created development certificates after a dry-run classification.
- Technical production readiness and contracted-customer readiness are separate. Procurement, audit, or legal work can block the latter after the application is deployable.
- HTTPS and encryption at rest are not E2EE. E2EE requires a documented threat model and key lifecycle in which the service operator cannot access the protected plaintext.
- SSO and SCIM are separate tenant capabilities; a provider selection or installed package does not prove either is complete.
- Do not turn commit subjects into historical decisions without corroborating evidence.
