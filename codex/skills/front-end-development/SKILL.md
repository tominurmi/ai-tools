---
name: front-end-development
description: Design, implement, debug, refactor, and review web frontends with version-verified APIs, maintainable JavaScript/TypeScript, appropriate framework choices, secure client/server boundaries, accessibility, performance, and practical testing. Use for HTML, CSS, JavaScript, TypeScript, React, Next.js, Vue, Nuxt, Svelte, SvelteKit, Angular, Astro, browser UI, forms, state management, frontend architecture, and code hygiene. Support Norwegian and English. Exclude native mobile, Godot implementation, backend-only tasks, and pure graphic design.
---

# Front-end development

Build the smallest maintainable solution that meets the actual user journey and deployment constraints. Preserve working project conventions. Treat framework choice as an engineering decision, not a ranking of popularity.

## Codex project integration

- Apply the effective repository instructions from AGENTS.md and AGENTS.override.md according to Codex's configured discovery and precedence rules; check applicable instructions for the files being changed.
- Work in the user's target project, not in this installed skill directory. Complete the project-context check below before making changes.
- Resolve bundled reference links relative to this SKILL.md. Use only tools available in the current Codex session; do not assume ChatGPT Work connectors, a browser or network access exist.
- Preserve existing sandbox and approval settings. Report blocked checks without claiming they ran.

## 0. Identify the project context before making changes

Run this check at the start of each task, before scaffolding, installing dependencies, choosing a stack, or editing files.

- Locate the intended project root and, in a monorepo, the relevant application/package and shared workspace configuration. Inspect the supplied path, applicable repository instructions, directory layout, manifests, configuration and existing source files. A missing `package.json`, Git repository or familiar `src/` directory does not mean the project is new; plain HTML sites and nested applications are existing projects too.
- **Existing project:** map the affected feature to its current structure. Inspect nearby representative files to identify folder responsibilities, naming, imports/aliases, component patterns, routing, styling/tokens, state/data access, test placement and tooling. Follow those conventions and extend existing modules/components before creating new ones. Apply the skill's defaults only where the project has no established convention.
- Keep additions in the appropriate existing locations. Do not introduce a competing folder hierarchy, duplicate configuration, second package manager, replacement scaffold or broad reorganization merely to match a preferred template. Scope changes to the requested task and preserve unrelated work.
- **New project:** use the architecture selection workflow only after confirming that the intended target has no existing implementation to preserve, or that the user explicitly requested a separate new application. Respect any parent workspace conventions and existing files.
- **Unclear or unavailable context:** do not assume a blank project. Inspect further or ask for the project path/files if the ambiguity blocks safe implementation; explain the limitation when only advice or a snippet review is possible.
- Briefly state whether the task extends an existing project or starts a new one, and which relevant conventions will guide it. If existing patterns contain a concrete defect or security problem, explain the conflict and make the smallest justified correction within scope; do not reproduce unsafe behavior solely for consistency.

## 1. Inspect before deciding

- Read applicable repository instructions, working-tree status, package manifests, lockfiles, runtime configuration, routes, representative components, tests, and CI. Preserve unrelated work.
- Determine the installed framework and major version, router mode, build tool, package manager, rendering model, styling system, browser targets, deployment platform, and backend/auth boundaries. Read environment variable names only; do not expose secret values.
- Clarify blocking product requirements; resolve ordinary implementation choices using existing conventions. Identify the main user journey, SEO needs, accessibility target, data sensitivity, and whether deployment supports a server runtime.
- Keep a supported existing stack unless there is a concrete reason to change it. Do not turn a small fix into a framework migration or tooling replacement.
- For new projects or architecture decisions, read [architecture.md](references/architecture.md). Record the choice, one credible alternative, and the decisive trade-off briefly.

## 2. Verify versions and sources

- Use the project's actual versions as the baseline. Check official version-matched documentation before relying on unfamiliar or changing APIs, server/client boundaries, caching, authentication helpers, or build settings.
- Use [sources.md](references/sources.md) as the research index, not as a frozen assertion of current versions. Check release notes, migration guides, support status, and security advisories when selecting or upgrading dependencies.
- Distinguish verified facts, engineering preferences, assumptions, and untested behavior. If sources are unavailable, state the gap and use conservative, already-established patterns. Never invent an API or claim a dependency is current or vulnerability-free.
- Avoid prerelease features unless requested or already intentional in the project. Use one package manager and its committed lockfile; avoid unrelated lockfile churn.

## 3. Implement a coherent vertical slice

- Define acceptance criteria in observable user behavior, including relevant loading, empty, validation, success, and failure states.
- Read [code-hygiene.md](references/code-hygiene.md) before substantial JavaScript/TypeScript, component, state, or API changes.
- Use semantic HTML first. Keep local state local, derive values instead of duplicating state, and isolate data access from presentation at a scale justified by the project.
- Prefer TypeScript strict checking for new application code; migrate existing JavaScript incrementally when warranted. Validate untrusted inputs at runtime: a TypeScript assertion is not validation.
- Reuse existing components, tokens, utilities, and framework primitives before adding packages or abstractions. Require a concrete use case for global state, generic repositories, micro-frontends, or a design-system rewrite.
- Preserve errors and cancellation semantics. Do not conceal failed operations behind success UI, fallback mock data, blanket catches, or disabled checks.
- Use the user's language for communication and existing repository conventions for code. Avoid introducing a new naming language mid-project.

## 4. Review boundaries and user experience

- Read [security.md](references/security.md) for auth, forms, external content, uploads, third-party scripts, environment variables, API calls, server actions, or browser storage.
- Treat all browser code and client-exposed configuration as public. Keep secrets and authoritative permission checks on the server. Treat server actions and API routes as directly callable endpoints.
- Read [ux-performance.md](references/ux-performance.md) for UI work. Use WCAG 2.2 AA as an engineering target unless a different requirement is supplied; do not claim legal or full WCAG compliance from a checklist or automated scan.
- Maintain responsive layouts, keyboard operation, visible focus, labels, readable errors, and reduced-motion behavior. Validate real content and all relevant interaction states.
- Profile before adding memoization, virtualization, workers, or architectural complexity. Choose performance budgets for the actual route and users.

## 5. Verify proportionately

Read [verification.md](references/verification.md). Discover the actual repository commands; do not assume that a script named `test`, `lint`, or `typecheck` exists.

- Run relevant formatting/lint, type checks, focused tests, and production build when warranted by the change. Separate pre-existing failures from regressions.
- For meaningful interaction or layout changes, exercise the affected flow in a browser at representative viewport sizes when a browser is available. Include keyboard and error paths.
- For security-sensitive changes, exercise negative cases, including unauthorized access and malformed input, in an authorized test environment.
- Add behavior-based regression tests for risky logic or reproducible bugs. Do not add tests that merely restate trivial implementation or create a test stack for a cosmetic change.
- Do not weaken tests, type safety, linting, accessibility, or security settings just to make checks pass.
- If a check cannot run, report it explicitly. A successful build does not prove runtime correctness, security, accessibility, or production performance.

## 6. Deliver evidence

Summarize what changed, the reason, checks actually run, and material remaining limitations. For reviews, report actionable findings with severity, file location, observed evidence, impact, and a specific repair; distinguish confirmed bugs from hypotheses. Avoid broad certification language. Respect the user's deployment and approval scope.

## Reference routing

- [architecture.md](references/architecture.md): stack selection, rendering, state and boundaries.
- [code-hygiene.md](references/code-hygiene.md): types, components, asynchronous work and dependency discipline.
- [security.md](references/security.md): browser trust, XSS, sessions, CSRF, CSP and supply chain.
- [ux-performance.md](references/ux-performance.md): accessible responsive UI, CSS, performance and SEO.
- [verification.md](references/verification.md): meaningful tests, validation scope and completion evidence.
- [sources.md](references/sources.md): dated primary-source research and refresh rules.
