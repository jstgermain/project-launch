# Launch readiness

Load this for "what is missing before launch", "prepare for production", or a store release. Judge only the surfaces in scope. A missing iOS icon is irrelevant to a marketing site. A missing StoreKit product is irrelevant to an app that sells nothing.

Do not claim production is ready because the repository looks finished. Console, DNS, and secret-store state stay `NEEDS VERIFICATION` until confirmed.

Prepare mode may fix in-repo gaps. It still may not apply production migrations, change DNS, submit for review, or switch a provider to live mode unless the user asks for that action.

## Web production

Include when a web app or site ships:

- Production build is defined. Actually running it is allowed only after the user asks to verify the build
- Tests the project already has are part of the gate, not a new framework
- Production environment variable names are listed and stored in the host
- Production database exists and the migration workflow is documented, when a database is in scope
- Domain, canonical host, redirects, and TLS. The public site URL includes `www` unless a different host or another subdomain is already specified
- Production auth settings and production payment mode, when those features exist
- Error monitoring and a rollback path
- Privacy policy and terms links when the site collects personal data or takes payment

## iOS release

Include for a native iOS launch:

- Release configuration builds without committed secrets
- Production API base URL selected
- Production auth configured, including Sign in with Apple when social login needs it
- StoreKit production catalog and server verification, when digital goods are sold
- Privacy manifest and permission strings for capabilities the app uses, when the platform requires them
- Icon and launch assets
- Screenshots, metadata, privacy answers, and support URL
- TestFlight on a build the team has actually installed
- Review notes and a demo path that does not require the reviewer to pay, when the app has accounts
- Primary flows verified on the smallest supported iPhone, with larger Dynamic Type, safe-area placement, scrolling sheets, keyboard avoidance, and any camera/photo/crop interactions on a physical device
- Any first-run or update setup flow has Cancel or Back behavior, resumes incomplete setup, distinguishes an explicit skip from completion, and leaves a visible route to finish later
- CI distinguishes TestFlight from App Review, hard-gates both on applicable checks, and blocks replacement of an existing review submission without explicit per-release consent

## Android release

Include for a native Android launch:

- Release build is defined and signing uses Play App Signing plus an uncommitted upload key
- Production API and production auth selected
- Play Billing catalog and acknowledgement, when required
- Icon, screenshots, feature graphic, Data safety, and privacy policy
- Internal or closed testing on a build the team has installed
- Production track and rollout plan
- Primary flows verified on a compact physical device with both gesture and three-button navigation, system insets, scrolling sheets, keyboard avoidance, responsive actions, and any camera/photo/crop interactions
- Any first-run or update setup flow has Cancel or Back behavior, resumes incomplete setup, distinguishes an explicit skip from completion, and leaves a visible route to finish later
- CI distinguishes internal testing from production, hard-gates both on applicable checks, and fails closed when production signing or Play credentials are missing

## Privacy and legal

Include when the product collects personal information, accounts, or payments. This is not legal advice. Copy and policy choices are `NEEDS USER ACTION` and often need review by the user's counsel.

Consider, then keep only what applies:

- Privacy policy and terms of service
- Account deletion and the data deletion path behind it
- Data export, when the product stores customer content
- Cookie or consent UI, when non-essential tracking is used
- App Store privacy details and Play Data safety, when those apps exist
- A support contact
- Accessibility of the primary flows

Do not draft legal text and call it approved.

## Post-launch

Include only when the user is preparing a real production launch or the product is already live. Keep it small:

- Who receives alerts
- Where logs are retained
- How a bad deploy is rolled back
- Who applies database migrations
- How dependency updates are noticed

Do not invent an on-call rotation or a status page for a first marketing site unless the user asked.

## Enterprise customer readiness

Include only when a contracted or target customer requires enterprise review. Load [enterprise-readiness.md](enterprise-readiness.md).

Distinguish product launch from customer approval. The application may be deployable while a customer rollout is blocked by SSO/SCIM testing, managed-device validation, penetration-test remediation, evidence collection, legal redlines, support commitments, or procurement onboarding.

For every blocker, record the requirement source, owner, dependency, target date, and evidence needed to close it. Do not promise a procurement date from engineering estimates alone. Do not call a security questionnaire, policy set, or internal test an independent audit.

## Readiness output

Group gaps by blocker:

1. Blocks launch: missing production data path, broken release build, no admin authorization, store billing required but absent, secrets committed
2. Blocks store review: missing privacy answers, icons, or review access
3. Should be done before traffic: monitoring, backups, domain TLS
4. Blocks contracted customer launch: unverified enterprise identity, E2EE design, managed-device behavior, audit evidence, legal commitment, or procurement dependency
5. Can follow launch: polish, extra test layers, staged rollout

Say which group each gap is in. Do not collapse them into a score.
