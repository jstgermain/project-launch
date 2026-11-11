# Enterprise readiness

Load this reference when the product targets enterprise, regulated, public-sector, security-sensitive, or centrally managed customers, or when an existing project is entering a formal security review or procurement process.

This phase is conditional. Do not add enterprise controls to a marketing site or consumer product without a buyer, threat, contractual, or regulatory reason. Do not claim certification, legal compliance, or contractual acceptance.

## Determine the requirement

Use repository evidence first. When the audience is plausibly B2B, regulated, public-sector, security-sensitive, or centrally managed but still unknown, ask one screening question: **Will those customers be in scope now or before the planned launch?**

- If no, record the phase as not applicable only when a deliberate omission would otherwise be surprising, then stop loading this reference.
- If yes, ask the smallest grouped follow-up needed to identify the known requirements below.
- If unknown, record the buyer decision as `NEEDS VERIFICATION`; do not add all enterprise capabilities while waiting.

Ask only what remains unknown:

- Which customer segments and jurisdictions are in scope?
- Is there a named buyer requirement, security questionnaire, contract, regulation, or sales deadline?
- Which capabilities are required now: E2EE, SSO, SCIM, MDM, audit logs, data residency, retention controls, or customer-managed keys?
- Which assurance artifacts are expected: security audit, penetration test, SOC 2 report, ISO certification, policy set, business continuity evidence, accessibility report, privacy documentation, or a subprocessor list?
- What contractual support, uptime, incident-notification, recovery, or response commitments are being considered?
- Who owns security, legal, privacy, support, finance, and procurement responses?

Record the source of each requirement. A feature requested by one prospect is not automatically a universal platform requirement. Put buyer-specific commitments in the appropriate contract or sales record, and put reusable product capabilities in the launch checklist.

## Security assessments and audits

Use the dedicated security-audit workflow for technical findings when it is available. This reference owns readiness planning, evidence dependencies, and external work; it does not duplicate vulnerabilities from that report.

Depending on risk and buyer expectations, consider:

- Threat model and data-flow review
- Secure development and change-management evidence
- Dependency, SAST, secret, and infrastructure checks already justified by the stack
- Independent penetration test and remediation evidence
- Access reviews, incident exercises, backup restoration tests, and disaster-recovery exercises
- Vulnerability intake, remediation targets, and customer security contact

A configured scanner is evidence that a check exists, not proof that findings are resolved. An internal review is not an independent audit. Mark external assessment scheduling, auditor selection, report issuance, and remediation verification separately.

## End-to-end encryption

E2EE means plaintext is unavailable to the service operator for the protected content under the stated threat model. HTTPS, database encryption at rest, and provider-managed disk encryption are important but are not E2EE.

Before recommending or implementing E2EE, determine:

- Protected content and explicitly unprotected metadata
- Participants and device trust model
- Where keys are generated, stored, rotated, revoked, backed up, and recovered
- Multi-device enrollment and lost-device behavior
- Account recovery and organization offboarding
- Sharing, search, previews, notifications, exports, moderation, support, legal hold, retention, and backup consequences
- Whether enterprise key management or customer-managed keys are actually required instead
- Cryptographic design review and test strategy

Prefer established protocols and libraries. Do not invent cryptography. Treat a change to E2EE as an architecture decision that updates data flows, key boundaries, recovery UX, operations, and the threat model. If product requirements conflict with the E2EE trust model, mark the design blocked until the owner chooses the tradeoff.

## Enterprise identity: SSO and SCIM

SSO and SCIM are separate capabilities. Include only those buyers require.

For SSO, account for:

- SAML 2.0 or OIDC based on buyer and provider compatibility
- Organization and verified-domain ownership
- Per-tenant identity-provider configuration and metadata or key rotation
- Service-provider initiated and identity-provider initiated flows when required
- Just-in-time provisioning policy
- Attribute and role mapping
- Session lifetime, logout, MFA responsibility, and break-glass access
- Enforcement rules that do not lock every administrator out
- Audit events, error handling, test tenant, and administrator documentation

For SCIM, account for:

- SCIM 2.0 users and groups actually required
- Tenant-scoped credentials with rotation and least privilege
- Stable identifiers, pagination, filtering, idempotency, and rate limits
- Create, update, suspend, reactivate, and deprovision behavior
- Group-to-role mapping and protection against unintended privilege escalation
- Reconciliation, audit logs, provider interoperability tests, and customer setup documentation

Do not mark SSO or SCIM complete because a library or provider is selected. Verify tenant isolation, provisioning and deprovisioning, role mapping, failure handling, and at least one representative identity provider.

## Managed devices and MDM

Include MDM readiness only for mobile or desktop products expected to run on organization-managed devices.

Determine which platforms and management ecosystems matter. Account for applicable managed-app configuration, managed distribution, app restrictions, certificate or per-app VPN requirements, managed open-in/data-sharing rules, remote account removal, device posture integration, update policy, and administrator documentation.

Keep secrets out of managed configuration unless the platform and threat model explicitly support the value. Test on a genuinely managed device or representative test tenant. A configuration schema in the repository is partial until deployment behavior is verified.

## Compliance evidence

Start from the actual customer, contractual, and regulatory scope. Do not select a framework because it is recognizable.

Build an evidence register that names:

- Control or requirement
- System and environment in scope
- Evidence artifact and location
- Owner
- Collection method and review cadence
- Coverage period
- Reviewer or approver
- Open gap, remediation, and target date

Evidence may include policies, access reviews, change records, training records, risk assessments, vendor reviews, incident exercises, backup tests, vulnerability reports, penetration-test reports, architecture and data-flow diagrams, retention/deletion tests, and availability records. Repository files prove only what they contain; console, organizational, and operating evidence stays `NEEDS VERIFICATION` until confirmed.

Never write “compliant,” “certified,” or “audit passed” unless the appropriate independent authority has issued that result and the exact scope and period are recorded.

## Contractual support and operations

When contracts may promise support or reliability, separate product capability from commercial commitment. Consider:

- Support hours, channels, severity definitions, and escalation path
- Response and resolution targets
- Service-level objectives versus contractual service-level agreements
- Uptime measurement, exclusions, maintenance windows, and service credits
- Incident notification and security contact
- Backup, recovery, continuity, and disaster-recovery commitments
- Data export, deletion, return, retention, residency, and subprocessor notification
- Customer onboarding, implementation, training, and offboarding responsibilities

Legal, support, operations, finance, and leadership must approve applicable commitments. Do not turn a monitoring dashboard into a contractual uptime promise.

## Procurement and lead time

Enterprise procurement may outlast engineering. Track it as a dependency with an owner, target date, and blockers. Possible work includes:

- Security and privacy questionnaires
- Architecture and data-flow diagrams
- Data-processing, confidentiality, business-associate, or other required agreements
- Subprocessor, data-location, retention, deletion, and privacy materials
- Insurance certificates and business/financial information
- Accessibility documentation such as a VPAT when required
- Vendor onboarding, sanctions or background checks, purchase order, tax, and payment setup
- Security review, penetration-test remediation, legal redlines, and executive approvals

Do not store confidential buyer questionnaires or contracts in public documentation. Keep the project checklist generic and point to the approved private system of record when one exists.

## Checklist and status

Split enterprise work into:

1. Product engineering that can be implemented in the repository
2. Security findings owned by the security-audit report
3. Evidence that must be collected or refreshed
4. External assessments and certifications
5. Legal and contractual approval
6. Buyer procurement and onboarding

Mark long-lead work early. A product may be technically launch-ready while blocked from a contracted customer launch. State both truths.

## Evidence judgment

| Observation | Status |
| --- | --- |
| Requirement, owner, evidence, scope, and verification are recorded | Complete for that item |
| Package or policy exists, but tenant flow or operating evidence is absent | Partially complete |
| Buyer requires the capability and no implementation or plan exists | Missing |
| Legal, auditor, identity-provider, MDM tenant, or buyer action is pending | Blocked or needs verification, with the dependency named |
| Marketing claim exists without scoped evidence | Missing evidence; do not repeat the claim as fact |
