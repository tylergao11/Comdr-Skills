---
name: cocos-ui
description: Cocos Creator 3.x UI adaptation system mental model. Use when designing UI layout, responsive adaptation, or debugging layout/sorting issues.
paths: "**/*.ts"
---

# Cocos 3.x UI 适配思路模型

## 两层适配模型

1. **Canvas**（fitHeight/fitWidth）— 决定画布缩放
2. **Widget** — 决定节点在缩放后画布上的定位

横屏游戏用 fitHeight（宽度自适应），竖屏用 fitWidth。两者解决的问题不同，可以叠加。

## Widget 双开对齐 = 拉伸

`isAlignTop` + `isAlignBottom` 同时开 → 节点被**竖向拉伸**填满父节点高度。不是居中，是拉伸。容易出意外。

## Layout resizeMode

- NONE — 不改自身尺寸（默认，大部分 bug 源于忘了改）
- CHILDREN — 根据子节点调整自身
- CONTAINER — 根据自身调整子节点

## 渲染排序与合批

同 Canvas 下，Hierarchy 越靠下 → 渲染越靠前。不同图集节点之间**打断合批**（+drawcall）。Canvas 下放不透明全屏背景可截断排序、省 drawcall。

## 设计分辨率 ≠ 实际分辨率

Canvas design resolution 只是坐标参考系。750×1334 设计下 Widget top=10 对应物理屏 5-15px（取决于设备密度）。
