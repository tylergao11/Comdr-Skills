---
name: cocos-creator-3x-judgment
description: Cocos Creator 3.x domain judgment for TypeScript code, lifecycle, resources, prefab/scene boundaries, UI layout, bundles, Comdr/editor-vs-code decisions, and Cocos-specific code review. Use when modifying or reviewing Cocos TS, debugging initialization/order/resource/UI issues, deciding whether work belongs in code or editor artifacts, or preparing Cocos/Web/WeChat/native delivery checks.
---

# Cocos Creator 3.x Judgment

Use this skill to add Cocos-specific engineering judgment before changing code or judging a bug. Prefer existing project patterns over generic architecture.

## First Pass

1. Classify the target: code logic, editor artifact, prefab/scene structure, resource ownership, UI layout, protocol/data flow, or platform runtime.
2. Read the smallest relevant project files first; do not infer Cocos behavior from generic TypeScript alone.
3. If the change affects prefab serialized references, bundles, resources, scene lifecycle, build output, or device behavior, treat it as a Cocos boundary problem, not just a code problem.
4. Keep fixes scoped to the feature owner. Touch global framework code only when the root cause is proven there.

## Routing

- For lifecycle, UI, asset, bundle, and node-reference judgment, read `references/lifecycle-ui-assets.md`.
- For platform and review checks, read `references/platform-review-checklist.md`.
- For editor-vs-code decisions, use the Comdr boundary in `references/lifecycle-ui-assets.md`.
- If a more specific local skill exists, combine this skill with it instead of duplicating its work.

## Default Review Lens

Check these before approving a Cocos change:

- Lifecycle order: `onLoad`, `onEnable`, `start`, scene switching, delayed callbacks, and event cleanup.
- Node ownership: serialized `@property` references, dynamic children, long-path `find`, prefab UUID risks.
- Resource ownership: dynamic loads, bundle boundaries, release path, stale cache/build output.
- UI behavior: Canvas fit mode, Widget stretch, Layout resize mode, render order, draw-call churn.
- Data flow: manager/cache updates data, component refreshes view, UI does not silently mutate source state.
- Platform: WeChat mini-game/native/browser differences, storage limits, texture/font/runtime differences.

## Output

When this skill meaningfully changes the answer, report:

- The Cocos-specific risk found.
- The file or prefab boundary involved.
- The test or inspection needed to verify it.
