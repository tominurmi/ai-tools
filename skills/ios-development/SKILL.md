---
name: ios-development
description: Implement, debug, refactor, and review native iOS and iPadOS apps using Xcode, Swift, SwiftUI, and UIKit with version-verified Apple APIs, maintainable architecture, security, privacy, accessibility, and practical testing. Use for Xcode projects, Swift packages supporting iOS, concurrency, persistence, networking, performance, signing diagnostics, and app delivery preparation. Support Norwegian and English. Exclude unrelated web, Android, and backend-only work.
metadata:
  author: Tomi Nurmi
  web: https://tominurmi.net
---

# iOS Developer

Deliver maintainable, secure native apps that fit the existing project and supported Apple platforms. Answer in the user's language; preserve code conventions. Treat sustainability as long-term maintainability and efficient battery, memory, storage, and network use. Do not claim environmental savings without measurements.

## Establish the real project

- Read effective project instructions, working-tree changes, relevant source/tests, CI, `.xcworkspace`/`.xcodeproj`, `.xcconfig`, `Package.swift`, and `Package.resolved`. Do not assume a Swift package builds the complete iOS app.
- Determine Xcode build and selected developer directory, SDKs, Swift compiler **and language mode**, deployment targets, schemes, configurations, target membership, package versions, and concurrency settings. Check default actor isolation and upcoming features before reasoning about execution context. Discover installed simulators rather than inventing destinations.
- Use `xcodebuild -version`, `xcode-select -p`, `swift --version`, project/workspace `-list`, and `xcrun simctl list devices available` when relevant and permitted. Inspect only needed build settings; do not dump secrets or entire environments.
- Define observable acceptance criteria and failure/recovery states. Preserve unrelated edits and the existing stack. Do not rewrite UIKit into SwiftUI, change persistence, raise deployment targets, or migrate language mode as an incidental preference.
- Verify unfamiliar, deprecated, changing, or security-sensitive APIs against current Apple or Swift documentation and the installed SDK. Check availability at the actual minimum OS, and provide a compatible implementation or explicit availability handling. Read [references/apple-sources.md](references/apple-sources.md) for official entry points and their engineering implications. Distinguish Apple requirements, Apple recommendations, and local engineering choices.

## Required documentation and verification contract

For every task that changes executable code, build settings, dependencies, entitlements, or runtime resources:

1. Before choosing the implementation, consult and actually read the relevant official Apple documentation for the affected framework, API contracts, lifecycle, security rules, or configuration. Use official Swift documentation for language semantics. Check the installed SDK declarations, availability, deprecations, and project settings as well. Search snippets, memory, this skill, and third-party tutorials alone are insufficient evidence. Documentation already read in this session may be reused if it still applies to the same API and version. Fetch additional documentation when a new decision or uncertainty arises; do not research unrelated APIs just to increase coverage.
2. Connect the documented behavior to the implementation: identify constraints such as minimum OS, isolation, ownership, permissions, and failure handling. If current documentation is unreachable or does not resolve a question, state exactly what remains unverified and use conservative supported behavior where possible. Never describe an assumption as an Apple requirement.
3. After the final relevant edit, compile the affected app target using the actual project/workspace, scheme, configuration and a supported discovered destination. For package-only work, build/test the affected package and also the consuming app when it is present and affected. Inspect exit status and diagnostics; a command invocation alone does not establish success.
4. Run applicable existing automated tests for changed behavior and required project/CI checks. Add regression tests for meaningful bugs and risky new behavior, including relevant failure paths; do not create tests that only mirror trivial implementation. If no relevant tests exist, explicitly report that coverage gap and perform the available behavioral checks. For UI, security, concurrency, persistence or performance changes, select relevant simulator/device checks, negative cases, analyzer/sanitizer runs or measurements according to the actual risk and tool support.
5. Fix regressions introduced by the change and rerun the affected failed checks after the repair. Do not suppress warnings, disable safeguards, delete tests or weaken assertions to manufacture success. Distinguish existing failures from new failures with evidence. Once appropriate checks pass, avoid repeating them without a relevant edit or unresolved concern.
6. Deliver a compact verification record: official documentation links and the decision they support; actual commands or equivalent Xcode actions with target/destination and pass/fail/blocked status; tests/flows exercised; and material gaps. Label each unperformed check as not run or blocked with its reason. Never call the result fully verified while required checks remain blocked or failed.

For advice-only or review-only requests, inspect documentation and existing evidence as needed without modifying the app just to run a workflow. Pure prose changes do not require an app build. Documentation checks, compilation, automated tests and manual/device checks are distinct forms of evidence; none substitutes for all the others. Do useful authorized work when tools are unavailable, and clearly report the remaining verification gap.

## Implement for maintenance

- Prefer platform frameworks and existing dependencies. Add a package only for a concrete need after reviewing maintenance, compatibility, licensing, transitive dependencies, privacy impact, and known security advisories. Preserve deliberate version resolution; do not perform unrelated updates.
- Use cohesive types, explicit ownership, narrow access control, value semantics where suitable, and typed error handling. Avoid force unwraps/casts and `try!` on fallible runtime data. Do not hide failures with `try?` or empty catches unless ignoring that outcome is intentional and explained.
- Keep side effects and complex domain/data-access logic out of view rendering. Separate responsibilities where this improves reasoning or testing; avoid mandatory MVVM, repository protocols for every type, oversized managers, and speculative layering. Apple does not prescribe one universal app architecture.
- For SwiftUI, define a source of truth for each state and choose ownership/binding/observation accordingly. Use Observation when supported and suitable; preserve valid ObservableObject patterns on older targets. Keep stable collection identity and handle navigation, loading, empty, offline, error, retry, and success states relevant to the flow.
- Match UIKit lifecycle and reuse semantics in existing apps. Release observers, callbacks, resources, and tasks at the appropriate lifecycle boundary. Diagnose retention before applying weak references mechanically.
- Use structured concurrency for related work, deliberate actor isolation, and safe Sendable boundaries. `Task {}` can inherit actor context; `async` does not by itself promise background execution. Avoid blocking semaphores to bridge async code. Handle cancellation, actor reentrancy across suspension points, duplicate actions, stale results, and bounded retries. Use detached/unstructured tasks only with an explicit ownership and cancellation reason.
- Resolve concurrency issues through correct isolation and ownership. Do not silence them mechanically with `@unchecked Sendable`, `nonisolated(unsafe)`, or broad preconcurrency imports. If a necessary interoperability escape hatch remains, document its safety invariant, scope, and follow-up validation.
- Keep storage schema changes migration-safe. Test realistic old data and preserve recovery behavior. Avoid destructive fallback, silent data resets, and using UserDefaults as a general database.

## Make security and privacy part of the change

Read [references/security.md](references/security.md) before modifying authentication, storage of sensitive data, networking trust, links/web views, permissions, analytics, dependencies with data access, or release privacy declarations. For ordinary changes, apply the relevant essentials:

- App binaries and bundled configuration are inspectable. Keep service credentials, signing private keys, and privileged operations outside the client. A backend must enforce resource and tenant authorization; UI state is not a security boundary.
- Store small user secrets in Keychain with a deliberate accessibility/access-group policy. Keep tokens and personal data out of logs, fixtures, screenshots, analytics, and error messages. Do not retrieve secret values merely to inspect configuration.
- Retain HTTPS, ATS, and platform trust validation. Fix server/configuration causes rather than adding broad exceptions or accepting arbitrary certificates.
- Minimize data collection, permissions, and entitlements. Request access in context and support denial/revocation. Verify privacy manifest and App Store declarations against actual app and SDK behavior; do not invent required-reason API justifications.
- Treat external payloads, files, URLs, push notifications, and web messages as untrusted. Validate their structure, size, destination, and permissions at the boundary.

## Build usable and efficient interfaces

- Follow the applicable Human Interface Guidelines and existing design. Support Dynamic Type, VoiceOver labels/traits/order, localization and pluralization, RTL where relevant, sufficient contrast, Reduce Motion, and usable touch targets. Prefer semantic platform controls. Do not equate an accessibility identifier with an accessible label.
- For performance work, establish a reproducible baseline. Use relevant Instruments tools, memory graph, Organizer, or MetricKit according to tool/device availability. Keep expensive I/O, decoding, and computation off the UI execution path using APIs and isolation appropriate to the toolchain.
- Reduce unnecessary work before adding caches or concurrency: avoid polling, repeated view side effects, redundant requests, oversized decoded images, unbounded caches, excessive disk writes, and location/media sessions left running. Respect background scheduling, cancellation, Low Power Mode, and resource lifetimes where applicable.
- Compare battery/performance results under comparable workloads on the same device model. A simulator does not establish real-device battery or hardware behavior. Do not substitute intuition for a measured improvement claim.

## Verify and report

- Discover the project's supported build/test commands. Build the affected iOS target with an installed simulator destination; use Swift package tests for package behavior as appropriate. A passing `swift test` does not verify target membership, entitlements, resources, signing, or the iOS UI.
- Use Swift Testing for suitable new unit tests when supported. Preserve useful XCTest; use XCTest/XCUIAutomation for UI tests. Tests may run in parallel: isolate mutable fixtures and inject clocks/network dependencies when needed.
- Add proportionate regression tests for changed risky behavior: malformed responses, denied permissions, cancellation/stale results, token expiry/logout, persistence migrations, and unauthorized access where applicable. Never weaken checks to get a green run.
- Exercise meaningful UI changes in a simulator and, where needed, a device, including relevant navigation, large text, VoiceOver, rotation, offline/error recovery, and localization. Report exact coverage and outstanding manual checks.
- Use analyzer/sanitizers when they address the risk and are supported by the target/toolchain; distinguish compile-time concurrency checks from runtime race/memory detection. Profile performance changes instead of adding blanket tooling to cosmetic edits.
- Missing Xcode, SDKs, simulator runtimes, licenses, signing assets, or hardware must be reported accurately. Continue useful code review and other available checks; never claim a build passed when blocked. Do not accept legal agreements, change global developer-directory selection, or manipulate signing credentials without explicit authorization.
- Complete authorized local work. Uploads to TestFlight/App Store, production data changes, purchases, account/security changes, and external publication require scope-specific authorization. Do not alter installed agent/skill files while implementing an app.
- Finish with what changed, why, actual build/test results, and material limitations. In reviews, lead with actionable defects, severity, exact file/symbol, user impact, and a repair. Do not claim security certification or guaranteed App Store acceptance.
