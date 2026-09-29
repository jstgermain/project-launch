# Security

Security is part of the launch plan. It is not a pile of invented vulnerabilities.

If the repository already contains a security-audit skill, a `docs/security-audit.md` report, or another security-audit workflow, use that workflow for findings. Record a checklist pointer to it. Do not run a second, competing audit or restate its findings as if this skill discovered them.

If no security workflow exists, record the launch tasks below that match the shape. Report a defect only when you can point at it. Absence of a scanner is a gap in tooling, not proof of a vulnerability.

## Secrets

- `.gitignore` ignores `.env` and local secret files. `.env.example` lists names and empty values
- No committed private keys, keystores, payment secrets, or connection strings
- Production secrets live in the host or CI secret store. The checklist names the variables
- Never ask the user to paste a secret into chat or into a markdown file
- If you find a likely real secret, report the path and the type, and recommend rotation. Do not print the value. Deleting the file does not make an exposed credential safe

You may confirm which keys exist. You may not quote the values.

## Checks that match the shape

Use only the rows that apply.

| Area | What "done" means |
| --- | --- |
| Dependencies | The project has a lockfile and a documented audit or update path. A clean audit is `NEEDS VERIFICATION` until someone runs it. Do not run an installer during discovery to find out |
| Authz | Protected data and admin actions are checked on the server |
| Client boundary | Privileged credentials are not shipped to the browser or the mobile binary |
| Database | The app role is not a superuser, and production is not the local default |
| Uploads | Type and size limits exist, and private files are not world-readable |
| Webhooks | Inbound webhooks verify signatures |
| HTTP | Public web apps use HTTPS. Security headers are configured where the host or framework allows. Do not call a missing optional header a breach |
| Rate limiting | Login, password reset, and other abuse-prone routes have a limit when those routes exist |
| Least privilege | Cloud and store credentials used by CI can do the deploy, not everything in the account |
| SAST | Optional. If a scanner is already configured, keep it. Do not add three scanners to a new repo |

## Existing tooling

Note Dependabot, Renovate, CodeQL, or a dependency audit workflow when you see it. That is evidence. Do not replace it.

## Out of scope

Do not claim the application is secure because the checklist is complete. Do not label the project compliant with a regulation or a store policy. Do not exploit a suspected issue. Do not add attack procedures, payloads, or proof-of-concept code.

When a formal security review is warranted and no security skill is present, say so as a recommendation. Do not pretend this checklist was that review.
