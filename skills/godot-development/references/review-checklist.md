# Review checklist

Select relevant checks. Prioritize crashes/data loss/incorrect behavior, then architecture/performance, then readability. Give location, evidence, consequence and correction. Distinguish proven defects, conditional risks and style suggestions.

## Integration
- Verify API/syntax and inherited contracts in the project version.
- Check actual node types, exported assignments, Input Map, resources/config.
- Preserve existing behavior and unrelated work.
- Match addon/export/renderer requirements.

## Code
- Type important contracts without concealing unchecked Variant inputs.
- Handle casts, external data and error returns.
- Keep responsibilities clear and avoid duplicated rules.
- Investigate warnings; justify narrow suppressions.
- Document units, contracts and non-obvious decisions.

## Lifetime
- Keep scenes independent of unknown ancestors/siblings.
- Supply dependencies before use; diagnose missing required setup.
- Check unique-name configuration/scope.
- Distinguish parent/owner and removal/freeing.
- Check pooling/reconnection and duplicate signal handling.
- Handle deferred/awaited work under cancellation, scene change and stale references.

## Systems/data
- Separate definitions from per-instance state.
- Verify nested resource isolation and custom changed notifications.
- Check delta, units, local/global space and collision configuration.
- Check gameplay input after UI, including polling.
- Define timer/tween pause/lifetime.
- Avoid unsafe tree access from threads.
- Validate saves/network inputs and relevant write integrity.

## Evidence
- Exercise behavior, not only syntax.
- Check required visual/device/export behavior.
- Measure performance claims.
- Report performed versus proposed checks accurately.
