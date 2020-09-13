---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： 入门Flutter
author: 知识铺
weight: -1
---

# 入门Flutter

Flutter利用Skia绘图引擎，直接通过CPU、GPU进行绘制，不需要依赖任何原生的控件  

- `GPU`将信号同步到 `UI 线程`
- `UI 线程`用`Dart`来构建`图层树`
- `图层树`在`GPU 线程`进行合成
- 合成后的`视图数据`提供给`Skia 引擎`
- `Skia 引擎`通过`OpenGL 或者 Vulkan`将显示内容提供给`GPU`

Skia 已然是 Android 官方的图像渲染引擎了，因此 Flutter Android SDK 无需内嵌 Skia 引擎就可以获得天然的 Skia 支持；

而对于 iOS 平台来说，由于 Skia 是跨平台的，因此它作为 Flutter iOS 渲染引擎被嵌入到 Flutter 的 iOS SDK 中，替代了 iOS 闭源的 Core Graphics/Core Animation/Core Text，这也正是 Flutter iOS SDK 打包的 App 包体积比 Android 要大一些的原因

开发模式切换

https://www.jianshu.com/p/242e61db8d4f

https://www.jianshu.com/p/591cc23f03b0