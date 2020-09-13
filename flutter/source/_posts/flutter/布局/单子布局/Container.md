---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Container
author: 知识铺
weight: -1
---

# Container

Container组件类似于其他Android中的View，iOS中的UIView。

如果你需要一个视图，有一个背景颜色、图像、有固定的尺寸、需要一个边框、圆角等效果，那么就可以使用Container组件, Container在开发中被使用的频率是非常高的，特别是我们经常会将其作为容器组件  

```dart
Container({
  this.alignment,
  this.padding, //容器内补白，属于decoration的装饰范围
  Color color, // 背景色
  Decoration decoration, // 背景装饰
  Decoration foregroundDecoration, //前景装饰
  double width,//容器的宽度
  double height, //容器的高度
  BoxConstraints constraints, //容器大小的限制条件
  this.margin,//容器外补白，不属于decoration的装饰范围
  this.transform, //变换
  this.child,
})
```

注:   
- 容器的大小可以通过width、height属性来指定，也可以通过constraints来指定，如果同时存在时，width、height优先。实际上Container内部会根据width、height来生成一个constraints；
- color和decoration是互斥的，实际上，当指定color时，Container内会自动创建一个decoration

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
    return Center(
        child: Container(
          width: 100,
          height: 100,
          color: Color.fromRGBO(3, 3, 255, .5),
          child: Icon(
            Icons.pets,
            size: 32,
            color: Colors.white,
          ),
        )
    );
  }
}
```

### BoxDecoration

Container有一个非常重要的属性 decoration：

他对应的类型是Decoration类型，但是它是一个抽象类。
在开发中，我们经常使用它的实现类BoxDecoration来进行实例化

```dart
const BoxDecoration({
  this.color, // 颜色，会和Container中的color属性冲突
  this.image, // 背景图片
  this.border, // 边框，对应类型是Border类型，里面每一个边框使用BorderSide
  this.borderRadius, // 圆角效果
  this.boxShadow, // 阴影效果
  this.gradient, // 渐变效果
  this.backgroundBlendMode, // 背景混合
  this.shape = BoxShape.rectangle, // 形变
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
    return Center(
      child: Container(
        width: 150,
        height: 150,
        child: Icon(Icons.pets, size: 32, color: Colors.red,),
        decoration: BoxDecoration(
          color: Colors.amber,
          border: Border.all( // 边框
            color: Colors.redAccent,
            width: 3,
            style: BorderStyle.solid,
          ),
          borderRadius: BorderRadius.circular(20),
          boxShadow: [
            BoxShadow( // 阴影
              offset: Offset(5, 5),
              color: Colors.purple,
              blurRadius: 5, // 阴影模糊化
            )
          ],
          gradient: LinearGradient( // 渐变
            colors: [
              Colors.green,
              Colors.red,
            ],
          )
        ),
      ),
    );
  }
}
```