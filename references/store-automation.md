# Native store automation

Use this in Prepare mode for TestFlight, App Review, Google Play testing or production, store listings, screenshots, growth assets, or post-submission status reconciliation. Load [apple-release-automation.md](apple-release-automation.md) for Apple targets and [google-play-release-automation.md](google-play-release-automation.md) for Android.

## Start with an inventory

Reuse working automation before adding another release system. Inventory:

- application IDs, bundle IDs, package names, platforms, flavors, schemes, and tracks
- where marketing versions, build numbers, `versionCode`, and `versionName` originate
- listing metadata, localized release notes, screenshots, privacy/data-safety answers, review notes, demo credentials, TestFlight notes, tester groups, and Play tracks
- archive, export, upload, processing, distribution, review, rollout, and verification commands
- credentials by variable name and runtime location, never value
- every CI workflow, scheduler, webhook, and backend job that can mutate or reconcile store state

Do not add a second manifest or competing command family when the repository already has a clear source of truth.

## Release request contract

When no equivalent exists, create a checked-in release request or manifest that declares intent without containing secrets. It should identify:

- schema version, request ID, creation time, owner, and draft/requested/completed state
- destination: TestFlight, App Review, Play internal/closed/open testing, or Play production
- selected platforms and exact app identifiers
- per-platform marketing version and build number or `versionCode`
- localized What to Test, What's New, and release notes sources
- tester groups or Play track, phased release or rollout percentage, and release mode
- whether metadata sync, upload, review attachment, submission, or rollout is requested
- an explicit confirmation token for review submission, replacement/withdrawal, or production rollout

The manifest is an auditable request, not authorization by itself. Validate it against a schema before any network mutation. Reject ambiguous destinations such as `mobile` or `deploy all` unless the command resolves them to named store stages.

## Command and stage boundaries

Fit names to the repository, but preserve these independently invokable stages:

1. `validate`: local schema, metadata, assets, version consistency, privacy, and credential-name checks
2. `status`: read-only remote state for the exact app, platform, version, build, groups/tracks, review state, and rollout
3. `sync-metadata`: listing and review metadata only
4. `build` or `archive`: produce the platform artifact
5. `upload`: upload the artifact without silently submitting it
6. `wait`: wait for processing and fail on invalid or expired artifacts
7. `distribute-testing`: TestFlight groups or Play testing track
8. `attach-review`: attach the exact processed build to the intended version
9. `add-for-review`: create or update the review item
10. `submit-review`: final App Review submission
11. `promote` or `rollout`: Play track promotion or production rollout
12. `verify`: query remote state and prove the intended result
13. `reconcile`: persist observed release state for the product or operations surface

Validation, status, and dry-run are the defaults. Mutating stages require an explicit apply flag. Final review submission, cancellation/replacement, track promotion, and production rollout require separate one-run confirmation. A broad request may authorize several named stages, but automation must still log and verify each boundary.

## Pre-launch and post-launch

Pre-launch automation establishes app records, identifiers, signing capabilities, listings, screenshots, privacy/data-safety content, review contact and demo access, tester groups/tracks, pricing/availability, and the first processed build. It exposes console-only gaps instead of pretending they are complete.

Post-launch automation increments platform versions/builds, generates or validates localized notes, uploads the exact artifact, preserves active reviews, distributes testing builds, promotes tracks, verifies processing and review state, and reconciles the result. A release script must be safe to retry after an interrupted upload or partially completed run.

## CI reliability

- Use a dedicated manual release workflow with a required target/destination input. Keep verification and reconciliation available as read-only targets.
- Use release concurrency that prevents overlapping mutations. Do not cancel an in-progress store upload merely because a newer workflow started.
- Pin toolchains and CI actions. Select Xcode, SDK, Flutter, JDK, and Gradle versions that satisfy current store requirements.
- Check exact build-number or `versionCode` uniqueness before building or uploading.
- Make uploads idempotent where vendor APIs allow it. On retry, inspect remote state before creating a new version, certificate, profile, edit, or review request.
- Gate store work on shared checks, native validation, and any required live API health check. An intentionally app-only release may proceed only when its backend compatibility is already verified.
- Wait for asynchronous processing, then verify the exact version/build and requested destination. An HTTP 200 from an unrelated API is not store-release evidence.
- Persist a sanitized audit summary: request ID, commit, platform, version/build, artifact checksum when available, remote resource IDs, destination, result, and timestamp.
- Fail closed on missing credentials, failed processing, unresolved review conflicts, invalid privacy metadata, or inability to verify the result.

## Status ownership

Store status is remote state, not a webhook-only event. Choose one authoritative reconciliation path and one scheduler. App Store server notifications and Google real-time developer notifications do not provide a complete release-status feed. Poll the store APIs on a bounded cadence and keep a manual reconciliation command. Do not run duplicate pollers in CI, the application host, and the database platform.

## Growth assets

Apple Custom Product Pages, Asset Library items, and Product Page Optimization are related to release automation but do not own the app-version release flow.

- Keep growth validation, status, screenshot sync, and headed audit commands separate from release submission.
- Store Custom Product Page, editable version, and localization IDs separately.
- Copy the current Ready for Distribution page as the screenshot baseline.
- Require at least one valid PNG per configured source directory. Add missing screenshot sets only with an explicit apply flag, resizing in memory without deleting or replacing existing sets.
- Attach creative assets to their parent review item. Refuse duplicate standalone-asset submissions.
- Product Page Optimization needs its own explicit start flag and approved baseline/assets.
- Growth automation must never attach, replace, withdraw, or submit an app version as a fallback.

Never print private keys, tokens, certificates, profiles, or demo passwords. Keep credential files ignored and document variable names and configuration locations only.
