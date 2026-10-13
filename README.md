# ai-tools

Agents and skills for AI coding tools. Each tool has its own folder with the same agents and skills, adapted to that tool's format.

## Structure

```text
claude/            Claude Code
  agents/*.md      Subagents (frontmatter plus instructions)
  skills/<name>/   Skills (SKILL.md plus references/)
codex/             OpenAI Codex
  agents/*.toml    Custom agents
  skills/<name>/   Skills (SKILL.md, references/, agents/openai.yaml)
```

See [claude/README.md](claude/README.md) and [codex/README.md](codex/README.md) for install and use.

## Agents

| Claude Code | Codex | Role |
| --- | --- | --- |
| `service-designer` | `service_designer` | Questions the problem in a user story or idea, then writes a handover spec. Never designs. Not brand-specific |
| `elbits-ux-designer` | `elbits_ux_designer` | Information architecture, user flows, wireframes and solution options for user testing. Never does UI design |
| `elbits-ui-designer` | `elbits_ui_designer` | Clickable HTML prototype with `elbriks-design-system`, from the UX spec only |
| `elbits-frontend-developer` | `elbits_frontend_developer` | Implements, refactors, debugs and optimizes UI code |
| `a11y-specialist` | `a11y_specialist` | Audits and fixes WCAG 2.2 AA issues, including Nav Aksel practice. Not brand-specific |

Pipeline: service designer → UX designer → UI designer → frontend developer, with the a11y specialist consulted along the way.

## Skills

| Skill | Purpose |
| --- | --- |
| `front-end-development` | Build, debug, refactor and review web frontends (architecture, security, accessibility, performance, testing) |

## Keep the versions in sync

Content is the same for both tools. Only tool-specific parts differ: file format, agent names (kebab-case vs. snake_case), project instruction files (`CLAUDE.md` vs. `AGENTS.md`) and install paths. When you change one version, change the other.
