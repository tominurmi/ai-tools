# Frontend security

Review controls against the actual threat model. The frontend may collect and display data, but cannot authoritatively enforce permissions. Sources: [R11–R16, R18, R23](sources.md).

## Trust and privileged actions

Treat browser bundles, public environment variables, HTML and serialized hydration data as visible to users. Vite's exposed environment variables are bundled into client code. A gitignored `.env` file does not make a bundled value secret. Keep privileged keys on the server; distinguish intentionally public identifiers from secrets.

Check authentication and resource-level authorization at every protected server entry point. Hidden controls and route guards only shape UX. Server actions must verify callers and input independently of the page that renders them. Return only fields the client needs and keep privileged modules out of client imports. Verify cross-user and cross-tenant isolation, including shared caches. If a real secret was exposed, remove the exposure and coordinate rotation; editing the frontend alone does not revoke it.

## XSS and external content

Use framework text escaping and safe DOM text APIs. Avoid untrusted content in `innerHTML`, `dangerouslySetInnerHTML`, `v-html`, raw-HTML directives and executable URLs. If rich HTML is a genuine requirement, sanitize with a maintained, appropriate sanitizer and constrained policy; do not implement regex sanitization. Validate URL schemes and destinations for their intended use. Sanitization and encoding depend on the output context; one generic escape function does not make every sink safe.

## Sessions, CSRF and browser integration

Prefer a supported authentication implementation. Where the architecture allows it, use server-managed session cookies with Secure, HttpOnly, appropriately scoped Path/Domain and a deliberate SameSite policy. Do not default to keeping session identifiers or long-lived tokens in localStorage. For an existing SPA/provider SDK, inspect its documented token lifecycle and threat model before changing persistence; do not improvise an incompatible cookie flow.

For cookie-authenticated mutations, verify the framework's CSRF protections and appropriate token/origin checks. SameSite is defense in depth for most deployments, not a universal replacement. Do not mutate state via GET. HttpOnly reduces script access to cookies but does not make XSS harmless. CORS is not authorization.

For `postMessage`, verify expected sender origin, source and payload schema and use a precise target origin. Restrict embedded content according to actual needs. Minimize third-party scripts and sensitive data sent to analytics.

## Browser policy and delivery

Design CSP for the actual application and hosting platform. Use suitable hashes for static scripts or unpredictable per-response nonces for dynamic rendering. Never reuse a fixed nonce. Test hydration, scripts, styles and deployment behavior; consider Report-Only while measuring violations before enforcement. Do not resolve problems by broadly permitting unsafe execution. Review framing policy, MIME sniffing protection, referrer policy and Permissions-Policy directives; enable only the browser capabilities the application needs. Headers must be verified on the served response, not merely in a source file.

Review dependency advisories and installation-script risk. A scanner covers known patterns and cannot establish complete security. Test applicable negative cases in a test environment: denied resource access, malicious displayed content, expired sessions, malformed inputs and forged mutations. State server-side controls that remain outside the frontend change.
