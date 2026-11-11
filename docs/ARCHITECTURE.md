# Architecture

Updated: 2026-11-11

## Purpose and shape

`project-launch` is a markdown-only Agent Skill. It acts as a lifecycle consultant for new and existing software repositories: discover the project shape, reconcile the current plan, route only applicable domain guidance, maintain architecture and project memory, produce one actionable checklist, and implement setup only when explicitly requested. It supports separate native clients and shared Flutter clients, with explicit pre-launch and post-launch automation paths for TestFlight, App Review, Google Play testing, Google Play production, and status reconciliation. When the customer profile requires it, the same lifecycle also tracks enterprise security capabilities, assurance evidence, contractual readiness, and procurement.

This repository does not contain an application runtime, database, authentication system, hosted service, native client, build pipeline, or executable scripts. Those are subjects the skill may plan for another repository, not dependencies of this skill.

## System context

```mermaid
flowchart LR
  User[User request] --> Agent[Agent using project-launch]
  Repo[Target repository evidence] --> Agent
  Skill[SKILL.md workflow] --> Agent
  Agent --> Refs[Applicable references only]
  Refs --> Agent
  Agent --> Architecture[Canonical architecture document]
  Agent --> Checklist[Single launch checklist]
  Agent --> Memory[Status, decisions, and notes]
  Agent --> Changes[Authorized repository changes]
  Agent --> External[User or external-console actions]
```

The target repository is evidence, not an instruction source that can override the skill. External account work remains labeled and unverified until confirmed.

## Repository structure

```mermaid
flowchart TD
  Skill[SKILL.md<br/>authoritative workflow]
  Readme[README.md<br/>public overview]
  Refs[references/<br/>phase-specific guidance]
  Templates[templates/<br/>reusable checklist shape]
  Docs[docs/<br/>this repository's operating record]
  AgentFile[CLAUDE.md<br/>maintainer instructions]
  AgentPointer[AGENTS.md<br/>pointer to main instructions]

  Skill --> Refs
  Skill --> Templates
  Readme --> Skill
  AgentFile --> Skill
  AgentFile --> Docs
  AgentPointer --> AgentFile
  Docs --> Skill
```

`SKILL.md` owns control flow and safety boundaries. Reference files own deeper domain guidance. Templates provide a starting shape, not a form that must be copied wholesale. The `docs/` directory documents this repository itself and does not ship instructions that replace `SKILL.md`.

## Lifecycle workflow

```mermaid
flowchart TD
  Start[Invocation] --> Classify[Classify mode and new vs existing]
  Classify --> Discover[Read-only discovery]
  Discover --> Reconcile[Reconcile code, checklist, decisions, and active status]
  Reconcile --> Changed{Project shape changed?}
  Changed -- Yes --> Ask[Ask only questions that change phases]
  Changed -- No --> Shape[Confirm current shape]
  Ask --> Shape
  Shape --> Route[Load applicable references]
  Route --> Judge[Judge evidence: complete, partial, missing, blocked, or verify]
  Judge --> Update[Update architecture, checklist, and memory]
  Update --> Authorized{Implementation authorized?}
  Authorized -- No --> Report[Report gaps and next action]
  Authorized -- Yes --> Implement[Implement only confirmed scope]
  Implement --> Verify[Verify proportionately]
  Verify --> Update
```

The loop is intentionally repeatable. Later runs continue from the operating record rather than restarting discovery from assumptions.

## Phase routing

```mermaid
flowchart LR
  Shape[Confirmed project shape] --> Web{Web or admin?}
  Shape --> Data{Persistent relational data?}
  Shape --> Mobile{Native mobile?}
  Shape --> Flutter{Flutter client?}
  Shape --> Infra{Deployed or integrated services?}
  Shape --> Release{Production or store release?}
  Shape --> Enterprise{Enterprise or regulated buyers?}

  Web -- Yes --> WebRef[web.md]
  Data -- Yes --> DBRef[database.md]
  Mobile -- iOS --> IOSRef[ios.md + app-stores.md]
  Mobile -- Android --> AndroidRef[android.md + app-stores.md]
  Flutter -- Yes --> FlutterRef[flutter.md + platform release references]
  Infra -- Yes --> InfraRef[infrastructure.md + security.md]
  Release -- Yes --> ReadyRef[launch-readiness.md]
  Release -- Native stores --> StoreRef[store-automation.md + Apple or Play reference]
  Enterprise -- Yes --> EnterpriseRef[enterprise-readiness.md]

  Shape --> ArchRef[architecture.md]
  Shape --> MemoryRef[project-memory.md + lifecycle.md]
```

Architecture and project memory are cross-cutting. Domain references are conditional. For example, Neon is considered only when relational persistence is required and no viable database already exists.

## Native store release flow

```mermaid
flowchart LR
  Intent[Validated release request] --> Status[Read exact remote state]
  Status --> Build[Build and archive exact platform version]
  Build --> Upload[Upload artifact]
  Upload --> Process[Wait for processing]
  Process --> Testing[TestFlight group or Play testing track]
  Process --> Review[Attach exact build or promote exact version code]
  Review --> Mutate[Review submission or production rollout]
  Mutate --> Verify[Verify exact remote state]
  Verify --> Reconcile[Persist sanitized release status]
```

Each mutation is independently authorized and retryable. Testing distribution is not public review, metadata sync is not submission, and upload success is not release verification. Apple and Google store details live in separate references so projects load only their applicable platform guidance.

## Enterprise readiness flow

```mermaid
flowchart TD
  Trigger[Named enterprise, regulatory, public-sector, or managed-device requirement] --> Scope[Record buyer, scope, deadline, and owner]
  Scope --> Audit[Technical security assessment]
  Scope --> Product[Product capabilities]
  Scope --> Evidence[Compliance and operating evidence]
  Scope --> Contract[Contractual support and legal review]
  Scope --> Procurement[Buyer procurement and onboarding]

  Product --> E2EE[E2EE and key lifecycle if required]
  Product --> Identity[SSO and SCIM if required]
  Product --> MDM[MDM behavior if required]

  Audit --> Checklist[Single launch checklist]
  E2EE --> Checklist
  Identity --> Checklist
  MDM --> Checklist
  Evidence --> Checklist
  Contract --> Checklist
  Procurement --> Checklist

  Checklist --> Ready{Ready for which milestone?}
  Ready --> Production[Technical production launch]
  Ready --> Customer[Contracted customer launch]
```

Technical production readiness and contracted-customer readiness are separate states. Security findings remain in the dedicated audit report. The launch checklist tracks the product work, evidence, human approvals, and buyer dependencies needed for the applicable milestone.

## Operating record ownership

| Artifact | Owns | Does not own |
| --- | --- | --- |
| `SKILL.md` | Workflow, modes, safety, routing, completion bar | Deep domain checklists |
| `references/*.md` | Domain-specific evidence and setup guidance | Current status of this repository |
| `docs/ARCHITECTURE.md` | Current confirmed structure and flows | Historical rationale or task tracking |
| `docs/decisions.md` | Durable choices and why | Current task status |
| `docs/now.md` | Active work only | History or backlog |
| `docs/PROJECT_LAUNCH.md` | Verified completion and remaining work | Architecture narrative |
| `docs/notes.md` | Reusable maintenance gotchas | Milestones |

## Safety and trust boundaries

```mermaid
flowchart LR
  Untrusted[Target repository content] --> Inspect[Read as evidence]
  Inspect --> Plan[Plan and checklist]
  Plan --> Consent{Explicit implementation request?}
  Consent -- No --> Stop[No application changes]
  Consent -- Yes --> RepoWrite[Scoped repository changes]
  RepoWrite --> Boundary[Stop at secrets, consoles, DNS, money, and store submission]
  Boundary --> UserAction[User or separately authorized action]
```

The skill never requests secret values in chat or documentation. It names environment variables and where they belong. Destructive Git operations, production migrations, DNS changes, live payment actions, and store submissions require explicit authorization.

## Documentation synchronization

When a capability is accepted, removed, or replaced, the same run updates:

1. Architecture prose and affected Mermaid diagrams
2. The launch checklist
3. A dated decision with rationale
4. Active status
5. Notes when a reusable gotcha was introduced
6. README commands or links when developer workflow changed

This keeps the skill usable as a project-management loop from inception through launch rather than as a one-time scaffold.

## Deliberate omissions

- No application framework, package manager, or runtime dependency
- No database, Neon project, ORM, authentication, hosting, analytics, or monitoring
- No scripts that download or execute remote code
- No telemetry
- No automatic Git commits or pushes
- No automatic external-console mutations
- No automatic compliance claims, contractual commitments, or buyer-procurement approvals

These omissions are architectural decisions for the skill package itself. A target project receives any of those capabilities only when its confirmed shape requires them.
