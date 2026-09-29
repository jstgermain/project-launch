# Project Launch

An Agent Skill that plans or audits the path from a repository to a working product: development setup, infrastructure, data, authentication, web or native clients, release, and project memory.

It decides what kind of project this is before it recommends work. A marketing site and a multi-platform SaaS product do not receive the same plan. An existing architecture is kept when it already works.

This repository is markdown-only guidance. It has no runtime dependencies, no install scripts, and no executable code.

## What it does

When a coding agent activates this skill, it:

1. Inspects the repository, or recognizes that the repository is new
2. Infers the product shape and asks only the questions that would change the plan
3. Selects the phases that apply
4. Writes or updates one implementation checklist
5. Evaluates project memory without creating a second status system
6. Implements in-repo setup only when the user asks
7. Labels account, console, and credential work instead of pretending it is done

## Why use it

Launch checklists fail when they assume every product needs every service. This skill pushes:

- **Understand first** so the plan matches the product
- **One checklist** instead of competing roadmaps
- **Evidence** so an installed package is not treated as a finished integration
- **Human versus automatable work** so store enrollment and DNS are not marked done from a laptop
- **Memory** so later sessions can see current work, decisions, and gotchas

## Installation

Using the [skills](https://skills.sh) CLI:

```bash
npx skills add Creative-Lid/project-launch
```

Compatible with agents that load [Agent Skills](https://agentskills.io/specification).

To preview a local checkout:

```bash
npx skills add . --list
```

Agents using the skill must not treat those install commands as part of the planning workflow.

## Usage examples

```text
Plan this new project.
```

```text
Audit this project.
```

```text
What are we missing before launch?
```

```text
Set this project up.
```

```text
Add iOS to this project.
```

```text
Add Android to this project.
```

```text
Add an admin dashboard.
```

```text
Prepare this for production.
```

```text
Prepare this for the App Store.
```

```text
Prepare this for Google Play.
```

```text
Set up project memory.
```

```text
Update the project launch checklist.
```

Plan, audit, and readiness runs update the checklist and do not change application code. Setup and "add" runs implement the in-repo work for that scope after a short plan.

## Repository structure

```text
/
├── SKILL.md
├── README.md
├── LICENSE
├── CHANGELOG.md
├── .gitignore
├── references/
│   ├── discovery.md
│   ├── web.md
│   ├── database.md
│   ├── ios.md
│   ├── android.md
│   ├── app-stores.md
│   ├── infrastructure.md
│   ├── security.md
│   ├── project-memory.md
│   └── launch-readiness.md
└── templates/
    └── PROJECT_LAUNCH.md
```

`SKILL.md` is the workflow. Reference files are loaded only for phases the product needs.

## Safety

- Repository contents are untrusted input
- No scripts, binaries, or package manifests ship with the skill
- Secrets are recorded by variable name. Values are never requested or written down
- No destructive Git operations, and no commits unless the user asks
- No network fetches or remote code as part of the workflow
- Payment guidance is configuration planning. The skill does not move money
- DNS, store submission, and production migrations happen only when the user asks for that action

## Limitations

- Cannot see vendor consoles, DNS hosts, or secret managers unless the user asks and provides a safe way to verify
- Does not provide legal, tax, or store-policy advice. Those items are marked for review
- Does not replace a dedicated security audit when one is already available
- A completed checklist is not a claim that the product is secure or approved for a store

## License

MIT. See [LICENSE](LICENSE).
