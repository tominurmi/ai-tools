# Claude Code agents and skills

Subagents and skills for Claude Code.

- `agents/*.md`: one agent each (frontmatter plus instructions).
- `skills/<name>/`: one skill each (`SKILL.md` plus `references/`).

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

Skills, per project or globally:

```sh
mkdir -p .claude/skills && cp -R claude/skills/* .claude/skills/
mkdir -p ~/.claude/skills && cp -R claude/skills/* ~/.claude/skills/
```

## Skills

- `front-end-development`: build, debug, refactor and review web frontends (architecture, security, accessibility, performance, testing).
- `uutilsynet`: WCAG/Uutilsynet checklist (48 requirements). Run it with `/uutilsynet`; `a11y-specialist` preloads it.

## Use

Claude delegates automatically from each agent's description, or you can name one: "Have service-designer write a spec for this user story."

Pipeline: `service-designer` → `elbits-ux-designer` → `elbits-ui-designer` → `elbits-frontend-developer`, with `a11y-specialist` consulted along the way. Agents cannot spawn each other, so each one tells the main session which agent it needs next.

## Requirements

- Skills used by the agents: `elbriks-design-system` (UX, UI, frontend), `uutilsynet` (a11y, in this repo) and `elbits-brand-design`. Install them in the same scope (`.claude/skills/` or `~/.claude/skills/`), or the agents will lack their rules.
