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

## Project memory

- [ ] Initialize or verify project memory
- [ ] Main agent instructions exist and mention current status
- [ ] Active status covers only current work
- [ ] Durable decisions have a single home
- [ ] Reusable gotchas have a single home

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

- [ ] [NEEDS VERIFICATION] Confirm the canonical hostname and TLS certificate

## Security

- [ ] [AUTOMATABLE] Ignore local env files and keep `.env.example` names only
```

That sample is a shape, not a form to fill for every product. A marketing-site checklist stops after memory, web, hosting, domain, analytics, monitoring, and security. An iOS-only checklist uses memory, iOS, Apple Developer, and the store sections instead.

When a section has no open or completed items, omit the section.
