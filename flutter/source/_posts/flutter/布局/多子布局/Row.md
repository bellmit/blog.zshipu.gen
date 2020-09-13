---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Row
author: 知识铺
weight: -1
---

# Row

参考: 

- [https://juejin.im/post/5d93306cf265da5b7a753a6b](https://juejin.im/post/5d93306cf265da5b7a753a6b)

```dart
Row({
  Key key,
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, // 主轴对齐方式
  MainAxisSize mainAxisSize = MainAxisSize.max, // 水平方向尽可能大
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, // 交叉处对齐方式
  TextDirection textDirection, // 水平方向子widget的布局顺序（默认为系统当前Locale环境的文本方向(如中文、英语都是从左往右，而阿拉伯语是从右往左））
  VerticalDirection verticalDirection = VerticalDirection.down, // 表示Row纵轴（垂直）的对齐方向
  TextBaseline textBaseline, // 如果上面是baseline对齐方式，那么选择什么模式（有两种可选）
  List<Widget> children = const <Widget>[],
})
```

mainAxisSize：

- 表示Row在主轴(水平)方向占用的空间，默认是`MainAxisSize.max`，表示尽可能多的占用水平方向的空间，此时无论子widgets实际占用多少水平空间，Row的宽度始终等于水平方向的最大宽度
- 而`MainAxisSize.min`表示尽可能少的占用水平空间，当子widgets没有占满水平剩余空间，则Row的实际宽度等于所有子widgets占用的的水平空间；

mainAxisAlignment：表示子Widgets在Row所占用的水平空间内对齐方式

- 如果mainAxisSize值为`MainAxisSize.min`，则此属性无意义，因为子widgets的宽度等于Row的宽度
- 只有当mainAxisSize的值为`MainAxisSize.max`时，此属性才有意义
- `MainAxisAlignment.start`表示沿textDirection的初始方向对齐，
- 如textDirection取值为`TextDirection.ltr`时，则`MainAxisAlignment.start`表示左对齐，textDirection取值为`TextDirection.rtl`时表示从右对齐。
- 而`MainAxisAlignment.end`和`MainAxisAlignment.start`正好相反；
- `MainAxisAlignment.center`表示居中对齐。

crossAxisAlignment：表示子Widgets在纵轴方向的对齐方式

- Row的高度等于子Widgets中最高的子元素高度
- 它的取值和MainAxisAlignment一样(包含`start`、`end`、 `center`三个值)
- 不同的是crossAxisAlignment的参考系是verticalDirection，即verticalDirection值为`VerticalDirection.down`时`crossAxisAlignment.start`指顶部对齐，verticalDirection值为`VerticalDirection.up`时，`crossAxisAlignment.start`指底部对齐；而`crossAxisAlignment.end`和`crossAxisAlignment.start`正好相反

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
    return Row(
      mainAxisSize: MainAxisSize.max, // 占整行
      mainAxisAlignment: MainAxisAlignment.start, // spaceEvenly space均分
      textDirection: TextDirection.ltr,
      verticalDirection: VerticalDirection.up, // up或down, up: 顶部对齐  down: 底部对齐
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

mainAxisAlignment = MainAxisAlignment.start 时
textDirection = TextDirection.ltr: 左对齐, 子控件从左向右依次排列
textDirection = TextDirection.rtl: 右对齐, 子控件从右向左依次排列

mainAxisAlignment = MainAxisAlignment.end 时
textDirection = TextDirection.ltr: 右对齐, 子控件从左向右依次排列
textDirection = TextDirection.rtl: 左对齐, 子控件从右向左依次排列

mainAxisAlignment = MainAxisAlignment.center 时
textDirection = TextDirection.ltr: 居中对齐, 子控件从左向右依次排列
textDirection = TextDirection.rtl: 居中对齐, 子控件从右向左依次排列

ltr 和 rtl 指的是方向  

```
ltr 的方向是: [start]---------->[end] 那么如果对齐方式是start, 就是左对齐; 如果对齐方式是end, 右对齐
rtl 的方向是: [end]<----------[start] 那么如果对齐方式是start, 就是右对齐; 如果对齐方式是end, 左对齐
```

crossAxisAlignment：表示子Widgets在纵轴方向的对齐方式, 它的取值和MainAxisAlignment一样(包含start、end、 center三个值)
crossAxisAlignment = CrossAxisAlignment.start 时:
verticalAlignment = VerticalDirection.down: 顶部对齐
verticalAlignment = VerticalDirection.up: 底部对齐

crossAxisAlignment = CrossAxisAlignment.end 时: 
verticalAlignment = VerticalDirection.down: 底部对齐
verticalAlignment = VerticalDirection.up: 顶部对齐

crossAxisAlignment = CrossAxisAlignment.center 时:
verticalAlignment = VerticalDirection.down: 无意义, 纵轴方向依然居中对齐
verticalAlignment = VerticalDirection.up: 无意义, 纵轴方向依然居中对齐

down 和 up 指的是方向: 

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

#### Expanded  

如果希望红色和黄色的Container Widget不要设置固定的宽度，而是占据剩余的部分，可以使用 Expanded 来包裹 Container Widget，并且将它的宽度不设置值:  

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
    return Row(
      mainAxisSize: MainAxisSize.max, // 占整行
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      textDirection: TextDirection.ltr,
      verticalDirection: VerticalDirection.up, // up或down, up: 顶部对齐  down: 底部对齐
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        Expanded(
          flex: 1,
          child: Container(color: Colors.red, height: 60,),
        ),
        Container(color: Colors.red, width: 60, height: 60),
        Container(color: Colors.blue, width: 80, height: 80),
        Container(color: Colors.green, width: 70, height: 70),
        Container(color: Colors.orange, width: 100, height: 100),
        Expanded(
          flex: 1,
          child: Container(color: Colors.orange, height: 100,),
        ),
      ],
    );
  }
}
```