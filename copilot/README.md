# GitHub Copilot agents

Custom agents for GitHub Copilot in VS Code.

- `agents/*.agent.md`: one agent each (frontmatter with `name`, `description`, `argument-hint`, `tools`, `agents` and `handoffs`, plus instructions).

## Install

Per project (commit it so the team gets the agents):

```sh
mkdir -p .github/agents && cp copilot/agents/*.agent.md .github/agents/
```

Globally (all your projects):

```sh
mkdir -p ~/.copilot/agents && cp copilot/agents/*.agent.md ~/.copilot/agents/
```

Pick the agent in the agent dropdown in Copilot Chat. Copilot identifies an agent by its `name` field.

## Use

Select an agent and describe the task, for example `service-designer` with a user story.

Pipeline: `service-designer` → `elbits-ux-designer` → `elbits-ui-designer` → `elbits-frontend-developer`, with `a11y-specialist` consulted along the way.

- Handoffs: when an agent is done, it shows buttons for the next step (for example "Hand over to UX designer"). The button switches agent and fills in the prompt. You review and send it.
- Subagents: `elbits-ui-designer` and `elbits-frontend-developer` run `a11y-specialist` as a subagent for guidance and review. The a11y agent reports findings only; the calling agent makes the fixes.

## Requirements

- VS Code with GitHub Copilot and custom agent support. Subagents need the `agent` tool to be enabled.
- Skills used by the agents: `elbriks-design-system` (UX, UI, frontend), `uutilsynet` (a11y) and `elbits-brand-design`. Install them as Copilot agent skills (`.github/skills/` or `~/.copilot/skills/`), or the agents will ask for the source and not invent values.
- Web access (research, Nav Aksel) uses the `web` tool.
