---
name: cocos-conventions
description: Cocos Creator 3.x real-world coding conventions — when to use what. Covers static vs dynamic assignment, node references, MVC in practice, constants centralization, debugging discipline.
paths: "**/*.ts"
---

# Cocos 3.x 实战约定

## 硬编码 → 单一真相源

数值、路径、枚举散落各文件是第一大烂代码。`Constants.ts` / `Paths.ts` / `Enums.ts` 集中定义，改一处全项目生效。不同于 prefab 上的属性（那是"这个节点的默认值"），常量文件定义的是"游戏规则层面的值"。

## Interface 中心化

`types/` 目录按模块定义 interface，全项目共用。组件间传数据用 interface 而非 `any`——Intellisense 可用，重构改名自动同步。

## MVC 在 Cocos 的实际形态

不搞三层。实际：**Manager 改数据发事件 → Component 监听事件刷 UI**。数据流单向，UI 不直接改数据，Manager 不直接操作节点。

## 静态赋值 vs 动态赋值

判断线：**换张美术图这个值还得改吗？** 要 → 编辑器设（策划自己调）；不要 → 可能代码算。值随设计稿变 → 静态，值随用户数据变 → 动态。

## 节点引用策略

1. `@property(Node)` 拖拽赋值 — **首选**，零开销，重构安全
2. `findChildByName()` — 动态生成的模板子节点
3. `find()` — **只在** Canvas/MainCamera 这种永不变的路径用。生产代码长路径 find = 坏味

## 找 bug 纪律

git diff 确认变更范围 → 二分法缩小 → 数据流逐段 log（输入/处理/输出）→ **先证明因果再修**。别看见旁边不对劲就顺手改。

## 一次只修一个问题

修 A 时看到 B 写得烂 → 忍住，记下来，commit A 后再修。混着改回头 git bisect 定位不了，review 也看不懂。
