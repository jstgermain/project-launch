# Project memory

Every repository is evaluated for a lightweight memory system. The goal is a one-minute briefing an assistant can trust, plus a place for current work, durable decisions, and reusable gotchas.

This is a checklist item named **Initialize or verify project memory**. Writing the files is implementation. In plan, audit, and readiness modes, record the gap. Create or edit memory files only when memory setup is requested or an authorized setup pass includes it.

## Learn the repository first

Before writing memory files, read:

- Root README
- `docs/` README if present
- Package and build files
- Workspace configuration
- Top-level structure
- Existing agent instructions and rules
- Project status files, decision logs, and notes
- Hooks, skills, voice or writing rules, and Git rules
- The last 20 commits, read-only

Look especially for `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `.cursor/rules/`, `.cursor/hooks/`, `.cursor/skills/`, `docs/PROJECT_STATUS.md`, `docs/now.md`, `docs/decisions.md`, and `docs/notes.md`.

Never guess project facts. Never overwrite useful content. Integrate with the system that already exists.

Commit subjects are hints. Do not turn them into decision-log entries unless the code, docs, or the user confirms the decision.

## Choose the main instruction file

Use the file that is already the real source of agent instructions.

1. Existing `CLAUDE.md` when that is the established instruction file.
2. Existing `AGENTS.md` when that is the established instruction file.
3. Otherwise create `CLAUDE.md`.

If both files contain real instructions, do not merge them silently. Prefer the one the other file, the README, or the rules already point to. If they conflict and neither is canonical, ask which file wins.

The other filename, if it exists or is expected by the user's tools, should only point at the main file:

```markdown
# Agent instructions

Project instructions live in CLAUDE.md. Read that file.
```

Do not keep two copies of the same rules.

## Main file contents

Keep it short enough to read in about a minute. Preserve unique facts that are already there. Add a section instead of replacing a useful file. A stub may be rewritten into this shape.

Include:

- A short description of what the project is
- Real install, dev, test, and build commands, or a pointer to the README that owns them
- Key conventions
- Important gotchas, or a pointer to `docs/notes.md`
- Git rules: do not commit, push, force-push, or rewrite history unless the user asks in the current session. If asked, write a normal commit message with no `Co-authored-by` trailer and no mention of an AI assistant
- A pointer to the voice or writing rule, when one exists
- The session habit below

Do not paste secrets, customer data, or machine-specific paths.

## Session habit

The main file must tell assistants and developers to:

- Read current memory and status at the start of work
- Update decisions when a decision is made
- Update notes when a reusable gotcha is discovered
- Keep the active-status file accurate
- Update an existing project-status system through its own mechanism
- Avoid a second source of truth

Use this wording when you are adding the habit and the repo does not already state it:

```markdown
## Project memory

At the start of a task, read this file and the active status.
When a durable decision is made, record the date and why.
When a reusable gotcha appears, add it to the notes.
Keep active status short and current. Rewrite it instead of appending history.
If a broader status document exists, update that document and keep the active file as the narrow slice.
Do not create a second system for the same facts.
```

## Active status

`docs/now.md` contains only active work. Keep it short. Rewrite it when the current work changes. Do not append a running diary.

If `docs/PROJECT_STATUS.md` or another file is already the canonical handoff, leave that file in charge of milestones. `docs/now.md` stays a narrow slice and points at the broader status. Never create two milestone systems.

If `docs/now.md` already mixes history and current work, move confirmed durable facts to the decision log and confirmed gotchas to the notes before rewriting. If you cannot tell where a fact belongs, leave it and add a checklist item to sort it. Do not delete it.

## Decisions

`docs/decisions.md` holds durable decisions and why they were made. Dated entries. Newest first.

Seed it only from decisions you can confirm in the code, the docs, or the user's request. A new project's accepted stack choices qualify after the user accepts the plan. Do not fabricate history from an empty repository.

When a decision file already exists under another name, keep using it. Point to it from the main instruction file instead of creating `docs/decisions.md`.

## Notes

`docs/notes.md` holds gotchas worth remembering: migration behavior, deployment quirks, environment traps, build oddities, hook behavior, Git policy, voice-rule location, and third-party integration quirks.

Prefer a pointer when the detail already lives in the README or a runbook. Do not copy a second full copy.

## Voice and writing rules

If the repository has a voice, style, or writing skill or rule, follow it for user-facing copy and mention it from the main instruction file or the notes. Do not create a new voice rule when one already exists. Do not invent one when the project has none.

## What not to store

- Secret values, tokens, or connection strings
- A second launch checklist. Launch tracking stays in the launch checklist
- A second roadmap when project status already exists
- Speculation about unconfirmed product history

## Audit judgment

| Evidence | Status |
| --- | --- |
| Main instructions exist, are short, and point at current status, decisions, and notes | Complete |
| Instructions exist but status, decisions, or the session habit is missing | Partially complete |
| No agent instructions and no status docs | Missing |
| Two files disagree about the same rules or milestones | Partially complete, until one is chosen as canonical |
| Files exist but you have not read them | Needs verification |
