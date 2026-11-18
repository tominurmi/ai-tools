# Security and privacy engineering

Read the relevant sections for the trust boundaries affected by the task. These are engineering defaults; verify platform details in current official documentation. Scale threat analysis and testing to the data and consequences involved.

## Credentials and local data

Identify what is sensitive, who can access it, how long it is needed, and which boundaries it crosses. The app is an untrusted client relative to a backend: server-side authorization must check the caller and requested resource, including account/tenant ownership.

Use Keychain for small user secrets. Choose accessibility based on foreground/background access and device-lock requirements; consider a ThisDeviceOnly class when migration/sync is undesirable. Do not apply a foreground-only policy blindly to background work. Narrow keychain queries by service/account and intended access group; handle missing, duplicate, locked/unavailable items and OSStatus errors. Separate missing credentials from transient unavailability to avoid accidental logout/data loss. Update existing values intentionally and delete the app's intended items on logout. Do not assume uninstall removes Keychain items.

Keep privileged service keys on a trusted backend. Obfuscation and `.xcconfig` do not turn a bundled secret into a secure credential. Use platform authentication flows such as AuthenticationServices where suitable; verify redirect handling and the provider's state/nonce/PKCE requirements. Treat local biometric checks as local access controls, not proof of server authorization. Handle expiry, refresh races, revocation and logout without restoring stale sessions.

For sensitive files/databases, choose appropriate iOS Data Protection and backup behavior, including access while locked. Consider temporary files, URL caches, notifications, app-switcher snapshots and exported files according to the actual threat model. Do not claim complete screenshot prevention on iOS. Use CryptoKit/Security for justified cryptography; avoid custom algorithms and do not invent key recovery or rotation behavior.

Sources: [Keychain services](https://developer.apple.com/documentation/security/keychain-services), [Using the keychain to manage user secrets](https://developer.apple.com/documentation/security/using-the-keychain-to-manage-user-secrets), [Restricting keychain item accessibility](https://developer.apple.com/documentation/security/restricting-keychain-item-accessibility), [Apple Platform Security](https://support.apple.com/guide/security/welcome/web).

## Network and external inputs

Prefer URLSession over custom transport for ordinary HTTPS requests. Preserve ATS and normal certificate/hostname verification. Do not introduce broad NSAllowsArbitraryLoads, trust-all delegates, or insecure TLS to fix a failing endpoint. If an unavoidable legacy exception is in scope, document its smallest domain scope, rationale and removal condition. ATS does not secure arbitrary low-level network code automatically. Pinning requires a threat-model reason and an operational rotation/recovery strategy; it is not a universal default.

Check HTTP status, decoding errors, domain constraints, payload/file size and content where relevant. Use timeouts, bounded retries and cancellation; retry non-idempotent operations only with a safe design. Logs and user-visible errors must not disclose tokens, sensitive URL parameters, bodies or personal data. Use Logger privacy controls where appropriate, while avoiding collection of secrets in the first place.

Validate URL components using URL parsing: scheme, exact host and allowed path/action. Reject lookalike hosts and unexpected redirects for privileged flows. Prefer associated-domain Universal Links for suitable app links, while still validating every action and caller's session. A link, push payload or restored navigation state cannot grant authorization. For WKWebView, narrow navigation/message origins, expose minimal native bridge capabilities, and validate messages before executing native actions.

Sources: [Preventing Insecure Network Connections](https://developer.apple.com/documentation/security/preventing-insecure-network-connections), [URLSession](https://developer.apple.com/documentation/foundation/urlsession), [Supporting universal links](https://developer.apple.com/documentation/xcode/supporting-universal-links-in-your-app), [Logging](https://developer.apple.com/documentation/os/logging).

## Permissions, SDKs and release declarations

Request only necessary access at a meaningful user action; use accurate purpose strings and graceful denial/revocation behavior. Prefer narrower system pickers or scoped access when they satisfy the feature. Avoid speculative background modes, shared access groups and entitlements.

Inspect app and SDK data collection, tracking, privacy manifests and required-reason API use. Confirm accepted keys/reasons and current SDK requirements from Apple. Never select a plausible-looking reason merely to pass submission validation. Ensure PrivacyInfo.xcprivacy is included in the correct target and built bundle; a file in the repository is insufficient evidence. Use Xcode's aggregated privacy report when available and reconcile App Store Connect disclosures with actual behavior. ATT, permission prompts, manifest declarations and privacy labels serve different purposes and do not replace one another.

Before adding/upgrading dependencies, check provenance, version constraints, transitive packages, license, maintenance, advisories and privacy behavior. Distinguish unknown vulnerability status from evidence of a vulnerability. Do not download or run unreviewed scripts to diagnose a build.

Sources: [Privacy manifest files](https://developer.apple.com/documentation/bundleresources/privacy-manifest-files), [Describing data use](https://developer.apple.com/documentation/bundleresources/describing-data-use-in-privacy-manifests), [Adding a privacy manifest](https://developer.apple.com/documentation/bundleresources/adding-a-privacy-manifest-to-your-app-or-third-party-sdk), [Human Interface Guidelines: Privacy](https://developer.apple.com/design/human-interface-guidelines/privacy).

## Evidence to collect when relevant

Test with synthetic data and authorized nonproduction accounts. Select cases based on the changed boundary: missing/locked Keychain item, expired credentials, logout during refresh, unauthorized resource identifier, invalid URL/redirect, malformed/oversized payload, offline timeout, permission denial/revocation, or old persistence schema. Confirm sensitive values are absent from captured logs. Separate source inspection, successful tests, outstanding device checks and remaining risk. Do not present a checklist as a security certification.
