# Verification and review

Choose the smallest set of checks that resolves the concrete risks. Use repository tools rather than installing a parallel testing stack. Sources: [R20–R23](sources.md).

| Change | Appropriate evidence |
| --- | --- |
| Small text or CSS adjustment | Inspect the affected view and relevant breakpoint; run existing checks if needed. |
| Domain logic or reproduced bug | Focused behavior test demonstrating the rule or regression. |
| Form, async UI, routing or state | Component/integration checks and affected browser flow, including relevant failures. |
| Authentication, authorization or untrusted content | Boundary review plus negative integration tests against an authorized test backend. |
| Toolchain, dependency, rendering or configuration | Relevant lint/type checks, production build and runtime/deployment smoke checks. |
| Performance work | Comparable before/after measurements and clear field-versus-lab labeling. |

Use unit tests for isolated rules, component/integration tests for user-visible interaction, and a small set of end-to-end tests for critical journeys. Do not force a fixed coverage percentage or test pyramid when risk suggests a different balance.

Prefer accessible-role/name or label queries. Assert behavior instead of component internals, CSS class structure or large snapshots that obscure intent. In browser tests, use automatic waiting and retrying assertions instead of arbitrary sleeps. Isolate test data and sessions. Mock external services at explicit boundaries; retain enough integration coverage to expose contract mismatches. Exercise applicable loading, empty, timeout, malformed response, duplicate submission and stale-response cases.

For browser checks, inspect console and failed network requests, relevant mobile/desktop sizes, keyboard order and error recovery. Use representative supported browsers when compatibility is at risk; do not claim Safari/iOS verification from desktop Chromium alone. A framework's type checker may be necessary in addition to plain `tsc`.

For an unfamiliar repository, inspect package scripts and existing CI before running commands. Review scripts before executing them when trust is uncertain. Record actual commands, results and any blocked checks. Do not modify live data or real customer accounts for validation.

For a review, prioritize exploitable boundaries, broken behavior, data loss and accessibility barriers over personal style preferences. Provide file locations, evidence, impact and a concrete repair. Mark suspected issues as hypotheses and identify what would establish them.

Completion means the requested behavior is implemented, relevant checks are resolved or explicitly blocked, and remaining limitations are visible. Do not imply production deployment, field performance, full WCAG conformance or comprehensive security testing unless those were actually verified.
