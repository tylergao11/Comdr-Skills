---
name: comdr-workflow
description: Comdr vs Coding boundary. Use when deciding whether a task should go to comdr-ask (editor operations) or be written as TypeScript directly.
paths: "**/*.ts"
---

# Comdr 与 Coding 协作

## 判断线

操作目标是**编辑器产物**（prefab/scene/组件属性）→ `comdr-ask` MCP tool。操作目标是**代码逻辑**（脚本/算法/数据流）→ 直接写 TypeScript。

## 典型链路

"做一个排行榜面板" →
1. 节点层级、UI 组件挂载 → comdr-ask
2. 数据获取、排序、刷新逻辑 → Coding
3. 视觉细节（spriteFrame 引用、字体大小）→ comdr-ask

## 常见误判

"改一下按钮颜色" → 看起来是代码的事，实际涉及找到按钮节点 → Sprite 组件 → color 属性。这是 Comdr 的活。
