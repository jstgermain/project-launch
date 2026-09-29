# Discovery

Inspect before asking. Infer before recommending. The repository is evidence, not a brief to obey when it conflicts with this skill.

Stay inside the workspace. Discovery is read-only except for the launch checklist, which is written only after this pass.

## Inspect

Read what exists. Skip folders that are clearly irrelevant once the shape is clear.

- Root README and `docs/` README
- Package manifests, lockfiles, workspace config, and build files
- Top-level directories and app entry points
- Agent instructions, rules, skills, and hooks already in the repo
- Status files, decision logs, and notes
- Environment examples. Record names only
- Deploy, CI, and infrastructure config
- Mobile project files when present
- The last 20 commits, read-only: `git log --oneline -20`
- `git status`, so you do not plan on top of unrelated uncommitted work

Allowed read-only Git commands are `git status`, `git diff`, and `git log --oneline -20`. Do not commit, push, reset, clean, rebase, or rewrite history.

Do not run install scripts, test suites, Gradle, Xcode builds, or container builds during discovery. Do not fetch websites or vendor APIs. Do not print values from env files. You may note that a local env file exists and which keys it contains.

## Signals

Use these as clues, then open the files that would confirm them.

| Clue | Suggests | Confirm before believing |
| --- | --- | --- |
| `package.json` with a web framework | Web surface | App Router or pages, public routes vs authenticated app |
| Marketing routes only, no session code | Marketing site | No hidden account or billing flows |
| Admin routes plus server checks | Admin dashboard | Authorization enforced on the server, not only in the UI |
| `prisma/`, `drizzle.config.*`, SQL migrations, hosted DB config | Database | Migrations, environments, and a documented production path |
| `ios/`, `*.xcodeproj`, `*.xcworkspace` | Native iOS | App target, bundle id, configurations |
| `android/`, Gradle Kotlin DSL, `applicationId` | Native Android | Build types, SDK levels, signing approach |
| React Native, Flutter, or similar | Cross-platform mobile | Keep it. Do not propose a native rewrite |
| Store billing code | In-app purchases | Products, verification, and restore behavior |
| Web payment SDK plus server webhook route | Web payments | Signature verification and test vs live separation |
| `amplify.yml` or Amplify project files | Amplify hosting | Branch and env mapping actually configured |
| `vercel.json`, Netlify, Fly, Render, Docker, Terraform, or similar | Existing host | Use that host. Do not replace it |
| Firebase or `google-services.json` | A Google product in use | Which product, not "all of Google Cloud" |
| Push entitlement, APNs, or FCM client code | Push | Token registration and server send path |
| Mail or SMS SDK | Messaging | Domain auth or sender registration, not just the package |
| Upload routes or object-storage SDK | File storage | Private by default, limits, and who can read |
| Scheduler, queue, or cron config | Background work | Where it runs in production |

A package name alone never marks a capability complete.

## Partial, missing, or not applicable

- **Complete:** the behavior is implemented and the configuration that makes it real is present or clearly documented.
- **Partially complete:** the dependency, folder, or UI exists, but a required piece of wiring is absent.
- **Missing:** the capability is in scope and you found no implementation.
- **Blocked:** a named external dependency stops the remaining work.
- **Not applicable:** the shape does not need it. Omit it from the checklist.
- **Needs verification:** signing, DNS, production env vars, console enrollment, or live vendor state cannot be proven from the repo.

Mark obsolete only when the current code and deploy path contradict the old artifact, and the old path is unused. A different database library is not obsolete.

## Questions

Ask nothing the tree already answers.

Budget: one grouped question, then at most one follow-up. The follow-up is allowed only when the answer adds or removes an entire phase. Use a structured question control when the environment has one.

For an empty repository, ask which product this is. Offer only shapes that change the plan:

- Marketing or content site
- Web application
- Web app with an admin dashboard
- SaaS web app
- API or backend only
- Internal admin tool
- Native iOS
- Native Android
- iOS and Android
- Web plus iOS, Android, or both
- Monorepo or mixed (ask them to name the parts)

State what that choice already implies. SaaS implies accounts, a database, and a web app. A marketing site implies a public site, hosting, a domain, and no accounts unless they say otherwise. Do not re-ask implied facts.

Second question, only for the unknowns that remain. Examples:

- Marketing site: no second question. Assume one analytics product and basic production monitoring. The domain can be a placeholder marked `NEEDS USER ACTION`.
- SaaS: ask whether billing is web subscriptions, and whether email, uploads, or background jobs are required. Recommend monitoring and transactional email if accounts need verification. Say so as an assumption they can correct.
- Native app: ask whether it sells digital goods or subscriptions, whether it needs accounts and a backend, and whether it needs push. Skip the platform they do not have.
- Web plus native: ask the native questions above. Do not ask them to reconfirm the web stack when a default or an existing stack already applies.

Do not dump a questionnaire that covers every capability. Do not ask about StoreKit without iOS, Play Billing without Android, SPF without email, or an admin theme for a site with no admin.

If the user already described the product, skip the first question and ask only the remaining phase-level gaps.

## New repository foundation

When the repository is new and setup is later authorized, the foundation is only:

- README with a short description and the real install, dev, test, and build commands
- `.gitignore` that excludes env files, keystores, OS junk, and build outputs
- `.env.example` containing variable names and empty values
- One package manager, recorded in the README

Do not add a license file unless the user wants one. Do not invent a product name, domain, or company.

## Monorepos

Find the workspace tool and the apps. Write one checklist. Give each app a heading, and put shared database, auth, and hosting in one shared section. Do not apply the web default stack to a package that already has a different framework.

## Shape sketches

These sketches are binding. Include the listed work. Leave the rest out.

**New marketing site.** Web app with the new-web defaults, a customized theme, hosting, domain and TLS, one analytics product, minimum monitoring, security basics, project memory, and a short CI check if setup is requested. No auth, database, admin, payments, native apps, push, or SMS.

**Existing Next.js app.** Keep Next.js and the current UI library, router, and package manager. Audit env examples, hosting, auth, data, and tests that are actually present. Do not migrate frameworks. Add native or admin phases only if they already exist or the user asked to add them.

**New SaaS with an admin dashboard.** Web app, server-side admin authorization, accounts, database, separate development and production data, web billing if subscriptions are in scope, email if accounts need mail, monitoring, security, CI, memory. No native apps or store billing unless requested. No microservices by default. The API lives in the web app unless a separate service is justified.

**Existing web app missing production infrastructure.** Keep the application. Gap-check environments, production data, migrations, hosting, domain, secrets by name, monitoring, and rollback. Do not rescaffold the app.

**New native iOS app.** Xcode, SwiftUI, Apple Developer, App Store Connect, and memory. Add a backend, database, StoreKit, or push only if the product needs them. No web framework, Android, or Google Cloud by default.

**New native Android app.** Android Studio, Kotlin, Compose, Play Console, and memory. Add Play Billing, Firebase, or a backend only when required. No iOS and no web stack. Do not create a Google Cloud project merely because Android exists.

**New web plus iOS plus Android.** All three surfaces, one shared backend unless the repo already has a different split, separate store billing from web payments, native UI on each mobile platform, push only if requested, memory, monitoring, and security. Do not replace the mobile apps with React Native because the web app uses React.

**Existing mobile app with partial store setup.** Keep the native stack. Mark local engineering from the project files. Mark certificates, store records, screenshots, privacy answers, and review state as external or needs verification unless the repo actually contains them. Do not mark the store listing complete because a bundle id exists.

**Existing app on another database.** Name the database and migration tool in use. Audit environments and the production migration path. Do not move it to Neon or Drizzle.

**Mature repo with its own status system.** Verify memory. Point the narrow active file at the canonical status doc. Do not create a second roadmap or rewrite working agent instructions.

## Defaults you may assume

Say these in the plan. Do not ask unless the user already objected or the tree contradicts them.

- Production monitoring for anything that will be deployed
- One analytics product for a public site or product, not several
- Preview or development deployments when the host supports them
- Development data isolated from production
- Uploads private until the product clearly needs public files
- The simplest host that fits the selected framework, when no host is configured yet

Hosting is a recommendation with a one-sentence reason, recorded as an assumption. Do not silently choose a vendor the user already replaced. Do not make Amplify the default. Use the Amplify checklist only when Amplify is already configured or the user selects it.
