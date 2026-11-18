# Official sources and engineering decisions

Research baseline: 2026-10-29. This is a source map, not a frozen SDK compatibility matrix. Recheck relevant official documentation, SDK availability and release notes whenever implementing version-sensitive behavior. Prefer installed SDK declarations and compiler evidence for what the local build supports; current web examples may require a newer SDK or OS. If a documentation page needs JavaScript, try its provided Markdown link or Apple's indexed documentation; disclose unresolved gaps.

## Swift and architecture

- [Swift API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/): make names and call sites clear; document non-obvious API contracts. Concision alone is not a design goal.
- [The Swift Programming Language: Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html): use structured task lifetimes, isolation and explicit suspension points when reasoning about shared state.
- [Swift 6 migration strategy](https://docs.swift.org/main/documentation/swift-6-concurrency-migration-guide/migrationstrategy/): migration can be incremental by module. Compiler version and language mode are distinct; do not force a whole-project conversion as a side effect of a feature.
- [Managing model data in your app](https://developer.apple.com/documentation/swiftui/managing-model-data-in-your-app): separate model and presentation concerns, define ownership and observation deliberately. SwiftUI Observation is available from iOS 17; verify availability of individual APIs rather than assuming all observation-related features share that baseline.
- [SwiftUI model data](https://developer.apple.com/documentation/swiftui/model-data): choose State, Binding, Environment and observation tools for their ownership semantics. No single wrapper or architecture fits every lifetime.

These sources support the skill's engineering defaults, not a claim that Apple mandates MVVM, Clean Architecture, a file-count limit, a coverage percentage, or a particular dependency-injection library.

## UX and accessibility

- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/): use platform behavior, coherent navigation and the applicable component guidance.
- [Accessibility](https://developer.apple.com/documentation/accessibility/): inspect actual assistive-technology behavior and system accessibility settings. An automated audit alone cannot establish complete accessibility.

## Verification and toolchain

- [Testing in Xcode](https://developer.apple.com/documentation/xcode/testing): combine fast logic tests, integration checks and critical user-flow UI tests according to risk. Xcode 16 and later includes Swift Testing alongside XCTest.
- [Swift Testing](https://developer.apple.com/documentation/testing): use expressive unit tests and isolate shared state because tests may execute in parallel. Preserve existing XCTest tests; UI automation remains an XCTest/XCUIAutomation concern.
- [Xcode documentation](https://developer.apple.com/documentation/xcode): verify target/scheme/configuration and installed simulator/device support before constructing build commands. Do not guess signing assets or bundle identifiers.

Discover the real build inputs first. Example command shapes, with values taken from the project:

```sh
xcodebuild -list -workspace <workspace.xcworkspace>
xcodebuild -showdestinations -workspace <workspace.xcworkspace> -scheme <scheme>
xcodebuild -workspace <workspace.xcworkspace> -scheme <scheme> -configuration Debug -destination 'platform=iOS Simulator,id=<available-UUID>' -derivedDataPath <temporary-build-directory> build
```

Use `-project` instead when that is the actual build entry point. Run `test` only with a scheme/test plan that supports it; use `-only-testing` for focused checks when suitable. Retain logs/xcresult evidence in a suitable temporary/artifact location without sensitive values. Simulator build success does not prove device signing or hardware features. A license-blocked command is blocked, not a compile failure or a passed test.

## Energy and measured performance

- [Improving your app's performance](https://developer.apple.com/documentation/xcode/improving-your-app-s-performance): profile the symptom and prioritize measured work. Distinguish launch, responsiveness, allocation, storage and rendering bottlenecks.
- [Reducing your app's battery use](https://developer.apple.com/documentation/xcode/reducing-your-app-s-battery-use): reduce work, use efficient high-level APIs and manage resource use in response to real user needs.
- [Analyzing your app's battery use](https://developer.apple.com/documentation/xcode/analyzing-your-app-s-battery-use): use available Xcode Organizer, Instruments and MetricKit evidence; no one tool proves every power characteristic.
- [Power Profiler](https://developer.apple.com/documentation/xcode/measuring-your-app-s-power-use-with-power-profiler): hardware/OS availability matters; the documented baseline is iPhone/iPad with OS 26 or later. Compare the same device model and controlled workloads; validate availability in the installed tools before promising a trace.

For meaningful comparison, record device/OS/build configuration, scenario, duration and relevant thermal/power/network conditions. Report what was measured and avoid unsupported battery or environmental claims.

## Security and release

Read [security.md](security.md) for boundary-specific guidance and Apple sources covering Keychain, ATS, external inputs and privacy manifests. Verify current App Store and SDK submission requirements at release time; research date alone does not establish continued compliance.

## Agent format

[Official OpenAI custom-agent documentation](https://learn.chatgpt.com/docs/agent-configuration/subagents) specifies standalone TOML files in the personal or project agents directory with name, description and developer_instructions. The parent supplies permissions and capabilities. Model settings are intentionally omitted here so this agent follows the parent session's selection.
