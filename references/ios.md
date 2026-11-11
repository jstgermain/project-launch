# Native iOS

Load this only when the product has, or the user is adding, a native iOS app. Do not create an iOS project for a web-only product.

If the repository already uses React Native, Flutter, or another cross-platform toolkit for iOS, keep it and audit that project. Do not replace it with SwiftUI unless the user explicitly asks for a native rewrite.

For a new iOS app, use Swift and SwiftUI. Do not choose a cross-platform toolkit because the web app uses React.

Store enrollment, App Store Connect, TestFlight, and StoreKit are judged with the app-store reference. An Xcode project does not make them complete.

## Local engineering

Account for:

- Xcode project or workspace, with a real app target
- Swift version and minimum iOS version recorded in the project
- SwiftUI or UIKit, matching what the project already uses
- Display name, bundle identifier, and version / build number
- Debug and Release configurations
- A development versus production configuration for the API or feature flags, when the app calls a backend
- Secrets kept out of the repo. Use build settings or a local config excluded by Git, and document the variable names
- Capability usage strings in the property list for permissions the app actually requests
- Associated domains and universal links only when the product uses them. The website host includes `www` unless another host or subdomain is already specified
- Keychain when the app stores credentials or tokens
- App Groups only when an extension or shared container is required
- Fixed and floating actions placed with SwiftUI safe areas, usually `safeAreaInset`, so controls remain reachable around the home indicator, keyboard, and compact screens
- Variable-height sheets and forms scroll on the smallest supported iPhone and under larger Dynamic Type sizes
- Camera, document-scan, crop, and photo-picker flows verified on a physical device when the product uses them. Persist the accepted media result, show it back to the user, and provide replace/retry behavior

Signing team, certificates, and provisioning profiles are usually outside the repo. Mark them `NEEDS VERIFICATION` or `EXTERNAL CONSOLE`. If a certificate or private key is committed, treat that as a security gap. Do not copy the material into the checklist or the chat.

## Push

Include push only when the product sends notifications.

- Push capability and entitlement
- Permission prompt at a sensible point in the product, not at first launch by default
- Token registration to the backend
- Server-side send path, shared with Android when both apps exist

APNs key material stays in the provider's secret store. Record the variable name only.

## Evidence

| Observation | Status |
| --- | --- |
| App target, bundle id, Debug and Release, versioning, and env split for a real backend | Local engineering complete |
| Project exists, bundle id still a sample, or only Debug is configured | Partially complete |
| README mentions iOS, no project | Missing |
| Signing, devices, and TestFlight | Needs verification unless the repo contains the config and you can explain it without secrets |
| Cross-platform app already shipping | Keep it. Audit release config. Do not rewrite |

Do not run `xcodebuild` during discovery. During an authorized prepare pass, a build is allowed only if the user asked to verify the build and the command is the project's documented one.

## New-app minimum

When setup is authorized for a new iOS app, create a SwiftUI app with the bundle id the user provided. If they have not chosen one, use a clearly placeholder identifier and mark the real id `NEEDS USER ACTION`. Do not invent an organization name.

Stop before Apple Developer portal work. List it. Do not claim a team, App ID, or profile exists.
