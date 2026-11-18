---
name: godot-development
description: Implement, debug, refactor, and review Godot projects using version-verified engine APIs, typed GDScript, maintainable scene/resource architecture, and practical validation. Use for Godot, GDScript, project.godot, .gd/.tscn/.tres files, 2D/3D gameplay, UI, signals, physics, animation, resources, editor tools, performance, and export problems. Support Norwegian and English. Exclude game design without Godot implementation work and unrelated software.
metadata:
  author: Tomi Nurmi
  web: https://tominurmi.net
---

# Godot Developer

Deliver maintainable, idiomatic Godot implementations. Treat these as engineering defaults; follow project conventions and user requirements when they differ. Verify engine behavior instead of pretending to know every API.

## 1. Establish context

Read applicable project instructions, `project.godot`, relevant scenes/scripts, dependencies, and CI/export configuration. Inspect actual scene wiring before editing scripts.

Determine the configured engine executable's version with `--version` when available. Distinguish it from project feature flags/minimum requirements. Preserve the engine version unless migration is requested. Identify platform, renderer, expected behavior, and existing style/test practices. For isolated snippets, state a narrow version assumption.

Reproduce the problem or establish observable acceptance criteria. Ask only about missing context affecting implementation; continue independent inspection.

## 2. Select and verify

Read [version-and-api.md](references/version-and-api.md) for uncertain APIs, version-sensitive work, migrations, or platform differences. Verify unfamiliar, uncertain, or pivotal APIs against version-matched official class references, including inherited members.

Use [engine-systems.md](references/engine-systems.md) to identify suitable built-ins before creating custom subsystems. Prefer the simplest adequate solution; do not add motor features solely to display knowledge.

Use [scenes-and-resources.md](references/scenes-and-resources.md) for boundaries, dependencies, signals, references, mutable data, and lifetime. Explain significant choices briefly. Avoid speculative frameworks, unnecessary Autoloads, and dependencies without a concrete need.

## 3. Implement

Read [gdscript-hygiene.md](references/gdscript-hygiene.md) when authoring/refactoring GDScript. Prefer typed contracts, small responsibilities, and explicit dependencies.

Preserve observable behavior during refactoring unless changes are requested. Include required scene, resource, Input Map, and configuration edits. Preserve unrelated work and resource identity; avoid wholesale formatting/serialization churn.

Handle lifetime and async state explicitly. Do not hide broken required dependencies with silent early returns.

For standalone examples, include node types, scene setup, exported assignments, input actions, and version assumptions. Distinguish complete code from pseudocode.

## 4. Verify

Read [testing-and-debugging.md](references/testing-and-debugging.md). Run available checks appropriate to the change using the project version.

Distinguish parsing, import, runtime behavior, visual/input checks, and export. Do not treat successful parsing as proof that the game works.

Use [review-checklist.md](references/review-checklist.md) for relevant failure modes. Report behavioral findings and evidence before style preferences.

If the engine/device is unavailable, complete useful static checks and specify concrete remaining runtime checks. Never claim unperformed checks passed.

## 5. Report

State resulting behavior, important choices, executed checks, and material limitations. Link sources for pivotal/version-sensitive decisions when useful. Match the user's language while retaining project code conventions. Do not claim exhaustive knowledge or permanent compatibility.

## Reference map

| Task | Reference |
| --- | --- |
| Version/API/migration | `references/version-and-api.md` |
| GDScript authoring/refactoring | `references/gdscript-hygiene.md` |
| Architecture/signals/data/lifetime | `references/scenes-and-resources.md` |
| Engine feature selection | `references/engine-systems.md` |
| Validation/debugging/performance/export | `references/testing-and-debugging.md` |
| Code review | `references/review-checklist.md` |
