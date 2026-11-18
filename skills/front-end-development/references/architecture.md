# Architecture and framework selection

Complete the project-context check in SKILL.md first. For an existing project, use its current structure and stack as the baseline; this table does not authorize restructuring or migration. For a new application, also respect any parent workspace conventions.

Use this table as an engineering heuristic, not a benchmark or exclusive mapping. Confirm deployment capabilities and team familiarity before scaffolding. All listed frameworks can serve more than one project type.

| Need | Candidates | Main decision |
| --- | --- | --- |
| Small mostly static site | Semantic HTML/CSS with small JS modules; Astro when content tooling helps | Avoid paying an application-runtime cost without an interaction need. |
| Content site, documentation, marketing | Astro, or an existing framework's static rendering | Prefer useful HTML at first response; hydrate only interactive areas. |
| Interactive dashboard with an existing API | Existing React, Vue, Svelte or Angular stack; Vite where a client build is sufficient | Plan routing, authentication, data fetching, errors and hosting fallback explicitly. |
| Public app with dynamic pages and server work | Next.js, Nuxt, SvelteKit, Angular SSR or an appropriate React framework | Compare rendering, caching, server boundaries, adapters and operational complexity. |
| Larger team seeking integrated conventions | Angular, or well-established conventions in another stack | Evaluate maintenance experience, forms, routing and upgrade costs rather than team size alone. |
| Existing working app | Its current supported stack | Prefer focused improvements over migration without measurable benefit. |

## Distinguish the layers

React is a UI library; Next.js adds application architecture. Vue is a UI framework; Nuxt adds application structure and rendering options. Svelte is a component framework/compiler; SvelteKit supplies application features. Vite is a build tool, not a backend or complete application framework. Angular supplies integrated routing, forms and dependency injection. Astro's islands let interactive components coexist with HTML-oriented pages. Sources: [R1–R7, R18](sources.md).

React's documentation recommends starting new React applications with a framework, while documenting a from-scratch route when its flexibility is justified. A Vite SPA remains a deliberate choice when the API and hosting constraints support it; account for the work that a framework would otherwise provide. Do not use vendor feature descriptions as comparative performance evidence.

## Choose rendering per route

- Use static generation for content that can be built ahead of time, with an explicit refresh strategy.
- Use server rendering when request-time content or first-response HTML is useful and a compatible runtime exists.
- Use client rendering where browser interaction dominates and its loading/deep-link trade-offs are acceptable.
- Use hybrid rendering only when route-level differences justify added caching and deployment complexity.
- Keep personalized data out of shared caches. Define cache scope, invalidation after writes, freshness and logout behavior. Check framework-version defaults instead of assuming caching semantics.
- Avoid browser-only globals during server rendering and initial client/server output mismatches. Do not suppress hydration warnings to hide an unexplained defect.

## Organize by responsibility

Use the framework's routing conventions and project scale. Separate UI composition, domain rules, data access and platform integration where these responsibilities diverge. Colocate tests and feature-specific code when consistent with the repository. Extract shared code after a stable shared purpose emerges; similar syntax alone is insufficient.

Keep ephemeral UI state local; represent shareable navigation/filter state in the URL when appropriate; manage remote data with existing loaders or a server-state cache. Introduce a global store only for demonstrated cross-feature client state. Describe the owner and lifetime of state before choosing a library.

Record architectural decisions in the project's established location: constraints, chosen option, rejected alternative, operational cost and a condition that would justify revisiting the choice.
