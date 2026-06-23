---
name: qzxz-migration-boundary
description: qzxz subgame migration guardrail for the WXGame_MJLandscape project. Use before changing or reviewing Lua-to-TypeScript qzxz code, qzxz protocol/PB bindings, qzxz room/cache/UI behavior, qzxz resources, or any suspected boundary between assets/package/subGames/qzxz and assets/package/base.
---

# qzxz Migration Boundary

Use this skill before changing qzxz. It protects the main-game/subgame boundary and keeps Lua-to-TS migration work tied to evidence.

## Project Boundary

- qzxz is a subgame. Default edit scope: `assets/package/subGames/qzxz/`.
- Main/base framework lives under `assets/package/base/`. Change it only after proving the root cause is global.
- Lua 七张血战 source is under `D:\UserProfiles\Tylergao\Desktop\zgqzxz_develop\scripts\`.
- TS qzxz source is under `d:\WXGame_MJLandscape\assets\package\subGames\qzxz\`.

## Workflow

1. Identify the bug surface: protocol/PB, room/cache state, UI/prefab component, rule config, resource path, or base framework.
2. Read the TS file and its Lua predecessor before changing migrated behavior.
3. Do not assume Lua wire format maps one-to-one to TS; this project uses PB binding in TS.
4. Prefer qzxz-local fixes. Escalate to base only with a file/line trail showing the shared layer is wrong.
5. After edits, do an independent test pass and then an audit pass for main-game impact, protocol bindings, and qzxz resource boundaries.

## Routing

- For qzxz file map and owner boundaries, read `references/project-map.md`.
- For migration hazards and known audit points, read `references/migration-audit.md`.
- For Cocos lifecycle/resources/UI risks, also use `cocos-creator-3x-judgment` when available.

## Output

When using this skill, include:

- Whether the fix stayed inside qzxz or touched base.
- The Lua-to-TS evidence used.
- The protocol/resource/state risk checked.
- What was tested and what still requires Cocos/editor/device verification.
