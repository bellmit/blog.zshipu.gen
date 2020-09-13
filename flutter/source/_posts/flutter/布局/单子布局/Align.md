---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Align
author: 知识铺
weight: -1
---

# Align

```dart
const Align({
  Key key,
  this.alignment: Alignment.center, // 对齐方式，默认居中对齐
  this.widthFactor, // 宽度因子，不设置的情况，会尽可能大
  this.heightFactor, // 高度因子，不设置的情况，会尽可能大
  Widget child // 要布局的子Widget
})
```

`widthFactor`和`heightFactor`作用：

- 因为子组件在父组件中的对齐方式必须有一个前提，就是父组件得知道自己的范围（宽度和高度）；
- 如果`widthFactor`和`heightFactor`不设置，那么默认Align会尽可能的大（尽可能占据自己所在的父组件）；
- 我们也可以对他们进行设置，比如widthFactor设置为3，那么相对于Align的宽度是子组件跨度的3倍

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
    return Align(
      child: Icon(Icons.pets, size: 36, color: Colors.red,), // 如果只有这一句, 那么图标会在屏幕中间显示
      alignment: Alignment.bottomRight, // 如果没有后面代码, 此icon显示在屏幕右下角
      widthFactor: 2, // 宽度占2位icon大小, 由于对齐方式为bottomRight, 即左边留一个icon宽的空白
      heightFactor: 3, // 高度占3倍icon大小, 由于对齐方式为bottomRight, 即上边留2个icon高的空白
    );
  }
}
```