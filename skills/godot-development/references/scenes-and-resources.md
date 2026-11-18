# Scenes, resources and lifetime

## Choose building blocks

| Need | Starting point |
| --- | --- |
| Tree/input/processing/visual participation | Appropriate Node subtype |
| Reusable hierarchy | Scene stored as PackedScene |
| Inspector-editable serializable definitions | Resource |
| Nonvisual logic/state without tree lifecycle | RefCounted or built-in values |
| Project-wide service persisting across scenes | Carefully scoped Autoload |

Compose independent capabilities; inherit meaningful shared contracts. Do not make all data nodes or all services global managers.

Keep scenes independent of unknown ancestors/siblings. Supply external dependencies through a parent/composition root. Use methods to request behavior and signals to announce events. Treat “signal up, call down” as a heuristic, not a ban on valid explicit references.

Give groups a membership contract. Do not use discovery to conceal missing dependencies. Mark scene-unique nodes before using `%Name`; check scene/owner scope, since names are not universal cross-scene IDs. Cache useful stable references; avoid per-frame descendant searches.

Scope Autoloads carefully, define initialization/reset, and avoid retaining disappearing scene nodes. Autoload does not prohibit additional class instances.

## Initialization and ownership
- Do not assume exports/children are configured in `_init()`.
- Parents enter the tree before children; children become ready before parents. Inject prerequisites before `add_child()` when required at readiness, or design an explicit setup phase.
- `@onready` is not constructor-time access. `_ready()` normally runs once; consider `request_ready()` or explicit reinitialization for pooled/reinserted nodes.
- Distinguish parent hierarchy from owner serialization membership. `add_child()` alone does not guarantee packed-scene persistence.
- Freeing a node frees children; removal alone does not free it. Track detached and queued-for-deletion nodes.
- Prevent duplicate connections during repeated setup. Connections normally disappear when participating objects are freed; disconnect when a living object should stop observing.

## Mutable resources
Loaded resources may be shared across instances. Keep definitions separate from per-instance health/count/state, or explicitly isolate mutable resources.

Use `resource_local_to_scene` when its instantiation contract fits; changes after instantiation are not retroactive. Verify version-specific shallow/deep/nested-copy semantics. Test arrays, dictionaries and nested resources; do not assume `duplicate(true)` isolates every graph in every version.

Emit `changed` for meaningful custom resource updates when observers need it. Avoid required constructor parameters in resources created by editor/loading/duplication paths unable to supply them.

## Async
After `await`, re-evaluate external object validity, active scene, and operation relevance. Use request/generation tokens for superseded work where needed. Do not assume signals arrive after emitter cancellation/destruction; avoid cleanup that depends on already-freed objects resuming.

Use deferred operations for actual callback/thread restrictions, not as a universal initialization fix. Define timer/tween pause/time-scale behavior.

Official references:
- [Scenes](https://docs.godotengine.org/en/stable/tutorials/best_practices/scene_organization.html)
- [Node alternatives](https://docs.godotengine.org/en/stable/tutorials/best_practices/node_alternatives.html)
- [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)
- [PackedScene](https://docs.godotengine.org/en/stable/classes/class_packedscene.html)
- [Resource](https://docs.godotengine.org/en/stable/classes/class_resource.html)
- [Unique nodes](https://docs.godotengine.org/en/stable/tutorials/scripting/scene_unique_nodes.html)
- [Historical Autoload guide, 4.2](https://docs.godotengine.org/en/4.2/tutorials/best_practices/autoloads_versus_internal_nodes.html): verify current APIs separately.
