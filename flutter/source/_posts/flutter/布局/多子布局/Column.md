---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Column
author: 知识铺
weight: -1
---

# Column

Column和Row字段一致

```dart
Column({
	Key key,
	MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
	MainAxisSize mainAxisSize = MainAxisSize.max,
	CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
	TextDirection textDirection,
	VerticalDirection verticalDirection = VerticalDirection.down,
	TextBaseline textBaseline,
	List<Widget> children = const <Widget>[],
})
```

```dart
ltr 的方向是: [start]---------->[end] 那么如果对齐方式是start, 就是左对齐; 如果对齐方式是end, 右对齐
rtl 的方向是: [end]<----------[start] 那么如果对齐方式是start, 就是右对齐; 如果对齐方式是end, 左对齐
```

```dart
down的方向是:
[start]
  |
  |
  |
  |
  |
 \|/
[end] 

如果对齐方式是start, 就是顶部对齐;
如果对齐方式是end, 就是底部对齐;

up的方向是: 

[end]
 /|\
  |
  |
  |
  |
  |
[start] 

如果对齐方式是start, 就是底部对齐;
如果对齐方式是end, 就是顶部对齐;
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
    return Column(
      mainAxisSize: MainAxisSize.max, // 占整列

      // 竖直方向 纵轴
      verticalDirection: VerticalDirection.up,
      mainAxisAlignment: MainAxisAlignment.start,

      // 水平方向 横轴
      textDirection: TextDirection.rtl,
      crossAxisAlignment: CrossAxisAlignment.start,

      children: <Widget>[
        Container(color: Colors.red, width: 60, height: 60),
        Container(color: Colors.blue, width: 80, height: 80),
        Container(color: Colors.green, width: 70, height: 70),
        Container(color: Colors.orange, width: 100, height: 100),
      ],
    );
  }
}
```

