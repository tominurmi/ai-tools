# Claude Code agents

Subagents for Claude Code. Each `agents/*.md` is one agent (frontmatter plus instructions).

## Install

Per project (commit it so the team gets the agents):

```sh
mkdir -p .claude/agents && cp claude/agents/*.md .claude/agents/
```

Globally (all your projects):

```sh
mkdir -p ~/.claude/agents && cp claude/agents/*.md ~/.claude/agents/
```

A project agent overrides a global agent with the same name. Restart Claude Code, or run `/agents`, to load them.

## Use

Claude delegates automatically from each agent's description, or you can name one: "Have service-designer write a spec for this user story."

Pipeline: `service-designer` → `elbits-ux-designer` → `elbits-ui-designer` → `elbits-frontend-developer`, with `a11y-specialist` consulted along the way. Agents cannot spawn each other, so each one tells the main session which agent it needs next.

## Requirements

- Skills used by the agents: `elbriks-design-system` (UX, UI, frontend), `uutilsynet` (a11y) and `elbits-brand-design`. Install them in the same scope (`.claude/skills/` or `~/.claude/skills/`), or the agents will lack their rules.
- `elbits-*` agents are specific to elbits.no products. `service-designer` and `a11y-specialist` are not.
