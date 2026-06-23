# Lifecycle, UI, Assets, And Comdr Boundary

## Lifecycle

- Use `onLoad` for local component setup only. Do not assume other components on the same node have completed their own `onLoad`.
- Use `start` or an explicit initialization method for cross-component dependencies.
- Treat `onEnable` as earlier than many developers expect; it can run before `start`-initialized state is ready.
- Prefer explicit cleanup for event listeners, timers, scheduled callbacks, tweens, and async callbacks that capture component state.
- Scene switches can overlap old-scene teardown and new-scene setup. Audit singleton/cache state when a scene transition bug appears.

## Node References

- Prefer serialized `@property(Node)` or typed component references for stable prefab nodes.
- Use child lookup only for dynamic/template children whose structure is owned locally.
- Treat long global `find()` paths as fragile unless the path is a stable root such as Canvas or MainCamera.
- Remember that prefab component/script references are serialized by UUID. Moving or replacing scripts can break references without an obvious TypeScript error.

## UI Judgment

- Canvas fit mode controls coordinate scaling; Widget controls positioning after scaling. Do not treat them as the same layer.
- Double-sided Widget alignment stretches the node along that axis; it is not centering.
- Layout `resizeMode` determines whether the container sizes itself or sizes children. Wrong mode often looks like a data/render bug.
- Hierarchy order affects render order under the same Canvas. Mixed atlases and interleaved nodes can increase draw calls.
- Do not fix UI layout by adding magic offsets until Canvas, Widget, Layout, and parent transforms are inspected.

## Asset And Bundle Judgment

- Dynamic loads are not automatically safe just because a scene changes. Identify the owner responsible for release or cache retention.
- Bundle boundaries should follow feature/runtime loading boundaries: first package size, memory pressure, hot update granularity, and cross-bundle dependencies.
- Auto Atlas is a build-time packing strategy for related sprites; it is not a runtime loading mechanism.
- Shared art that crosses many panels may belong in an explicit shared atlas or shared bundle instead of a panel-local auto atlas.
- If a resource appears stale after rebuild, inspect generated build output and Cocos/WeChat caches before rewriting logic.

## Comdr Boundary

- Editor artifacts belong to Comdr/editor operations: prefab hierarchy, scene nodes, component properties, sprite frames, fonts, colors, anchors, Widget/Layout settings.
- Code logic belongs to TypeScript: algorithms, data flow, protocol processing, cache updates, event dispatch, state machines.
- Mixed tasks need a split plan. Example: a ranking panel needs editor work for nodes/components and TypeScript work for sorting/refresh logic.
