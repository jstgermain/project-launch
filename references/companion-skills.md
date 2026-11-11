# Companion skills

Offer these skills during a project-launch run. They are optional. Install one only after the user agrees in the current session. Install no other skill from the network.

| Skill | Offer when | Skip when |
| --- | --- | --- |
| [security-audit](https://www.skills.sh/creative-lid/security-audit/security-audit) | The project has application code, this run will create it, or enterprise/security-review readiness is in scope | The checklist already records a decline |
| [improving-code-quality](https://www.skills.sh/creative-lid/improving-code-quality/improving-code-quality) | The repository already contains application code, or the user asked to set up or add a surface | The tree is still empty and this run is plan-only |
| [web-presence-audit](https://www.skills.sh/creative-lid/web-presence-audit/web-presence-audit) | The shape includes a public website or public web app | API-only, native-only, or an internal tool with no public pages |

A skill counts as installed when it is already available in this session, listed in the project's `skills-lock.json`, or present under the project's `.agents/skills/`, `.cursor/skills/`, or `.claude/skills/` directory. Do not search outside the workspace.

## Ask

If every applicable skill is already installed, use those and do not ask.

Otherwise ask once which missing skills to install and include. Use a structured multi-select when the environment has one. Include a "none" choice. List only the applicable skills that are not installed.

If the user already named one of these skills in the request, treat that as agreement. Do not ask again for that skill.

Record the result on the launch checklist: installed and included, or declined. A later run does not ask again about a declined skill unless the user brings it up.

## Install

Run the install from the target project root. Prefer the `skills` command when it is already available. Otherwise use `npx skills` with no version tag. Do not pipe a download into a shell. Do not add `-g`.

```bash
skills add https://github.com/creative-lid/security-audit --skill security-audit -y
skills add https://github.com/creative-lid/improving-code-quality --skill improving-code-quality -y
skills add https://github.com/creative-lid/web-presence-audit --skill web-presence-audit -y
```

Run only the lines the user agreed to. After the command finishes, read that skill's local `SKILL.md`. Do not fetch the remote skill file yourself.

## How they join the run

Finish the launch checklist, then run each included skill on its own slice.

- **security-audit** owns technical security findings and remediation verification. Keep its report. Do not restate those findings as if this skill discovered them. `project-launch` still owns enterprise capability planning, evidence dependencies, contracts, and procurement status.
- **web-presence-audit** owns public SEO, sharing, discovery, security headers, and accessibility. Use it instead of inventing a second web-presence pass.
- **improving-code-quality** owns maintainability findings. It does not decide product shape, infrastructure, or store readiness.

On a plan, audit, or readiness run, companion skills report only. They do not change application code.

On setup, extend, or prepare, a companion skill may edit files only inside the scope the user already authorized, and only when that skill's own rules allow implementation.

If the user installs a skill but the tree has nothing for it to inspect yet, leave it installed and add a checklist item to run it once that code or those pages exist. Do not invent findings from an empty tree.
