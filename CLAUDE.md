# Project instructions

`project-launch` is a markdown-only Agent Skill for planning, auditing, setting up, and carrying software projects through launch. The authoritative workflow is [`SKILL.md`](SKILL.md). The architecture is documented in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

There are no runtime dependencies or application build commands. Validate changes with the Agent Skills validator and the local install preview documented in [`docs/PROJECT_LAUNCH.md`](docs/PROJECT_LAUNCH.md).

## Conventions

- Keep `SKILL.md` authoritative and load deeper references only when a phase applies.
- Keep examples generic and never include private project details, real credentials, or machine-specific paths.
- Do not add scripts or dependencies unless they are necessary and have been reviewed for public distribution.
- Public website URLs include `www` unless the user or an existing canonical host specifies another host or subdomain.
- Do not commit, push, force-push, rewrite history, or delete branches unless the user explicitly asks in the current session. Commit messages must not contain AI attribution or `Co-authored-by` trailers.

## Project memory

At the start of work, read this file, [`docs/now.md`](docs/now.md), [`docs/decisions.md`](docs/decisions.md), [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md), and [`docs/PROJECT_LAUNCH.md`](docs/PROJECT_LAUNCH.md).

When a durable decision is made, record the date and why. When the skill gains or drops a capability, update the checklist, decision log, architecture prose, and Mermaid diagrams before treating the new shape as settled. Add reusable gotchas to [`docs/notes.md`](docs/notes.md). Keep active status short and current. Do not create a second source of truth or add a service the current plan leaves out.
