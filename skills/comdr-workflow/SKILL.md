---
name: comdr-workflow
description: Comdr vs Coding boundary. Use when deciding whether a task should go to comdr-write (editor operations) or be written as TypeScript directly.
paths: "**/*.ts"
---

# Comdr 与 Coding 协作

## 判断线

操作目标是**编辑器产物**（prefab/scene/组件属性）→ `comdr-write`。操作目标是**代码逻辑**（脚本/算法/数据流）→ 直接写 TypeScript。

## 分工规则

- 编辑器产物包括节点层级、组件挂载、组件属性、prefab/scene 序列化结构、资源引用、UI 布局。
- 代码逻辑包括算法、状态管理、协议处理、事件流、数据获取、业务规则、TypeScript 源码。
- 一个任务跨两边时，按产物边界拆分：先确认需要的编辑器槽位，再做对应的 editor write；代码逻辑仍由 Codex 直接改源码。
- 进入 `comdr-write` 时描述自然语言写入意图和已确认槽位，不写 DSL，不编造 handle，不把节点名当 handle。

## 误判规则

- 如果目标是改变编辑器里已有节点、组件或资源引用，优先走 `comdr-write`。
- 如果目标是改变运行时行为但不需要改 prefab/scene 序列化结构，优先直接改 TypeScript。
- 如果无法判断，先用证据查询确认目标属于编辑器产物还是源码逻辑。
