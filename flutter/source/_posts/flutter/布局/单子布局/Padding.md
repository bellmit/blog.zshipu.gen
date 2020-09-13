---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Padding
author: 知识铺
weight: -1
---

# Padding

Padding在Flutter中是一个Widget，但是Flutter中没有Margin这样一个Widget，这是因为外边距也可以通过Padding来完成。
Padding通常用于设置子Widget到父Widget的边距（你可以称之为是父组件的内边距或子Widget的外边距）

源码:  
```dart
const Padding({
  Key key,
  @required this.padding, // EdgeInsetsGeometry类型（抽象类），使用EdgeInsets
  Widget child,
})
```

```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

main(List<String> args) {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text("Hello World"),
        ),
        body: HomeBody(),
      ),
    );
  }
}

class HomeBody extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: EdgeInsets.all(20),
      child: Text(
        "千山鸟飞绝, 万境人踪灭\n"
        "孤舟蓑笠翁, 独钓寒江雪",
        style: TextStyle(color: Colors.redAccent),
      ),
    );
  }
}
```