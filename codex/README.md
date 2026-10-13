# Codex agents and skills

Custom agents and skills for OpenAI Codex.

- `agents/*.toml`: one agent each (`name`, `description`, `sandbox_mode`, `developer_instructions`).
- `skills/<name>/`: one skill each (`SKILL.md`, `references/` and optional `agents/openai.yaml` for UI metadata and invocation policy).

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

Skills, per project or globally:

```sh
mkdir -p .agents/skills && cp -R codex/skills/* .agents/skills/
mkdir -p ~/.agents/skills && cp -R codex/skills/* ~/.agents/skills/
```

## Skills

- `front-end-development`: build, debug, refactor and review web frontends (architecture, security, accessibility, performance, testing). Codex can use it implicitly, or call it with `$front-end-development`.

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
