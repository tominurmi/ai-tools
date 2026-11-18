# Engine systems lookup map

Identify promising built-ins here, then check actual class contracts for the project version. Candidates are not exhaustive or universally best.

| Area | Candidates | Questions |
| --- | --- | --- |
| Input | Input Map, Input, InputEvent, Control | Continuous/discrete? Which UI consumes events? |
| Physics | CharacterBody, RigidBody, StaticBody, Area, ray/shape queries in 2D/3D | Motion authority, layers/masks, callbacks, units/space? |
| Navigation | NavigationAgent, regions/server | Map ready? Path following versus physical motion? |
| UI | Control, containers, themes, focus neighbors | Sizes, scaling, keyboard/controller focus? |
| Animation | AnimationPlayer, AnimationTree, Tween | Authored tracks, blends or dynamic targets? Property ownership? |
| Time | Timer, SceneTreeTimer, signals | Repeat/cancel, pause/time scale, physics/idle? |
| Audio | AudioStreamPlayer and 2D/3D variants, buses | Spatial, polyphony, scene lifetime? |
| Data | ResourceLoader/Saver, FileAccess, ConfigFile, JSON | Import-aware resources or raw files? Definitions/state? |
| Rendering | Node3D, Camera3D, meshes/materials/lights, MultiMesh | Local/global transforms, sharing, renderer, measured cost? |
| Background work | Threaded loading, WorkerThreadPool, servers | Thread safety, isolated data, handoff? |
| Editor tools | @tool, EditorPlugin, configuration warnings | Editor/runtime context, undo/redo, safe tree edits? |
| Multiplayer | MultiplayerAPI, peers, RPC, MultiplayerSpawner/Synchronizer | Authority, identity, validation, transfer mode? |

Apply relevant rules:
- Use configurable Input Map actions. Use unhandled events for discrete gameplay input after UI handling. Global Input polling is not automatically blocked when GUI consumes events; gate continuous controls when menus/focus require it.
- Use appropriate physics callbacks/body types. Godot 4 character movement sets `velocity` and calls `move_and_slide()` without multiplying velocity by delta again. Integrate acceleration with time; check `move_and_collide()` independently.
- Check movement mode for top-down versus grounded character motion, including scene overrides; do not assume the default suits the game. Verify floor/slope behavior where relevant.
- Let containers lay out children. Use themes/size flags and test several resolutions/focus routes rather than repeatedly overriding child positions.
- Create runnable tweens through Node/SceneTree, not `Tween.new()`. Create fresh tweens for replay and cancel conflicting property animations. Binding aligns lifetime to a node.
- Verify that a tweened property supports useful interpolation; use an interval/callback for discrete changes such as renaming instead of treating identifiers as visual animation values.
- Request/poll threaded loads and retrieve at completion; premature retrieval can block. Avoid arbitrary worker access to the active tree.
- Separate packaged `res://` assets from writable `user://` saves. Version/validate save data. Use staged replacement when interrupted writes matter; check platform semantics.
- For tools, check editor context, avoid destructive property-setter behavior, and use appropriate undo/redo integration.
- Validate received multiplayer intent at the authority boundary. RPC declarations alone are not authorization; verify identity/path and replication configuration.

Official entry points:
- [Input](https://docs.godotengine.org/en/stable/tutorials/inputs/inputevent.html)
- [Input polling semantics](https://docs.godotengine.org/en/stable/classes/class_input.html)
- [Physics](https://docs.godotengine.org/en/stable/tutorials/physics/physics_introduction.html)
- [Containers](https://docs.godotengine.org/en/stable/tutorials/ui/gui_containers.html)
- [Tween](https://docs.godotengine.org/en/stable/classes/class_tween.html)
- [Pause](https://docs.godotengine.org/en/stable/tutorials/scripting/pausing_games.html)
- [Loading](https://docs.godotengine.org/en/stable/tutorials/io/background_loading.html)
- [Threads](https://docs.godotengine.org/en/stable/tutorials/performance/thread_safe_apis.html)
- [Saves](https://docs.godotengine.org/en/stable/tutorials/io/saving_games.html)
- [Editor tools](https://docs.godotengine.org/en/stable/tutorials/plugins/running_code_in_the_editor.html)
- [Networking](https://docs.godotengine.org/en/stable/tutorials/networking/high_level_multiplayer.html)
