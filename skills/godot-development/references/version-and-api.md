# Version and API verification

Read binary version, project feature flags, CI, export templates, and addon requirements. Treat `config/features` as project requirements, not proof of the running binary. Do not upgrade solely for a convenient new API.

Select official documentation at `https://docs.godotengine.org/en/<major.minor>/...`. Use `stable` for discovery; resolve the actual project version. Treat `latest` as development documentation. If a URL fails, navigate the official documentation/version selector rather than silently substituting another version. Check patch notes for relevant regressions.

For unfamiliar, uncertain, version-sensitive, or pivotal APIs, verify:
1. Owning class and inherited member location.
2. Signature, argument order/types/defaults, and return value.
3. Units, coordinate space, and side effects.
4. Lifecycle stage, thread/process restrictions.
5. Availability, deprecation, and platform/renderer limits.
6. Signals and error semantics where relevant.

Prefer official version-matched references, installed editor help, and minimal experiments. Consult official source/release notes for ambiguity. Community examples can suggest approaches but do not override verified contracts.

Check `--help` before using tooling flags. Where supported, `--doctool` exports engine API XML; generate it outside project source. An API dump supports lookup but does not replace runtime/platform testing.

Verify version-sensitive features such as typed dictionaries, warning annotations, resource duplication and networking rather than claiming universal Godot 4 compatibility. Keep GDScript and C# examples distinct.

If offline, use local help, source, and parser evidence. Identify remaining assumptions; never invent methods, versions, or successful execution.

For migration, inventory formats, renamed classes, physics/input, shaders, addons and exports. Review conversion diffs and test representative scenes; keep unrelated redesign separate.

Official entry points:
- [Classes](https://docs.godotengine.org/en/stable/classes/index.html)
- [CLI](https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html)
- [Archive](https://godotengine.org/download/archive/)
- [Migration](https://docs.godotengine.org/en/stable/tutorials/migrating/index.html)
