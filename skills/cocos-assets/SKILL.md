---
name: cocos-assets
description: Cocos Creator 3.x asset system design constraints. Use when loading assets, designing bundle strategy, working with atlases, or debugging memory issues.
paths: "**/*.ts"
---

# Cocos 3.x 资源系统设计约束

## resources.load 引用计数陷阱

`resources.load` 的资源**不自动释放**。加载 10 次同一个 prefab → 内存里 10 份，需对应 10 次 `assetManager.releaseAsset`。场景切换不清理 resources 加载的资源。

## Bundle 拆分依据

Bundle = 构建时物理隔离 + 运行时独立加载单元。

**拆**：首包体积限制（微信小游戏 4MB）、按需加载（省内存）、热更新粒度
**不拆**：跨 bundle 引用产生依赖链，加载一个强制加载另一个

## 自动图集 vs 手动图集

- 自动图集（Auto Atlas）：同目录散图**构建时**合成大图，非运行时。同一面板的图放一个目录开自动图集
- 手动图集：跨多个面板复用的通用图（按钮背景等），不参与自动图集，单独管理

## SpriteFrame 与 Texture2D 依赖链

一个 Texture2D 上可有多个 SpriteFrame。释放 Texture2D → **连锁释放**所有关联 SpriteFrame。注意反向依赖。

## Prefab 里脚本引用走 UUID

Prefab 里的脚本引用不是文件路径，是 UUID。脚本重命名/移动后 prefab 中组件引用**静默断裂**——编辑器不报错，运行时 `getComponent` 拿 null。
