# Lifecycle

This skill manages the project from the first plan through launch. Each run continues the last one. It does not start over, and it does not build a service the current plan leaves out.

## Read the operating record first

Before recommending or setting anything up, read what the project already decided:

- The launch checklist
- Active status (`docs/now.md` or the canonical status file)
- Durable decisions
- Notes
- The main agent instruction file

Those files, plus the code, are the current plan. A missing file means that part of the record does not exist yet. Do not invent a history to fill it.

## Compare the plan with this run

Decide which of these happened:

- **Unchanged.** The request fits the recorded shape. Work the open checklist items. Leave out-of-scope services unbuilt.
- **Scope added.** The product now needs a capability the plan marked not applicable or never mentioned. Name it, say what new requirement caused it, and ask only the questions that capability still needs.
- **Scope removed.** The product no longer needs a capability. Record why. Mark those checklist items not applicable. Do not provision them. Leave a service that is already built in place unless the user asks to remove it.
- **Scope replaced.** A decision supersedes an earlier one. Record the new decision and the date. Point at the old entry. Do not keep two current answers for the same choice.

Take the signal from the user, the code, and the operating record. A package that was never configured does not mean the plan changed.

## Ask only about the change

When scope is added, ask the smallest set of questions that chooses the new design. Recommend a default when this skill has one and the repository does not already have that piece.

Examples:

- A site with no accounts later needs users and saved records. Recommend one relational database. If none exists, recommend Neon, Drizzle, and separate development and production branches. Ask which sign-in methods are required if the code does not already show them. Do not ask about native store billing unless a native app is now in scope.
- A local-only app later needs data shared by web and mobile clients. Recommend a hosted database and a single API. Ask whether production must be isolated from development, and assume yes unless the user says otherwise.
- A public site later adds a native app. Ask the native questions only: accounts, digital goods, push. Keep the existing web stack.
- File storage was planned, then the product keeps files on device. Drop the storage section. Do not create a bucket.
- A product later targets enterprise buyers. Ask only for known buyer requirements and deadlines. Add E2EE, SSO, SCIM, MDM, audit evidence, contractual support, or procurement work only when required, and preserve the current architecture where it still fits.

Do not repeat questions the checklist or decision log already answered. Do not reopen a stack choice that still fits.

## Set up only what the current plan includes

During setup, build a service only when the reconciled plan includes it.

Neon is the default new relational database. Set it up when the plan needs persistent relational data and no database exists yet. Do not set it up for a marketing site, a static site, or a local-only app whose plan has no shared data. Do not set it up because a later phase might want it.

When a later run is the one that adds that need, that run recommends Neon, asks the remaining questions, adds the database section to the checklist, and performs the in-repo setup if the user asked to set the project up or agreed to that addition. Console work and connection strings stay external. Record variable names only.

The same rule applies to auth, email, storage, payments, push, analytics, a native app, a cloud project, E2EE, SSO, SCIM, MDM, compliance evidence, and procurement work. Absence at the beginning is correct. Presence becomes required only when the plan changes.

## Keep the record current

When a decision or scope change is accepted, update the operating record before the run ends:

- Checklist: add, check, or retire the affected items. Do not leave a dropped capability looking required.
- Decisions: dated entry, newest first, including why the previous choice changed.
- Active status: rewrite it so it describes the work that is current now.
- Notes: add a gotcha when the change creates one later sessions will trip on.
- Architecture: update the canonical architecture prose and Mermaid diagrams when boundaries, flows, environments, integrations, or release paths changed.

Create these files on the first plan or the first setup if they do not exist. On a later run, update the files that already exist. A pure audit that finds no change still refreshes checklist status and does not rewrite history.

This record is how the next run knows that a database was intentionally absent, how it knows the moment that stopped being true, and how it sees the resulting architecture without reconstructing it from scratch.
