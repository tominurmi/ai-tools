---
name: pi-maintenance
description: Inspect, configure, troubleshoot and maintain Pi and this package's usage, background-agents and modes extensions. Use for Pi extensions, skills, MCP, model configuration, themes, TUI, SDK and usage-widget questions. Do not use for unrelated coding tasks.
compatibility: Pi coding agent; reference APIs verified against Pi 1.5.2. Recheck the active version before changes.
metadata:
  author: Tomi Nurmi
  web: https://tominurmi.net
---

# Pi maintenance

Use this skill as an on-demand navigation aid, not a replacement for current official documentation or higher-priority instructions.

## Workflow

1. Read [the reference](references/pi-reference.md). Resolve relative paths from this skill's directory, not the current working directory.
2. Identify the active Pi version with `pi --version` when commands are allowed, or use harness-provided installation metadata. Locate that installation's package root. Do not assume a user's home directory, a fixed release path or a global npm layout. In read-only planning mode, use available metadata and explain anything you cannot verify.
3. Read the relevant official documentation and examples before implementing changes. Resolve `docs/` and `examples/` beneath the active Pi package root. Follow relevant cross-references and any requirement to read documents in full. Prefer focused source inspection over dumping model catalogs or source maps.
4. For the `pi-tweaks` extensions, locate the actual `pi-tweaks` repository or installed package and read its README, implementation and tests. This copy lives in the ai-tools library: `../..` is not the pi-tweaks package root. Distinguish repository files from separately installed copies; identify the intended target before editing. Do not silently synchronize or replace active installations.
5. Respect Plan/Manual/Auto permissions and user scope. A skill does not grant extra tool permissions, authorize delegation, switch modes or bypass approval. Describe the proposed change and security boundaries before modifying authentication, process management or tool gates.
6. Use mocked tests first. Never read or expose credentials merely to inspect configuration. Resolve authentication through Pi APIs in extension code. Do not send keys to guessed endpoints or make paid calls as a test without authorization.
7. Validate the change using the relevant tests, then report files changed, what was tested, remaining limitations and whether `/reload` is needed. Do not claim live verification based on mocks or source inspection.
8. Update this skill's reference and extension documentation when behavior changes. Keep credentials, personal paths, account-specific observations, session data and transient balances out of documentation. Commit or publish only within the user's requested scope.

## Package documentation

The extension code and documentation remain in the separate `pi-tweaks` package, not in this library. Resolve these paths from its actual package root:

- Usage: `extensions/usage/README.md`
- Background agents: `extensions/background-agents/README.md`
- Execution modes: `extensions/modes/README.md`
- Security boundaries: `SECURITY.md`

Run `npm test` from the pi-tweaks package root when execution is permitted, not from ai-tools. Individual suites are documented in each extension README. Installing pi-tweaks exposes its bundled skill as `/skill:pi-maintenance`; adding this copy to a checkout alone does not activate it globally. When updating this library copy, compare it with the package's bundled skill to avoid drift.
