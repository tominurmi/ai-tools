# GDScript hygiene

Apply these defaults to new code; respect working project conventions and version-supported syntax.

## Types and contracts
- Type public parameters/returns, dependencies and important state. Use `-> void` for procedures and `:=` for clear inference; inspect inference from Variant-returning APIs.
- Use supported typed collections. Keep intentional `Variant` boundaries explicit and validate imported/received data.
- Use `class_name` for useful public contracts; avoid global name collisions, including Autoload names.
- Distinguish typing from nullability/lifetime. Casts can fail and node references can become invalid. Handle optional/external references deliberately and diagnose missing required configuration clearly.
- Check error returns and file/load failures. Do not rely only on assertions for external input or release-critical validation.

## Readability
Follow project conventions; otherwise use Godot's style guide: tabs, UTF-8/LF, snake_case functions/members/files, PascalCase classes, uppercase snake-case constants, readable lines under 100 characters, and consistent declaration order. Treat underscore prefixes as a convention, not access control.

Keep functions cohesive, use meaningful guards, name units, and extract repeated domain rules. Avoid duplicated logic, unexplained magic values, dead code, huge managers, and speculative abstractions.

Prefer typed method references/signal members over string calls for known relationships. Use reflection, groups, and dictionaries when runtime discovery actually requires them.

Document public contracts, units, side effects and lifetime with `##`. Explain reasons in ordinary comments; remove abandoned commented code.

## Warnings and refactoring
Investigate new warnings. Apply project-appropriate type-safety settings. Suppress understood warnings only at a narrow scope with a reason, using annotations supported by the engine version. Do not disable categories globally to make a patch appear clean.

Establish representative behavior before refactoring, change one boundary at a time, and preserve contracts. Prioritize substantive defects over style preferences.

Official references:
- [Style](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html)
- [Typing](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/static_typing.html)
- [Language](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html)
- [Warnings](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/warning_system.html)
- [Documentation comments](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_documentation_comments.html)
