# qzxz Project Map

## Roots

- Project root: `d:\WXGame_MJLandscape`
- TS qzxz subgame: `assets/package/subGames/qzxz/`
- Main/base framework: `assets/package/base/`
- Lua source: `D:\UserProfiles\Tylergao\Desktop\zgqzxz_develop\scripts\`

## TS qzxz Files

- `common/FXJController.ts`: qzxz controller; room/game message integration.
- `net/FXJCmd.ts`: qzxz C2S/S2C command constants and PB binding table.
- `net/FXJWriteAndRead.ts`: qzxz packet encode/decode and PB registration.
- `net/FXJPBAdaptive.ts`: PB package paths, including qzxz Common/Game proto packages.
- `cache/Room.ts`: desk/game state aggregation and reconnect/game message handling.
- `cache/RoomMgr.ts`: room and rule-state cache.
- `cache/PlayerMgr.ts`, `cache/OperationMgr.ts`, `cache/SettleMgr.ts`: player, operation, and settle state.
- `common/GameRuleConfig.ts`: qzxz rule defaults and resource/sound overrides.
- `component/GameComponent.ts`, `component/GameBaseComponent.ts`: qzxz game component hook layer.
- `common/FXJRes.ts`, `common/FXJSound.ts`: qzxz resource and sound path definitions.

## Main/Base Files To Treat As Shared

- `assets/package/base/proj/GlobalController.ts`: global network send/PB/cmd mapping dispatch.
- `assets/package/base/framework/network/WebSocketBuffer.ts`: packet buffer helpers.
- `assets/package/base/proj/controllers/RoomController.ts`: generic room controller parent.

## Lua Source Counterparts

- `socket/mjgamecmd.lua`: old command constants.
- `socket/mjgamewriter.lua`: old C2S byte writers.
- `socket/mjgamereader.lua`: old S2C byte readers.
- `socket/mjgameprocesser.lua`: old message processing and state hooks.
- `room/mjgameroomcontroller.lua`: old room controller behavior.
- `data/mjgamecarddata.lua`: old card/game data behavior.
- `data/mjgameoverdataparse.lua`: old settle parsing.
- `zgqzxzConfig.lua`: old rule constants.
