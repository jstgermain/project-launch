# Project launch checklist

Copy this structure into `docs/PROJECT_LAUNCH.md`, or into the planning file the repository already uses. Delete every section the shape does not need. Do not copy this help text into the project.

Rules:

- One checklist per repository. Reconcile with what is already written. Do not duplicate an item under a new heading.
- Check a box only after the item is verified.
- Add at most one tag when the owner is not obvious: `NEEDS USER ACTION`, `EXTERNAL CONSOLE`, `NEEDS VERIFICATION`, `AUTOMATABLE`, `MANUAL`, `BLOCKED`.
- Write paths you actually saw. Write secret names, never values.
- Keep `Updated` as an ISO date. Do not timestamp every line.
- Assumptions belong at the top, not buried in checkboxes.

```markdown
# Project launch

Shape: web application with admin dashboard
Mode: existing project audit
Updated: YYYY-MM-DD

Assumptions:
- The existing web framework stays in place.

## Companion skills

- [x] security-audit installed and included
- [ ] web-presence-audit declined

## Project memory

- [ ] Initialize or verify project memory
- [ ] Main agent instructions exist and mention current status
- [ ] Active status covers only current work
- [ ] Durable decisions have a single home
- [ ] Reusable gotchas have a single home

## Architecture documentation

- [ ] One canonical architecture document matches the current project shape
- [ ] Mermaid diagrams show the applicable system, data, environment, or release flows
- [ ] Architecture prose, diagrams, decisions, active status, and this checklist are aligned

## Web application

- [x] App shell and documented dev command (`package.json`)
- [ ] [AUTOMATABLE] Add a project theme instead of unthemed defaults

## Admin dashboard

- [ ] [AUTOMATABLE] Enforce admin checks on the server for every admin mutation

## Database

- [x] Schema and committed migrations are present
- [ ] [NEEDS USER ACTION] Store production `DATABASE_URL` in the hosting environment
- [ ] [EXTERNAL CONSOLE] Confirm the production branch is separate from development

## Production environment

- [ ] [NEEDS VERIFICATION] Confirm `https://www.example.com` is canonical and the apex host redirects to it, unless another host or subdomain was specified

## Flutter client

- [ ] [AUTOMATABLE] Confirm selected targets and keep one shared Dart client with platform adapters
- [ ] [AUTOMATABLE] Pin compatible Flutter/Dart and native platform toolchains
- [ ] [AUTOMATABLE] Verify production identifiers, endpoints, flavors/schemes, and per-platform versions/builds
- [ ] [NEEDS VERIFICATION] Prove release builds on the host required by each selected target

## Release pipeline

- [ ] [AUTOMATABLE] Make every deploy depend on applicable build and test gates
- [ ] [AUTOMATABLE] If an API deploy is selected, require its deployment and live health check before dependent web or mobile releases
- [ ] [AUTOMATABLE] Allow UI-only releases when API deployment is intentionally not selected
- [ ] [AUTOMATABLE] Keep TestFlight, App Review, Play testing, and Play production as explicit destinations
- [ ] [AUTOMATABLE] Require per-release consent before replacing an existing App Review submission
- [ ] [AUTOMATABLE] Validate a release request with exact platform versions/builds, notes, groups/tracks, and destination
- [ ] [AUTOMATABLE] Separate metadata sync, build, upload, processing, testing distribution, review attachment, submission, rollout, verification, and reconciliation
- [ ] [AUTOMATABLE] Prevent overlapping store mutations without cancelling an in-progress upload
- [ ] [NEEDS VERIFICATION] Verify the exact processed build or version code reached the requested testing, review, or production destination

## Security

- [ ] [AUTOMATABLE] Ignore local env files and keep `.env.example` names only

## Enterprise readiness

- [ ] [NEEDS VERIFICATION] Confirm which buyer requirements are contractual versus requested
- [ ] [AUTOMATABLE] Document E2EE threat model and key lifecycle if E2EE is required
- [ ] [AUTOMATABLE] Verify tenant-scoped SSO and SCIM lifecycle behavior if enterprise identity is required
- [ ] [MANUAL] Test managed-app configuration on a representative managed device if MDM is required
- [ ] [MANUAL] Assign owners and collection periods for required compliance evidence
- [ ] [NEEDS USER ACTION] Approve contractual support, SLA, privacy, and data-processing commitments
- [ ] [BLOCKED] Track buyer security review and procurement dependencies with target dates
```

That sample is a shape, not a form to fill for every product. A marketing-site checklist stops after memory, web, hosting, domain, analytics, monitoring, and security. An iOS-only checklist uses memory, iOS, Apple Developer, and the store sections instead. Delete the enterprise section unless the buyer, contractual, regulatory, or managed-device profile makes it applicable.

When a section has no open or completed items, omit the section.
