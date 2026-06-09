---
name: cocos-lifecycle
description: Cocos Creator 3.x component lifecycle non-obvious behaviors. Use when writing Cocos components, debugging initialization order issues, or working with scene/prefab lifecycle.
paths: "**/*.ts"
---

# Cocos 3.x 生命周期非直觉行为

## onLoad 不保证顺序

同节点其他组件的 `onLoad` 不一定已执行。一个组件的 `onLoad` 里 `getComponent(X)` 可能拿到 X 实例，但 `X.onLoad` 还没跑。跨组件初始化放 `start`。

## onEnable 不等 start

Prefab 实例化时 `onEnable` 立即触发，不走 `start`。如果 `onEnable` 依赖了 `start` 中初始化的 Manager，会拿不到。

## destroy vs removeFromParent

- `node.destroy()` — 触发 `onDestroy`，递归销毁子节点。场景切换时用这个
- `node.removeFromParent()` — 只从树移除，节点和组件还在内存。**绝对不要**用来做"暂时不用"，那是 `active=false` 的事

## 场景切换：replace vs additive

- `director.loadScene`（replace）— 销毁当前场景**所有**节点。跨场景数据只能放独立于场景的 Manager 单例
- `director.loadScene` 是异步的，新场景 `onLoad` 在老场景 `onDestroy` **之前**执行——两边生命周期交叠，做过渡动画时注意

## schedule 不自动取消

`scheduleOnce` / `schedule` 在 `onDestroy` 时**不自动取消**。组件销毁后回调触发，`this` 指向垃圾。`onDestroy` 里必须 `this.unscheduleAllCallbacks()`
