# Native Android

Load this only when the product has, or the user is adding, a native Android app.

If the repository already uses a cross-platform toolkit, keep it and audit that project. Do not rewrite it in Kotlin unless the user asks.

For a new Android app, use Kotlin and Jetpack Compose. Do not choose a cross-platform toolkit because the web app uses React.

Play Console, Play App Signing, and Play Billing are judged with the app-store reference. A Gradle module does not make the store listing complete.

Google Cloud and Firebase are not implied by Android. Add them only for a product requirement such as FCM, Google sign-in, or Maps.

## Local engineering

Account for:

- Android Studio project, Gradle wrapper committed, Kotlin version visible in the build
- `applicationId` / namespace
- `minSdk` and `targetSdk` set deliberately, not left as an unexamined sample
- Debug and Release build types
- Development versus production configuration when the app calls a backend. Build types or flavors are both fine. Match the project
- Secrets out of the repo. Local properties or env names that Git ignores. No store passwords in Gradle source
- JDK version recorded in the README or toolchain file

## Signing

Release signing must not commit the upload keystore or its passwords.

Checklist:

- Upload key created and stored by the user, outside the repository
- Play App Signing noted as a console step
- Release build reads credentials from a local file or environment variable names
- `.gitignore` covers keystores and local signing properties

If a keystore or password is already committed, report the path and the secret type. Do not open the keystore or copy the password. Recommend rotation. Removing the file from the branch does not unexpose it.

## Evidence

| Observation | Status |
| --- | --- |
| Application id, SDK levels, debug and release, env split, signing config references names only | Local engineering complete |
| Sample `applicationId`, no release build type, or passwords in Gradle | Partially complete |
| User asked for Android and no module exists | Missing |
| Play signing and store listing | Needs verification |

Do not run Gradle during discovery. During an authorized prepare pass, run a release build only when the user asked to verify it.

## New-app minimum

When setup is authorized, create a Compose app using the application id the user provided, or a placeholder id marked `NEEDS USER ACTION`. Do not invent a company name. Stop before Play Console enrollment.
