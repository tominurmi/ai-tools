# Codex agents

Custom agents for OpenAI Codex. Each `agents/*.toml` is one agent (`name`, `description`, `sandbox_mode`, `developer_instructions`).

## Install

Per project (commit it so the team gets the agents):

```sh
mkdir -p .codex/agents && cp codex/agents/*.toml .codex/agents/
```

Globally (all your projects):

```sh
mkdir -p ~/.codex/agents && cp codex/agents/*.toml ~/.codex/agents/
```

Codex identifies an agent by its `name` field, not the file name. Start a new Codex session to load them.

## Use

Codex only spawns subagents when asked, so name the agent: "Have service_designer write a spec for this user story."

Pipeline: `service_designer` → `elbits_ux_designer` → `elbits_ui_designer` → `elbits_frontend_developer`, with `a11y_specialist` consulted along the way. Agents cannot spawn each other, so each one tells the parent agent which agent it needs next.

To let Codex delegate on its own, add this to the project `AGENTS.md`:

```md
## Delegation
- New user story or feature idea: spawn `service_designer` first, then `elbits_ux_designer` with its spec.
- UI work needs a UX spec and wireframes in `docs/ux/` from `elbits_ux_designer`; without them, spawn that agent first.
- Spawn `a11y_specialist` for design and code review of any UI, and `elbits_frontend_developer` for implementation.
```

## Requirements

- Agents use `sandbox_mode = "workspace-write"` so they can write specs and prototypes. Subagents inherit the parent's approval policy.
- Skills used by the agents: `elbriks-design-system` (UX, UI, frontend), `uutilsynet` (a11y) and `elbits-brand-design`. Install them as Codex skills, or the agents will ask for the source and not invent values.
- Web access (research, Nav Aksel) depends on your Codex network and search settings.
- `elbits_*` agents are specific to elbits.no products. `service_designer` and `a11y_specialist` are not.
