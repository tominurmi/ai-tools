# Accessible UI and measured performance

## Usability and CSS

Preserve established components and design tokens for color, type, spacing, focus and motion. Use Grid/Flexbox, content-driven breakpoints and resilient sizing. Test narrow screens, long translations, real data, zoom, text wrapping and both pointer and keyboard input. Do not equate a desktop screenshot with a finished interface.

Use appropriate headings, landmarks, links, buttons, labels and form controls. Prefer native semantics; add ARIA only when necessary and correctly implemented. Implement predictable focus, keyboard operation and focus restoration for overlays. Communicate errors in text near the control and associate them programmatically. Preserve entered data after recoverable failures. Support password managers and pasting in authentication flows.

Target WCAG 2.2 AA as an engineering default: check contrast, visible/unobscured focus, keyboard access, accessible names, reflow, non-color cues and pointer-target requirements including their exceptions. Test reduced motion and use announcements carefully. Automated accessibility checks find only part of the issues; combine them with manual interaction and assistive-technology checks appropriate to scope. Do not claim full conformance without a complete evaluation. Sources: [R17, R24](sources.md).

## Performance

Use field data when available. The Core Web Vitals good thresholds researched on 2026-10-13 are LCP ≤ 2.5 s, INP ≤ 200 ms and CLS ≤ 0.1, evaluated at the 75th percentile with mobile and desktop segmentation. Distinguish these from lab measurements. A Lighthouse score alone is not evidence that real users meet these targets. Recheck the current definitions when applying them. Source: [R19](sources.md).

Define route-specific budgets for delivered JavaScript, critical assets and interactions using the product's device/network profile. Measure before and after under comparable conditions. These budgets are project choices, not universal standards.

Avoid unnecessary client JavaScript and hydration. Split routes or heavy optional features when measurement justifies it. Size and compress images appropriately, reserve dimensions to limit shifts, and avoid lazy-loading the critical hero/LCP image. Load noncritical media lazily. Limit font variants and avoid blocking content unnecessarily. Keep long-running work off critical interactions; consider a worker only for demonstrated computation cost. Avoid speculative memoization and indiscriminate preloading.

## Discoverability and operational behavior

For public content, verify useful initial HTML, descriptive titles, metadata, canonical URLs where appropriate, correct status codes and meaningful not-found behavior. For client-routed applications, test direct deep links, refresh, back/forward and server fallback. Confirm locale-aware number/date formatting and deliberate timezone handling. Test slow requests and failed assets. When using service workers, define update behavior and avoid caching authenticated content without an explicit isolation strategy.
