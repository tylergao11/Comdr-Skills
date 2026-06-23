# qzxz Migration Audit Points

## Protocol

- Lua uses old byte stream reader/writer/processer files.
- TS qzxz uses PB encode/decode and command bindings. Check `FXJCmd.ts`, `FXJWriteAndRead.ts`, and `FXJPBAdaptive.ts` together.
- Do not copy Lua read/write offsets into TS unless the current server command still uses the same binary payload.
- Audit duplicate or suspicious command bindings before blaming state/UI. Known inspection point: `USER_HUAN_SAN_ZHANG_RESULT` appears in both C2S command constants and repeated PB binding areas in `FXJCmd.ts`; verify intent before changing.

## Rule Constants

- Lua `zgqzxzConfig.lua` currently shows:
  - `playerNumer = 6`
  - `HAND_CARD_NUM = 7`
  - `totalMahjongNum = 72`
- TS `common/GameRuleConfig.ts` currently shows:
  - `CardTotalNum: 72`
  - `playerNum: 4`
- Treat the player-count difference as an audit question, not an automatic bug. Confirm whether TS qzxz intentionally limits active seats through framework/UI constraints.

## State And UI

- Reconnect bugs usually cross protocol parse, `Room.ts`, `RoomMgr.ts`, player/operation caches, and UI component refresh.
- Seat mapping depends heavily on `GameRuleConfig.playerNum`; inspect all local-seat conversions before changing only one view.
- qzxz components often use `QZXZGameComponent` as an indirection layer. Follow `doGameCompFun` or component delegation before concluding a method is unused.

## Resources And Encoding

- qzxz resources are registered through subgame bundle paths such as `SubGameConfig.SubGamePackage.SUBGAME_QZXZ_REMOTE`.
- Check both `FXJRes.ts` and actual asset paths before changing resource names.
- Many migrated comments/string literals may display as mojibake in PowerShell or source files. Before editing Chinese text, confirm encoding and avoid PowerShell text pipelines for non-ASCII content.

## Base Escalation Rule

Escalate from qzxz to `assets/package/base` only when:

- The qzxz packet/cmd/PB binding is correct but global dispatch loses or corrupts data.
- Multiple subgames are affected by the same base behavior.
- The shared controller/socket/buffer contract is violated and the evidence is in base file/line references.
