# Code hygiene

These are engineering defaults; adapt them to the repository and change size. Sources: [R8–R10, R18, R22–R23](sources.md).

## Types and boundaries

Prefer strict TypeScript for new application code. Preserve the framework's supported compiler configuration. Evaluate `noUncheckedIndexedAccess` and `exactOptionalPropertyTypes` separately; do not assume `strict` includes them. Incremental adoption is preferable to an unrelated whole-project conversion.

Use `unknown` for untrusted data and narrow it through runtime validation at API, URL, storage and message boundaries. Reuse an existing schema library when suitable; avoid a new package for a trivial predicate. Validate server-side independently of client validation. Model meaningful states with discriminated unions when that makes impossible combinations unrepresentable. Avoid broad `any`, unexplained non-null assertions and casts that silence uncertainty. Do not treat generated API types as proof of a valid runtime response.

## Components and state

Keep render logic predictable and components cohesive, with clear props and events. Separate complex domain calculations into testable functions. Name things by domain meaning. Prefer composition over inheritance and clear duplication over a premature general-purpose abstraction. Avoid arbitrary line-count rules.

Derive filtered data, totals and labels from existing state rather than copying them into state. In React, reserve Effects for synchronization with external systems; handle user actions in event handlers and include correct dependencies and cleanup. Apply the equivalent computed/derived-state idioms in other frameworks after checking their version. Use stable item identities when rendering mutable lists.

## Asynchronous work

Represent pending, empty, error and success explicitly where they affect UX. Check HTTP status; a resolved fetch does not imply an HTTP success. Validate payloads before using them. Prevent older requests from overwriting newer state using cancellation and/or result identity checks, including cleanup. Avoid unbounded retries; retry only when the operation's semantics permit it. Prevent duplicate submissions and coordinate server-side idempotency for important writes. Roll back or reconcile optimistic changes after failure.

Keep credentials and personal payloads out of logs. Log actionable diagnostics at the appropriate boundary without swallowing exceptions. Do not expose raw internal stack traces as user-facing errors.

## Tools and dependencies

Keep the existing formatter and linter. Use type-aware lint rules where appropriate, recognizing their cost. Prefer rules that expose defects, including unhandled promises and framework lifecycle errors. Scope necessary suppressions narrowly and explain them; do not disable whole classes of checks to finish a task.

Remove dead imports, abandoned code, accidental debug output and stale comments within the touched scope. Comments should explain constraints and decisions. Keep public interfaces documented where non-obvious.

Use one package manager and committed lockfile. Use its reproducible CI installation mode; for npm this is `npm ci` with consistent configuration. Review new dependencies for necessity, maintenance, compatibility, license, bundle cost, install scripts and known advisories. Inspect lockfile changes. Do not run a forced automatic audit repair or major upgrade without understanding behavior changes. Audit results require triage, not claims of complete safety.
