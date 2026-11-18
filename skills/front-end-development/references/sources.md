# Research and primary sources

Research date: 2026-10-13. The guidance is an engineering synthesis, not a finding that one framework is universally best. Use the links to verify the installed version and current API, support and security status at the time of work. Do not interpret this date as a guarantee that every linked page is unchanged or that all framework releases have been assessed.

## Conclusions to apply

Select architecture from content, interaction, deployment and maintenance needs. Keep the core skill framework-neutral and read framework-specific documentation on demand. Make code hygiene observable through types, coherent responsibilities and checks. Treat browser/server trust boundaries, accessibility and performance as design inputs. Require evidence proportionate to the change, and report unverified behavior honestly.

## Frameworks and rendering

| ID | Official source | Research use |
| --- | --- | --- |
| R1 | [React: Creating a React App](https://react.dev/learn/creating-a-react-app) | Framework-first recommendation and deliberate from-scratch alternatives. |
| R2 | [React: Build from Scratch](https://react.dev/learn/build-a-react-app-from-scratch) | Responsibilities outside the UI library. |
| R3 | [Vue: Introduction](https://vuejs.org/guide/introduction.html) | Incremental adoption and component model. |
| R4 | [Nuxt: Rendering Modes](https://learn.nuxt.com/en/concepts/rendering-modes) | Universal, client and hybrid rendering. |
| R5 | [SvelteKit: Introduction](https://svelte.dev/docs/kit/introduction) | Routing, rendering and application features. |
| R6 | [Angular: Overview](https://angular.dev/overview) | Integrated framework capabilities. |
| R7 | [Astro: Islands](https://docs.astro.build/en/concepts/islands/) | Selective interactivity and hydration. |

## Code quality and security

| ID | Official source | Research use |
| --- | --- | --- |
| R8 | [TypeScript: strict](https://www.typescriptlang.org/tsconfig/strict.html) | Compiler checks and upgrade implications. |
| R9 | [typescript-eslint: Typed linting](https://typescript-eslint.io/getting-started/typed-linting/) | Type-aware rules and performance trade-offs. |
| R10 | [React: You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect) | Derived state and external synchronization. |
| R11 | [OWASP: Web Frontend Security](https://cheatsheetseries.owasp.org/cheatsheets/Web_Frontend_Security_Cheat_Sheet.html) | Browser trust and frontend attack surface. |
| R12 | [OWASP: XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html) | Contextual encoding, safe sinks and sanitization. |
| R13 | [OWASP: HTML5 Security](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html) | Browser storage and cross-document messaging. |
| R14 | [OWASP: CSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) | Cookie-authenticated mutation protection. |
| R15 | [MDN: CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP) | Nonces, hashes and policy deployment. |
| R16 | [Next.js: Data Security](https://nextjs.org/docs/app/guides/data-security) | Server entry points, authorization and data exposure. |
| R18 | [Vite: Environment Variables and Modes](https://vite.dev/guide/env-and-mode) | Client-exposed environment values and build-time behavior. |
| R23 | [npm: audit](https://docs.npmjs.com/cli/v11/commands/npm-audit/) | Audit behavior and repair implications. |

## Accessibility, performance and validation

| ID | Official source | Research use |
| --- | --- | --- |
| R17 | [W3C: WCAG 2.2](https://www.w3.org/TR/WCAG22/) | Accessibility requirements; an engineering target is not a legal opinion. |
| R19 | [web.dev: Web Vitals](https://web.dev/articles/vitals) | Field thresholds and 75th-percentile measurement. |
| R20 | [Playwright: Best Practices](https://playwright.dev/docs/best-practices) | User-facing locators, isolation and reliable browser checks. |
| R21 | [Testing Library: Guiding Principles](https://testing-library.com/docs/guiding-principles/) | Behavior-oriented component tests. |
| R22 | [npm: ci](https://docs.npmjs.com/cli/v11/commands/npm-ci/) | Reproducible installs; use the project's npm-version docs when different. |
| R24 | [MDN: Semantic HTML](https://developer.mozilla.org/en-US/curriculum/core/semantic-html/) | Native structure and accessibility fundamentals. |

## Evidence limits and refresh

The Nuxt 4 rendering guide URL returned a retrieval error during research; the official Nuxt learning page above was retrieved instead. Do not use the failed page as evidence of Nuxt 4 API behavior. No comparative framework benchmark, live application audit, exhaustive advisory review or legal assessment was performed for this skill.

Refresh targeted sources when choosing a new stack, changing a major version, touching authentication/caching/rendering behavior, adopting unfamiliar browser APIs, or responding to a security advisory. Read source content, not only search snippets. Check source version and publication status; distinguish stable guidance from previews. Preserve links and verification dates in significant architectural decisions without copying whole documentation pages into the skill.
