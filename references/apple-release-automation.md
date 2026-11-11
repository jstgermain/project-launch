# Apple release automation

Use this for iOS, macOS, TestFlight, App Store versions, App Review, and Apple growth assets. Follow the shared stages in [store-automation.md](store-automation.md).

## Exact identity and build selection

Resolve the App Store Connect app by confirmed app ID or bundle ID. Select builds by exact platform, marketing version, and build number. Never attach the newest build by timestamp when multiple platforms or release candidates exist. Wait until the build is processed and valid before distribution or review attachment.

Keep iOS and macOS versions/builds explicit even when they share Flutter code. Validate the archive's bundle ID, version, build number, signing team, entitlements, minimum OS, and production endpoint before upload.

## Signing and certificate hygiene

- Prefer a stable distribution-signing strategy appropriate to the project. Do not create a new development certificate on every CI run.
- Use a temporary CI keychain, import only the required signing material, and delete the temporary keychain after the job.
- If automatic signing with an App Store Connect API key creates certificates or profiles, query existing resources first and reuse valid ones where possible.
- Treat Apple certificate quota errors as lifecycle failures. Classify certificates by type, owner, and issuer before revocation.
- Revoke only expired or clearly automation-created development certificates that the current release no longer needs. Preserve distribution certificates, Developer ID certificates, personal developer certificates, and unknown assets unless the user explicitly authorizes their removal.
- Make cleanup bounded and auditable. A cleanup command reports what it would revoke before apply, rechecks immediately before mutation, and verifies capacity afterward.
- Never store `.p8`, `.p12`, passwords, profiles, or keychain contents in the repository or logs.

## TestFlight

TestFlight preparation may upload a build, wait for processing, update beta app details, update What's New or What to Test, and assign internal or external groups. It does not attach the build to an App Review version unless that separate stage is requested.

Verify the exact build appears in each requested group and that localized beta notes, review contact, export-compliance state, and required beta review information are present. External testing may require Beta App Review and is not equivalent to App Review.

## App Review

Keep these separate:

1. upload listing and review metadata
2. create or select the exact app version
3. attach the exact processed build
4. Add for Review
5. final Submit for Review
6. verify Waiting for Review or In Review

`Ready for Review` means final submission did not occur. Preserve any version already in review. Before creating a new request, query App Store Connect for active review items. Interactive automation may offer explicit one-run cancellation/replacement or no new submission; CI fails closed without that confirmation and rechecks immediately before mutation. Withdrawal or replacement is never a fallback for screenshots, growth assets, or a conflicting build.

Record review notes, contact data, demo-account requirements, encryption/export-compliance answers, privacy declarations, age rating, content rights, pricing/availability, and release mode as validated inputs. Treat fields that still require App Store Connect UI work as external-console blockers.

## API and browser boundaries

Use App Store Connect APIs for supported metadata, builds, beta details, groups, review items, and status. Use headed browser automation only for a documented API gap and only with a saved user-controlled session. Browser automation defaults to audit/read-only, uses stable labels and observed IDs, and takes evidence screenshots without exposing credentials.

After every mutation, query App Store Connect again and verify the exact resource and state. A successful `xcodebuild -exportArchive` or upload command alone is not proof of TestFlight distribution or review submission.
