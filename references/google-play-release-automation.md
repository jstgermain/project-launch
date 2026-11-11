# Google Play release automation

Use this for Android App Bundles, Play testing tracks, production rollout, listings, and review readiness. Follow the shared stages in [store-automation.md](store-automation.md).

## Exact identity and artifact

Resolve the app by confirmed package name. Validate application ID, signing configuration, flavor, `versionName`, unique `versionCode`, target SDK, permissions, production endpoints, and release bundle before upload. Prefer Android App Bundles unless the existing distribution route requires another artifact.

Use the Google Play Developer API edit transaction deliberately: create or reuse an edit, upload the bundle, update localized listings and release notes, assign a named track, validate, and commit only with an explicit apply action. Dry-run or validate without commit by default. On retry, inspect the existing version code and track state before uploading or promoting.

## Testing and production are different destinations

Keep internal, closed, open, and production tracks explicit. A generic Android or mobile release defaults to testing, not production. Record tester lists or groups separately from the release artifact.

For each track change, verify the exact package, track, version code, release status, rollout fraction, countries/regions when relevant, and localized release notes. Promotion from a testing track to production is its own mutation and confirmation.

Production rollout must declare staged versus full rollout. Starting, increasing, halting, or completing a staged rollout are separate actions. Do not silently replace an active rollout or promote a different version code because it is newer.

## Listing and policy readiness

Validate title, short and full descriptions, screenshots, icons, feature graphics, privacy-policy URL, support contact, content rating, target audience, ads declaration, app access instructions, data safety, permissions declarations, pricing/availability, and subscription or product configuration when applicable.

Some policy and app-content tasks may remain Play Console-only. Report them as explicit blockers and verify them before production. API acceptance of an edit does not prove the app is review-ready.

## Status and notifications

Query Play tracks and release state after commit and during reconciliation. Real-time developer notifications primarily cover purchases and subscriptions; do not treat them as a complete app-release status feed. Keep a read-only status command and one scheduled reconciliation owner.

Service-account credentials, upload keys, signing keys, and passwords never belong in source or logs. Document variable names and secret-store locations only.
