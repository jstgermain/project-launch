# Database

Load this only when the product stores relational data or already has a database. A marketing site without accounts does not get a database.

## Existing database

If the project already uses PostgreSQL, MySQL, SQLite, or a hosted database, keep that system and its migration tool. Document the name, where schema lives, how migrations run in development, and how they run in production.

Do not migrate a working database to Neon because Neon is the default for new projects. Do not introduce a second ORM.

Judge completeness from the migration path and environment split, not from the driver package.

## New relational default

When a new product needs relational data and no database is chosen:

- Neon PostgreSQL
- Drizzle ORM
- Drizzle Kit
- At least two branches: development and production
- Preview or staging branches when the host already has those environments

Neon Auth is appropriate only when Neon is the database, the product needs authentication, and Neon Auth covers the required sign-in methods and session model. If it does not, keep Neon for data and choose one separate auth provider. Do not run two user stores.

## Environments

Local and development code use the development branch. Production uses the production branch. Record the variable names per environment, typically `DATABASE_URL` plus a direct migration URL when the host distinguishes pooled and direct connections.

Use the pooled connection for the running app when the host is serverless. Use a direct connection for migrations. Document which variable is which.

Never point the default development env file at production. Say that in the README and in `docs/notes.md` when memory is set up.

Production branch protections, backups, and who may reset data are checklist items. Resetting or branching production is not something to do while planning.

## Roles

Prefer an application role that can use the product schema and a separate migration role when the platform makes that practical. Do not give the application role permission to drop the database. Exact role SQL is written only during an authorized setup, against the project's real schema, not copied blindly.

## Drizzle

When Drizzle is the tool, account for:

- Schema directory
- `drizzle.config` pointing at that schema and a migrations folder
- Generated SQL migrations
- The migration journal. A SQL file that is not listed in the journal is not part of the migration set
- A development command that generates and applies migrations
- A production command that applies committed migrations
- Review of generated SQL before it is treated as ready
- A seed path only when the product needs seed data. Seeds must refuse to run against production unless they are explicitly a production-safe reference seed

Prefer the project's generate command so the SQL file and the journal entry are created together. If SQL is added by hand, update the journal in the same change. The journal tag must match the migration filename.

Do not use a schema push command against production as a substitute for migrations. The project README or notes must state the real commands. If a local skill for Drizzle migration journals is already installed, follow it during implementation. Do not install skills from the network.

## Other ORMs

If Prisma, Kysely, or another tool is already in place, document its generate and deploy commands instead. The same environment and production-migration rules apply. Do not add Drizzle beside it.

## Evidence

| Observation | Status |
| --- | --- |
| Schema, committed migrations, journal or equivalent, and separate env names for development and production | Complete, aside from console state you cannot see |
| Client installed, no migration directory | Partially complete |
| Migrations exist, production command undocumented, push script is the only command | Partially complete |
| One shared production URL used for local development | Partially complete, and call out the risk |
| Hosted database console state, backups, and branch protection | Needs verification unless documented with evidence |

Creating the hosted project and storing production `DATABASE_URL` in the host are `EXTERNAL CONSOLE` or `NEEDS USER ACTION`. Do not invent the connection string.
