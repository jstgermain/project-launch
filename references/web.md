# Web application

Load this for a marketing site, web app, admin dashboard, or API that lives in the web project. Skip it for a native-only or API-only product that has no web UI. An API-only service still uses the API placement rules below when a backend is in scope.

## Existing stack

If the repository already has a web framework, UI library, package manager, or router, keep them. Record the versions and commands you found. Do not migrate Next.js, Remix, Astro, Rails, or anything else because the new-project default is different.

A strict TypeScript gap on an existing project is a checklist item, not a silent `tsconfig` rewrite.

## New web defaults

Use these only for a new web UI when the user has not chosen a stack:

- Next.js with the App Router
- TypeScript with `strict` enabled
- pnpm
- MUI as the component library
- A project theme, not stock component defaults with no tokens

Do not add authentication, a database, or an admin area unless the shape needs them.

## Visual direction

For a new user-facing web UI, create a custom MUI theme. The direction is clean, restrained, and premium: generous whitespace, careful typography, subtle depth, little clutter, thoughtful motion, accessible contrast, predictable interactions, and solid responsive behavior.

That is a design sensibility. Do not copy another company's website, assets, icons, or layout.

Define tokens for typography, spacing, breakpoints, shape, palette, surfaces, buttons, form controls, cards, navigation, dialogs, and responsive behavior. Apply them through the theme so screens do not restyle components one by one.

Admin dashboards prioritize clarity, density, accessibility, and usability. Do not decorate an admin tool with a marketing layout. Internal tools can skip a public marketing theme entirely.

## Admin dashboard

Include this section only when the product has an admin surface.

Require:

- Authentication and server-side authorization. Hiding a button is not authorization
- Admin roles stored and checked on the server
- A shell and navigation that match the real areas
- CRUD for the areas the product needs, with validation, search or filtering, and pagination where lists can grow
- Loading and error states
- Responsive behavior that stays usable, not a copy of the marketing site
- An API boundary. The browser does not talk to the database with privileged credentials
- Production access restrictions: who can sign in, and how that is separated from customer accounts

Schema and audit logging are in scope when the product changes customer data or money. Do not add an audit log to a static site.

## API placement

Keep the API in the web application when one deployable can meet the requirements. Server actions, route handlers, or a small server module are all acceptable. Choose the pattern the framework already uses.

Consider a separate service only for a real constraint: a non-web client that must deploy independently, a job worker that must not run in the web process, or an existing service the repo already operates. Do not introduce microservices, GraphQL, or a queue because they might be useful later.

When a separate API is justified, record how web and native clients authenticate to it and which environment URL each build uses.

Webhooks, cron, and real-time features are included only when the product uses them. Signature checks for inbound webhooks are required when those routes exist.

## Public site

A public marketing or content site needs:

- A real document title and description strategy
- A canonical host once a domain exists. In metadata, redirects, and scripts, use `https://www.example.com`. Omit `www` when the user or the existing config names another host, or when another subdomain is the host instead of `www`
- Usable empty, loading, and error states only where the site is dynamic
- Basic metadata and a sitemap path appropriate to the framework

Do not bolt on an account system for SEO. If [web-presence-audit](https://www.skills.sh/creative-lid/web-presence-audit/web-presence-audit) is installed or the user includes it for this run, use that skill for the public discoverability pass. Install rules are in [companion-skills.md](companion-skills.md).

## Hosting decision

If deploy config already names a platform, that platform is the host. Audit its environments, env vars, and domain wiring. Do not propose a migration.

If nothing is configured, recommend one host that can serve the chosen framework, with preview deployments, managed TLS, environment variables, logs, and a rollback path. Record the recommendation as an assumption with one sentence of reasoning. Account creation is `NEEDS USER ACTION`.

Use Amplify-specific tasks only when Amplify is already in the repo or the user chooses it. Those tasks live in the infrastructure reference: app, branches, build settings, environment variables, domain, TLS, distribution behavior, deploy permissions, and separation of development, staging, and production where the product needs them.

Static assets and image delivery follow the host and framework. Do not add a separate image CDN until the current host cannot meet the requirement.

## Evidence

| Observation | Status |
| --- | --- |
| Framework app runs from documented scripts, routes match the shape | Complete for the app shell |
| UI library present, theme file absent, new user-facing app | Partially complete |
| Admin pages exist, checks are only in client components | Partially complete |
| Host config file present, production env names undocumented | Partially complete |
| Another framework already in use | Complete as the stack choice. Audit gaps, do not replace it |
