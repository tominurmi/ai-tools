# Pi maintenance reference

Adapted from a local Pi reference. APIs were verified against **Pi 1.5.2**; recheck the active installation before relying on them. This is a navigation aid, not authoritative API documentation.

## Locate documentation

Find the active package root using harness-provided paths or the installed `pi` executable and package metadata. Some installations keep releases beneath `~/.pi/agent/install/releases/<version>/node_modules/@earendil-works/pi-coding-agent`; this is an example, not a universal layout.

Resolve these paths beneath the active package root:

| Topic | Documentation / example |
| --- | --- |
| Overview | `README.md` |
| Extensions and lifecycle | `docs/extensions.md` |
| Footer/widget examples | `examples/extensions/status-line.ts`, `examples/extensions/model-status.ts` |
| Terminal UI | `docs/tui.md` |
| MCP | `docs/mcp.md` |
| Skills, templates and themes | `docs/skills.md`, `docs/prompt-templates.md`, `docs/themes.md` |
| Packaging | `docs/packages.md` |
| Models and providers | `docs/models.md`, `docs/models-configuration.md`, `docs/custom-provider.md` |
| Context and compaction | `docs/compaction.md` |
| Commands | `docs/usage.md`, `docs/slash-commands.md` |
| SDK | `docs/sdk.md` |
| RPC and background processes | `docs/rpc.md`, `docs/rpc-commands.md`, `docs/rpc-extension-ui.md`, `docs/json.md` |

## Common extension APIs

```ts
import type { ExtensionAPI } from "@earendil-works/pi-coding-agent";

export default function (pi: ExtensionAPI) {
  pi.on("session_start", (_event, ctx) => {
    if (ctx.hasUI) ctx.ui.setWidget("example", ["Status text"], { placement: "aboveEditor" });
  });
  pi.on("session_shutdown", (_event, ctx) => {
    if (ctx.hasUI) ctx.ui.setWidget("example", undefined);
  });
}
```

- Global extensions normally load from `~/.pi/agent/extensions/`; project extensions load from trusted `.pi/extensions/`. Packages declare their entries in `package.json`.
- `/reload` reloads resources. Explicit temporary loading: `pi -e /path/to/extension.ts`.
- `ctx.ui.setStatus(key, text)` sets footer status; `undefined` removes it.
- `ctx.ui.setWidget(key, lines, options)` sets a widget; `undefined` removes it. `setHeader` replaces the header, which may scroll out of view.
- Use semantic colors through `ctx.ui.theme.fg`. Guard dialogs/widgets with `ctx.hasUI`, and terminal-only components with `ctx.mode === "tui"`.
- `ctx.modelRegistry.getApiKeyForProvider(provider)` resolves credentials; `getProviderAuth(provider)` resolves fuller auth/configuration. Do not read `auth.json` directly in adapters.
- `model_select` reports user/model switching; session restoration requires initialization from `ctx.model` in `session_start`.
- `agent_settled` is the final idle notification; `agent_end` can occur before retries or continuations.
- Start long-lived resources in session events, not extension factories. Abort network requests and clear timers in `session_shutdown`, including reload/session replacement.
- Set timeouts, avoid overlapping refreshes, and label stale data. Never display raw credential-bearing errors.

## Package extension map

Paths here are relative to the repository/package root, three directories above this reference file's directory. Read the extension READMEs for current details.

### Usage

Entry: `extensions/usage/index.ts`. Styling: `style.ts`. Adapters: `providers/codex.ts`, `providers/openrouter.ts`, `providers/claude.ts`.

- One widget follows the selected model's provider. Unsupported providers such as Nous show only a display name, without usage requests.
- `/usage` refreshes/reports all supported configured providers. Internal adapter commands are captured by the coordinator.
- Adapters declare `{ provider, install }` and use exact provider IDs, not model-name guesses.
- Refresh on startup/model selection, every five minutes, and after agent settlement (throttled to once per minute). Manual refresh shares an in-flight request.
- Missing credentials hide supported adapters. Rejected credentials retain an unavailable/stale warning. Authentication-resolution failures must not expose raw diagnostics.
- `Promise.allSettled` isolates unexpected command failures. Codex uses fixed safe error messages. Partial OpenRouter credit failures retain key data and show a warning.
- Quota bars turn amber at 25% remaining and red at 10%; stale data is marked. Terminal wrapping is ANSI-aware; non-TUI output remains plain.

Data sources:

- **Codex:** read-only `GET https://chatgpt.com/backend-api/wham/usage`, using `openai-codex` OAuth and a `ChatGPT-Account-Id` header. Decode the account claim only for routing; decoding is not JWT verification. Derive labels from returned window durations. This is not a stable public API.
- **Claude:** read-only `GET https://api.anthropic.com/api/oauth/usage`, using `anthropic` browser OAuth and `anthropic-beta: oauth-2025-04-20`. No browser cookies or API-key quota inference. Supported five-hour/weekly/Opus/Sonnet windows only; no extra paid-usage reporting. This is not a stable public API; mocked tests do not establish live account compatibility.
- **OpenRouter:** `GET https://openrouter.ai/api/v1/key` and `/credits`. Account credits equal `total_credits - total_usage`; key budget uses `limit_remaining`. These are different balances. Uncapped keys do not imply unlimited account credit.
- No Nous usage/OAuth adapter is included. A newly configured provider is not automatically supported; verify its API and permitted authentication flow before implementation.

### Background agents

Entry: `extensions/background-agents/index.ts`; supporting modules: `manager.ts`, `ui.ts`, `guard.ts`, `security.ts`.

- `/agent` launches with access/model selection; `/agents` opens the native inspector. Exact unique model IDs bypass the picker; ambiguous hints do not silently select.
- `subagent` supports run/list/result/message/cancel/close. Delegate only when requested, with a self-contained task. Completion is notified; do not poll in a loop.
- Maximum three live child processes, including idle chats. Each consumes its own quota.
- Default read/find/ls access is scoped to source paths; recursive grep is disabled. Workspace mode adds shell/edit/write with explicit approvals. This is not an OS sandbox.
- Child environments use an allowlist. Stored Pi authentication remains available; parent environment-only keys are not inherited. Common secrets are redacted on a best-effort basis, not guaranteed.
- Children disable extension discovery, skills, templates and MCP; only their guard loads. No built-in browser verification. Do not claim a live-page audit from source inspection.
- Reload/session replacement/shutdown closes children. Transcripts remain under the active Pi agent directory's `background-agents/<session-id>/` tree; do not commit them. Close a child before independently resuming its saved session.
- Pi 1.5.2's exported RpcClient lacks a public UI-response method; this extension uses documented JSONL directly.

### Execution modes

Entry: `extensions/modes/index.ts`.

- `/mode` picker: Auto / Plan / Manual. Direct mode commands also work. Default is Manual on every startup/reload/session replacement; no persisted mode or shortcut.
- Manual automatically permits only built-in read/grep/find/ls. Other calls use Allow once / Change to auto / View details / Deny. Full arguments open separately; edits to the review view are ignored.
- Allow once and Enable auto are first choices in their respective menus; Enter can approve. Escape, timeout, cancellation, missing UI and errors fail closed. Oversized previews are blocked rather than truncated.
- Change to auto requires separate confirmation, approves the waiting call and enables Auto. `/mode` changes otherwise require idle state.
- Plan blocks all other tools and asks for a numbered plan. No automatic post-plan execution menu is implemented. PLAN is teal in TUI, darker on light themes.
- Auto disables only this extension's gate, not other safety requirements. User shell/slash commands, trusted extension code and already-running background agents are outside the gate. Reading tools retain filesystem access; this is not a sandbox.

## Token usage versus quota

- `/session` shows session tokens/cost; footer context percentage shows occupied context, not subscription quota.
- Repeated input can count across requests, even with caching. `/compact` summarizes older context; `/new` starts a fresh conversation. Neither removes installed extensions.
- In Pi 1.5.2, the default compaction reserve is 16,384 tokens. The trigger is context tokens above context window minus reserve. `keepRecentTokens` defaults to 20,000 and is not an additional reserve.
- Context limits depend on the selected provider/model entry. Never hardcode the model active when these notes were written.

## MCP quick reference

```sh
pi mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem .
pi mcp add docs --url https://example.com/mcp
pi mcp list
```

These are examples, not instructions to install or execute a server automatically. Only configure trusted servers. Use `--local` for project configuration; typical files are `~/.pi/agent/mcp.json` or project `.pi/mcp.json`. `/mcp` inspects connections/sign-in, and `/reload` loads external configuration changes. Pi 1.5.2 uses streamable HTTP for remote MCP, not legacy SSE.
