# Platform And Review Checklist

## Platform Risks

- Browser preview, Cocos editor, WeChat mini-game, and native builds can differ. Verify on the target surface when the bug is runtime-specific.
- WeChat mini-game storage and file APIs have platform limits; do not assume browser localStorage or desktop file behavior.
- WeChat-downloaded files may not be managed like Cocos assets unless loaded through the Cocos asset pipeline or explicitly wrapped.
- Native iOS and Android use different JS runtimes and graphics/font paths. Performance and font behavior can diverge even when TypeScript is identical.
- Texture compression settings must match the target platform. Missing compression can become a memory problem, not just an image-quality issue.

## Code Review Checklist

- Lifecycle: cross-component initialization in `start` or explicit init, cleanup in destroy paths, async callbacks guarded.
- Events: every listener has a clear owner and matching removal.
- Resources: dynamic loads have owner, cache policy, and release policy.
- Performance: no avoidable allocations, heavy lookup, or layout rebuilds in per-frame paths.
- UI: no long-path `find` for stable nodes; no magic offsets hiding Canvas/Widget/Layout problems.
- Architecture: managers/caches own data; components own nodes; UI actions call controllers/managers instead of mutating shared data directly.
- Constants: game rules, command IDs, resource paths, and magic numbers are centralized where the local project already expects them.
