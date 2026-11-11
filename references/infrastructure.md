# Infrastructure

Load the sections that match the shape. Skip the rest. Do not create vendor accounts while planning. Console and account work is `EXTERNAL CONSOLE` or `NEEDS USER ACTION`.

This skill never creates charges, moves funds, or sends real messages to customers.

## Hosting and deployment

Include for anything that is deployed.

Account for hosting, CDN or the host's edge, TLS, environment variables, custom domain when the product is public, preview and production deployments, server rendering and server functions when the framework needs them, static assets, image delivery, secret storage, logs, monitoring, and rollback.

Judge the existing platform from its config. Replace it only if the user asks.

When Amplify is selected or already used, check the repository artifacts and then mark console state `NEEDS VERIFICATION`:

- Amplify application
- Branch to environment mapping
- Build configuration
- Environment variables by name
- Domain connection and TLS
- Distribution behavior, such as CloudFront, where the product uses it
- Deploy permissions
- Development, staging, and production separation when the product needs more than one environment

A build spec file does not prove the hosted application exists.

When no host exists, recommend one and explain why in a sentence. Do not offer a menu of three hosts and stall. Do not default to Amplify.

## Domains and DNS

Include for a public product.

Account for domain ownership, DNS host, TLS, redirects, one canonical hostname, and the verification records the host or other vendors require.

The canonical website host includes `www`: `https://www.example.com`. Use that host in scripts, app config, canonical tags, sitemaps, environment examples, and any URL the skill writes.

Omit `www` only in these cases:

- The user specifies a different host.
- The repository already documents a different canonical host. Keep it.
- Another subdomain stands in for `www`, such as `app.example.com`, `api.example.com`, or `staging.example.com`. Use that subdomain as given. Do not write `www.app.example.com`.

Send `https://example.com` to `https://www.example.com` when `www` is canonical. Do the same for plain HTTP. Do not add `www` to localhost, a host the platform assigns for previews, or a vendor API endpoint.

Include SPF, DKIM, and DMARC only when the product sends email.

Do not change DNS unless the user explicitly asks. Live records are `NEEDS VERIFICATION` unless you were asked to inspect them and could do so without guessing.

## Environments

Where the product has more than one, distinguish local, development, preview, staging, and production. The checklist should show which database, auth client, payment mode, and API base URL belong to which environment.

Use names such as `DATABASE_URL`, `STRIPE_SECRET_KEY`, `APPLE_TEAM_ID`, and `GOOGLE_CLIENT_ID`. Never write real values. Do not reuse production credentials for local development unless the user explicitly accepts that risk.

## Authentication

Include only when users sign in.

Decide the provider from the product, or keep the provider already integrated. Record which methods are required: email and password, magic link, passkeys, Google, Apple, other social sign-in, MFA, recovery, and verification.

Account for session strategy, profile storage, role checks, and admin checks. Authorization for protected data is enforced on the server.

For an iOS app that offers social login, include Sign in with Apple as a requirement to verify against current platform rules.

Do not add auth to a marketing site that does not need accounts.

## File storage

Include only when users or admins upload files.

Choose a provider, or keep the one already used. Account for private versus public objects, upload permissions, signed URLs for private files, size limits, MIME checks, malware concerns appropriate to the product, image processing only if required, retention, deletion, backups, and CDN delivery for public assets.

Default to private. Public objects need an explicit product reason.

Do not commit bucket credentials. Document the variable names.

## Payments

Include only when the product takes payments. First classify them: physical goods or services, SaaS subscriptions, digital content, mobile in-app purchases, marketplace payouts, one-time payments, or recurring billing. The class changes the provider.

Web payments may use a provider such as Stripe when the product is allowed to take payment on the web. Plan for an account, test mode, live mode, products, prices, checkout, signed webhooks, a customer portal when subscriptions need self-service, refunds, taxes if they apply, failed payment handling, cancellation, and reconciliation. Live mode and tax configuration are external. Webhook signing secrets are variable names.

Native digital goods are planned in the app-store reference, not by reusing web checkout.

Do not call payment APIs to create live charges or move money. Implementing a checkout flow during authorized setup uses test-mode keys supplied through the environment, never keys pasted into chat or committed in docs.

## Email

Include only when the product sends transactional or marketing email.

Identify the provider, sending domain, SPF, DKIM, DMARC, templates, unsubscribe handling for marketing mail, bounce handling, separate test and production credentials, variable names, and rate limits.

Auth mail is a reason to include email. A brochure site is not.

## SMS

Include only when the product sends SMS.

Account for provider, sender number or messaging service, consent, opt-out handling, templates, rate limits, destination-country limits, variable names, and registration or approval the provider requires before production traffic.

Regulatory details are `NEEDS VERIFICATION`. Do not guess that a design is compliant.

## Push

Include only when the product sends push notifications.

iOS: APNs, the push entitlement, permission UX, device token registration, and a server send path.

Android: Firebase Cloud Messaging, a Firebase project and app, `google-services.json` handled without copying its keys into docs, token registration, notification channels, and a server send path.

If both apps exist, one backend owns delivery. Firebase is in scope because FCM needs it, not because Android exists.

## Analytics

Include when the user wants analytics or the product is a public site or SaaS and they have not refused it.

Pick one product that covers the need. Do not add a second analytics SDK "as well". Separate development from production so local traffic does not look like customers. Account for privacy and consent when the product collects more than anonymous operational metrics. Consent rules are `NEEDS VERIFICATION`, not a legal opinion.

## Monitoring

Production applications get the smallest set that will wake a human: error tracking, enough logs to debug a failed request, and an uptime check on the public URL when there is one. Add mobile crash reporting when there is a mobile app, and database or API checks when those exist.

Do not design a multi-vendor observability platform for a new product. Name where alerts go. The destination address or on-call rotation is `NEEDS USER ACTION` if unknown.

## Background jobs

Include for scheduled or queued work the product actually needs. Prefer the web host's scheduler or a single worker over a new queue cluster. Document how a job is invoked in production and how it authenticates to the database. A route with no authentication is not a cron endpoint.

For external lifecycle state, prefer a signed event when the vendor provides the right event and keep a bounded reconciliation job for missed delivery. Make both paths idempotent and scope them to the exact external identifier. A scheduled release-status job should first check whether the product has a pending version and exit before making vendor API calls when it does not.

Do not mistake billing notifications for app-publishing notifications. Do not add a backend solely to receive a webhook when an existing CI schedule can reconcile a static product's small amount of public state.

## CI

Software projects should consider CI once there is something to build. A useful minimum is install, lint, typecheck, test, and build, using the commands the project already has. Add a migration check when the database has committed migrations. Add native build validation only when a native app is in scope and the team is ready to maintain those runners.

## Safe release orchestration

Include this when the repository deploys more than one surface. Preserve the existing CI provider and release scripts; make the pipeline the authoritative orchestrator instead of duplicating release logic in workflow YAML.

- Every production deploy depends on the applicable build and test jobs. A failed prerequisite stops the release. Do not use `always()` or a permissive condition that turns failure into an intentional skip.
- Model each destination explicitly: web, API, iOS TestFlight, iOS App Review, Android internal testing, and Android production. A convenience mobile target may mean both testing tracks, but must never silently mean public review.
- When an API deploy is selected in the same run, web and mobile releases that use that API wait for the API deployment and its live health check. A failed or unhealthy API blocks downstream release jobs.
- When the API is intentionally not selected, a UI-only web or mobile release may proceed after shared checks. Express this as "API succeeded or was not requested," never "API failed or skipped."
- A web-only marketing deploy may proceed without an API deployment when the changed surface does not require one, but it still waits for the repository's web gates.
- Public store releases fail closed when signing or store credentials are missing. Internal testing may be an intentional no-op only when the repository explicitly documents that behavior.
- Keep concurrency controls per destination so a second release cannot cancel a store upload or production deployment already in progress.
- Keep screenshots and listing metadata as committed or deterministically generated CI inputs. Validate them before submission; do not depend on CI capturing simulator artwork during a release.

Load [store-automation.md](store-automation.md) when native store automation is applicable.

Do not build a release factory before the project needs it. Do not add a second CI system beside one that already works. Signing secrets stay in the CI secret store, referenced by name.

## Google Cloud and Firebase

Include a Google service only when a feature needs it: Maps, Places, Google sign-in, FCM, Play Developer API access, or an existing Firebase product.

Possible tasks, used only when that service is required: Cloud project, OAuth consent screen, OAuth client, service account, enabled APIs, Firebase app, Secret Manager, Cloud Storage, functions, and billing account. Each unused service stays out.

Play Console does not require a Cloud project for a simple listing. Android publisher API access is a separate, explicit need.

## Testing

Judge the test setup the repository already uses. Do not replace it or add a second runner.

For a new project, during authorized setup, add the test tool the chosen framework scaffolds and a small test that proves the runner works. Do not demand end-to-end coverage for a new marketing site. Add API or integration tests when there is a backend worth protecting. Mobile UI tests are optional until a flow is stable.

Levels to consider, then cut to what the shape needs: unit, integration, API, component, end-to-end, iOS, Android.
