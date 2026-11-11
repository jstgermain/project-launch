# Flutter client architecture

Load this only when the user selects Flutter or the repository already uses it. Do not migrate a working client without an explicit request.

## Confirm the boundary

Record the choice and requested targets: iOS, Android, macOS, Windows, Linux, and/or web. Choose either a shared Flutter product client across those targets or Flutter mobile/desktop with a separate web app. Keep a public marketing site or admin dashboard separate only when required.

Use Flutter/Dart for the shared client. Share feature logic, models, design tokens, and adaptive UI. Plan platform adapters for capabilities that differ; do not promise identical behavior or zero platform-specific work. Flutter uses its renderer for the UI; distinguish this from platform-native widgets and from a website running inside a WebView.

Do not infer Expo, React Native, Electron, or Tauri from existing JavaScript tooling. Keep a compatible existing backend and database. Do not move server credentials or privileged database access into Dart clients.

## Repository and contracts

- Fit the Flutter client into the existing repository, commonly `apps/client` or the established equivalent; avoid parallel competing client folders.
- Manage Dart dependencies and Flutter targets with Flutter tooling. A pnpm/Turborepo backend workspace can coexist, but Dart packages are not npm workspace packages.
- Document separate Dart and backend setup, analysis, test, build, and release commands; do not treat a placeholder npm build command as a native build.
- Define language-neutral REST request/response schemas, authentication, pagination, errors, and realtime events. Generate or validate Dart models against the API where appropriate. TypeScript modules cannot be imported directly into Dart.
- Record migration milestones and keep the legacy client until the replacement is verified. Remove superseded dependencies only within authorized migration work.

## Client foundation and verification

- Inspect Flutter/Dart SDK constraints, `pubspec.yaml`, lockfile, entry point, and generated runner folders for each selected target.
- Verify SDK/toolchain availability before reporting builds; name missing SDKs as blockers. Do not mark a target complete because a runner folder exists.
- Use one shared theme and adaptive navigation/layouts. Test narrow mobile screens, desktop resizing, keyboard/IME, selection, accessibility, text scaling, focus, shortcuts, and scrolling lists.
- Separate development/staging/production API endpoints and feature configuration. Client configuration is public; keep server secrets on the backend.
- Verify authentication refresh/logout, reconnect and background/resume behavior. Use platform-appropriate credential storage and record browser storage risks separately.
- Verify platform adapters for permissions, notifications, files/media, links, and lifecycle only when in scope. Audit plugin support per target rather than assuming mobile plugins work on desktop and web.
- Include Dart analysis, behavior/widget tests, and integration checks for the requested targets. A passing web build is not proof that mobile or desktop works.
- Use macOS/Xcode for iOS and macOS build checks, Windows tooling for Windows, and the required Android/Linux toolchains for those targets. Do not claim cross-host release validation.

## Releases and hosting

Keep one shared-client implementation section in the launch checklist, plus release tasks per selected target. Do not duplicate shared features under every operating system.

- iOS/Android: load the corresponding platform and app-store references for identifiers, signing, permissions, privacy declarations, store billing when applicable, physical-device checks, and release metadata. Do not create additional SwiftUI/Compose product clients.
- macOS: plan entitlements, signing, notarization or the selected store route, packaging, and updates.
- Windows: plan application identity, release packaging, signing, distribution, and updates.
- Linux: include packaging/distribution only when requested.
- Web: plan Flutter web hosting, routes and deep-link fallback, caching/update behavior, TLS, and backend CORS/auth. Assess browser compatibility, accessibility, and public-content discoverability; add a separate marketing site only if needed.

Store accounts, certificates, notarization, console configuration, and live deployments remain external or need verification until proven. Flutter support for a target does not imply signing, distribution, or integrations are complete.

## Flutter release automation

Treat the Flutter version in `pubspec.yaml` as an input, not proof that every store target is synchronized. iOS/macOS marketing versions and build numbers, Android `versionName` and `versionCode`, and desktop package versions may diverge. Record the intended values per platform in the release request and pass explicit `--build-name` and `--build-number` values when the project does not deliberately share one version.

For a releasable Flutter client:

- Pin or constrain Flutter and Dart, and record the compatible Xcode, iOS SDK, JDK, Android Gradle Plugin, Gradle, and CocoaPods versions. CI must select a toolchain that satisfies the current store SDK requirement rather than relying on the runner default.
- Keep generated runner files under an explicit repository policy. Run Flutter configuration before native archiving when required, but do not let it silently overwrite deliberate Xcode or Gradle settings. Back up and restore generated project changes when the release script must invoke configuration as a build step.
- Verify release builds use production endpoints, production identifiers, the intended flavor/scheme, and release entitlements. A successful debug run or Dart VM connection is not release evidence.
- Run Dart formatting, analysis, tests, and platform-native validation as distinct checks. Native archive/export failures can occur after Flutter checks pass.
- Build and verify all coordinated Apple artifacts before uploading either one when iOS and macOS are intended to ship together. This avoids a preventable half-release when the second archive fails.
- Use temporary CI keychains and explicit export options. Distinguish local automatic-signing behavior from CI signing and keep certificate/profile setup idempotent.
- Check build-number uniqueness before upload, wait for store processing, then verify the exact platform, marketing version, build number, testing group or track, and release notes.
- Keep build, archive, export, upload, testing distribution, review attachment, review submission, and production rollout separately invokable and retryable.

Load [store-automation.md](store-automation.md) for the shared release contract, [apple-release-automation.md](apple-release-automation.md) for iOS/macOS, and [google-play-release-automation.md](google-play-release-automation.md) for Android.
