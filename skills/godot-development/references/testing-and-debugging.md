# Testing and debugging

## Validate in layers
Use the project's configured executable. Confirm flags in `--help`; examples assume compatible Godot 4 editor support:

```bash
godot --version
godot --headless --path /absolute/project --import
godot --headless --path /absolute/project --script res://path/changed.gd --check-only
godot --headless --path /absolute/project --quit-after 120
```

Import checks editor/resources; script checking parses; bounded startup smoke-checks. Startup can miss lazy scenes/async work. Inspect logs as well as status. Import global classes before diagnosing dependency errors. Never claim one script check validates the project.

Use existing tests. Add meaningful checks for changed behavior, domain invariants and lifecycle defects, not implementation mirrors. Keep logic independent of the engine where that genuinely helps.

Test applicable first/repeated instances, reload, pause, removal/reentry, scene changes, cancellation and shared-resource mutation. Control random seeds and timing for reproducible domain checks.

Use editor/device checks for visuals, focus, input devices, audio, shaders and rendering. Headless cannot validate these alone. Check relevant exported builds for assets, filesystem casing, renderer/platform changes.

If no Godot binary/device is available, perform static review and specify remaining runtime checks. Do not claim execution or install arbitrary tools merely for a green check.

## Debug and profile
Reproduce minimally, read the first meaningful error/stack, inspect remote tree, exports, signals and resource identity, then verify fixes at the original integration point.

Measure representative workloads before optimization. Record platform/hardware/renderer and metrics; distinguish CPU/GPU/I/O/memory. Compare before/after. Use cached references, fewer callbacks, batching or threading only where evidence justifies them. Avoid speculative pooling.

## Preserve integrity
Track source scenes/resources/config and persistent identity metadata. Exclude regenerable caches according to the actual version's VCS guide. Do not blanket-ignore .uid or import metadata without checking their role. Preserve casing and references during moves; avoid unrelated global Git settings/reformatting.

Verify export presets/templates/target requirements. Keep credentials out of changes. Report executed checks and material remaining checks accurately.

Official references:
- [CLI](https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html)
- [Optimization](https://docs.godotengine.org/en/stable/tutorials/performance/general_optimization.html)
- [Organization](https://docs.godotengine.org/en/stable/tutorials/best_practices/project_organization.html)
- [VCS](https://docs.godotengine.org/en/stable/tutorials/best_practices/version_control_systems.html)
- [Export](https://docs.godotengine.org/en/stable/tutorials/export/exporting_projects.html)
