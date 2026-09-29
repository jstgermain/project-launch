# App stores and store billing

Load this when an iOS or Android app is in scope. Skip the platform that does not exist. Local project health is judged in the iOS and Android references. This file is the console, listing, review, and digital-goods billing work.

Most items are `EXTERNAL CONSOLE` or `NEEDS USER ACTION`. Do not mark them complete from a bundle id or package name. Do not submit an app for review unless the user explicitly asks in the current session.

Policy-sensitive billing is `NEEDS VERIFICATION`. Do not fetch vendor policy pages. Do not tell the user that a web payment provider satisfies store rules.

## Apple Developer and App Store Connect

Include for native iOS:

- Apple Developer Program membership
- App ID, capabilities, and identifiers matching the Xcode target
- Sign in with Apple when the iOS app offers third-party social login. Confirm the current platform rule before shipping. Mark it `NEEDS VERIFICATION` rather than treating it as legal advice
- App Store Connect app record, bundle id, and SKU
- Name, subtitle, categories, age rating
- Privacy policy URL, support URL, and marketing URL when the product has a site
- App privacy disclosures that match actual data collection
- Screenshots and preview video only if the listing uses video
- Review contact and demo-account notes, with no real customer password written into the repo
- TestFlight internal testing, then external testing when the product needs it
- Review submission and phased release only when the user wants a phased rollout

Certificates and profiles that must be created in the portal stay external. Associated-domain and push setup on the App ID must match the entitlements in the repo. A mismatch is partially complete.

## StoreKit

Include only when the iOS app sells digital subscriptions or digital functionality.

Account for products, a subscription group when subscriptions exist, the entitlement model, a StoreKit configuration for local testing, transaction verification, restore purchases, subscription state, grace periods when the product uses them, server notifications when the backend tracks state, sandbox testers, and the production catalog.

Verification of transactions belongs on a backend the client does not fully trust when the product has a backend. A client-only flag is not an entitlement system.

Physical goods and services can fall outside in-app purchase. Digital features generally do not. When the category is unclear, stop and mark the payment architecture `NEEDS VERIFICATION`. Never document web checkout as the way an iOS app sells digital access.

## Google Play

Include for native Android:

- Play Console developer account
- Application record and package name matching `applicationId`
- Store listing, category, and content rating
- Data safety form matching actual collection
- Privacy policy URL
- Screenshots and a feature graphic
- Internal testing, then closed testing. Open testing only if the user wants it
- Production track and staged rollout when they are ready to release that way
- Play App Signing enabled through the console, with the upload key kept private

## Play Billing

Include only when the Android app sells digital subscriptions or digital functionality.

Account for products, subscriptions, base plans, offers, purchase acknowledgement, entitlement validation, restore behavior, subscription state, backend verification when a backend exists, license testers, and internal testing of purchases.

The same policy caution as StoreKit applies. Do not reuse the web payment design inside the Android app when Play Billing is required. Mark unclear cases `NEEDS VERIFICATION`.

## Shared products

If both stores sell the same subscription, the checklist should say how entitlement is decided: each store is the source of truth for its own transactions, and the backend should not grant digital access from a web payment when store rules require store billing. Do not invent a legal conclusion. Flag the cross-platform entitlement design for verification.

## Evidence

| Observation | Status |
| --- | --- |
| Fastlane metadata or a committed listing directory matches the current app | Listing source complete for those fields. Console publish still needs verification |
| Bundle id set, no listing copy, no privacy URL | Store setup missing or partial |
| Billing client library present, no restore path and no server verification | Partially complete |
| Sandbox or license-test proof | Needs verification unless the user confirms it |
