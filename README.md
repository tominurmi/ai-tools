# ai-tools

A shared library of agent roles and skills for AI coding tools. Maintain each role and skill once; adapt it manually to the tool you use.

## Structure

```text
agents/                         Tool-independent role instructions
  frontend-developer.md
  ux-designer.md
  ui-designer.md
  service-designer.md
  a11y-specialist.md
  ios-developer.md
  elbits/                       Elbits-specific roles
    elbits-frontend-developer.md
    elbits-ux-designer.md
    elbits-ui-designer.md
skills/                         Each skill has SKILL.md and references/
  front-end-development/
  uutilsynet/
  design-and-validate-games/
  godot-development/
  ios-development/
  pi-maintenance/
```

The original content is based on the former Claude versions, supplemented with locally maintained game design, Godot, iOS and Pi maintenance skills. Agent files are ordinary Markdown, not tool-specific configuration. Skills retain their `SKILL.md` metadata and relative reference structure.

## Agents

| Agent | Role |
| --- | --- |
| [service-designer](agents/service-designer.md) | Questions the problem in a user story or idea, then writes a handover spec. Never designs. Not brand-specific |
| [ux-designer](agents/ux-designer.md) | Brand-independent information architecture, user flows, wireframes, solution options and usability review |
| [ui-designer](agents/ui-designer.md) | Brand-independent clickable HTML prototypes from a UX spec, using the project's design system or a proposed token foundation |
| [frontend-developer](agents/frontend-developer.md) | Brand-independent frontend implementation, debugging, refactoring and review, based on `front-end-development` |
| [a11y-specialist](agents/a11y-specialist.md) | Audits and fixes WCAG 2.2 AA issues, including Nav Aksel practice. Not brand-specific |
| [ios-developer](agents/ios-developer.md) | Native iOS/iPadOS implementation, debugging and review with Xcode, Swift, SwiftUI and UIKit |
| [elbits-ux-designer](agents/elbits/elbits-ux-designer.md) | Information architecture, user flows, wireframes and solution options for Elbits projects. Never does UI design |
| [elbits-ui-designer](agents/elbits/elbits-ui-designer.md) | Clickable HTML prototypes with `elbriks-design-system`, from the UX spec only |
| [elbits-frontend-developer](agents/elbits/elbits-frontend-developer.md) | Implements, refactors, debugs and optimizes Elbits UI code |

Pipeline: service designer → UX designer → UI designer → frontend developer, with the a11y specialist consulted along the way.

UX accepts a service-design spec or equivalent product brief. UI requires a UX spec, wireframes and handover brief from the UX agent or equivalent project documentation. A complete design pipeline is not required for debugging, refactoring or bounded changes with clear requirements.

The general agents do not require company-specific skills. The Elbits agents reference `elbriks-design-system` and, for branding work, `elbits-brand-design`. These skills are not included and must be supplied separately.

## Skills

| Skill | Purpose |
| --- | --- |
| [front-end-development](skills/front-end-development/SKILL.md) | Build, debug, refactor and review web frontends: architecture, security, accessibility, performance and testing |
| [uutilsynet](skills/uutilsynet/SKILL.md) | WCAG/Uutilsynet checklist: the 48 requirements Norwegian web solutions are tested against. User-invoked only |
| [design-and-validate-games](skills/design-and-validate-games/SKILL.md) | Game concepts, mechanics, balance, progression and playtesting |
| [godot-development](skills/godot-development/SKILL.md) | Godot implementation, debugging, architecture and validation |
| [ios-development](skills/ios-development/SKILL.md) | Native iOS/iPadOS development with Apple API verification, security and build/test evidence |
| [pi-maintenance](skills/pi-maintenance/SKILL.md) | Pi maintenance and navigation for the separate `pi-tweaks` package; extension code remains in that package |

Pi extension implementation and tests remain in the separate `pi-tweaks` package.

## Use with your tool

- **Agents:** Ask your assistant to read the relevant `agents/<name>.md` (or `agents/elbits/<name>.md` for Elbits roles), or copy its instructions into your tool's custom-agent configuration. These files are not ready-to-install Claude, Codex or Copilot agent definitions. Add names, descriptions, tool permissions, model settings and handoffs yourself where required.
- **Skills:** Copy or link the complete skill directory into a skill location supported by your tool. Keep `SKILL.md`, `references/` and any bundled assets together. If your tool does not discover skills, explicitly ask it to read the relevant `SKILL.md` and follow its instructions.
- **Codex:** Adapt agent instructions manually to the configuration supported by your Codex version. This repository does not maintain TOML variants or Codex-specific metadata.
- **Related skills:** Agent documents list related skills, but this does not preload them. Make them available and read their `SKILL.md` as needed, respecting explicit-invocation restrictions such as those for `uutilsynet`. Resolve library paths from this repository root, or use the actual installed skill location.
- **Tools and delegation:** Configure only tools you actually have. References to other roles do not automatically launch agents or grant permission to delegate. Respect the user's scope and your tool's approval rules.

No generated variants, adapters or build step are needed. Update the shared Markdown files directly.
