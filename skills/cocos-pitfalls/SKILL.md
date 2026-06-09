---
name: cocos-pitfalls
description: Cocos Creator 3.x platform-specific hard pitfalls. Use when building for native platforms (iOS/Android), WeChat Mini Game, or debugging platform-specific issues.
paths: "**/*.ts"
---

# Cocos 3.x 平台硬坑

## 纹理压缩：两个都勾

iOS 用 ASTC，Android 用 ETC2。Cocos 构建面板**两个都勾**——只勾一个，另一平台软解，内存翻 4-6 倍。

## Android TTF 字体不渲染

部分 Android 系统字体 fallback 链断裂导致 TTF 完全不渲染。项目自带 fallback 字体文件。

## iOS JSC ≠ Android V8

原生平台 JS 引擎不同：iOS 用 JSC（JIT 被苹果禁用），Android 用 V8（JIT 开启）。同样代码浏览器流畅、iOS 卡顿，常是这个原因。JSC GC 更激进，临时对象分配在 iOS 上更敏感。

## 微信小游戏资源管辖

`wx.downloadFile` 下载的资源不在 Cocos `assetManager` 管辖内，不自动管理。用 `assetManager.loadRemote` 或手动转 Cocos 资源。

## sys.localStorage 10MB 上限

微信小游戏 `sys.localStorage` 底层是 `wx.setStorageSync`，10MB 上限，超了静默失败。
