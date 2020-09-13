---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： TextField
author: 知识铺
weight: -1
---

# TextField

```dart
const TextField({
  Key key,
  this.controller,
  this.focusNode,
  this.decoration = const InputDecoration(),
  TextInputType keyboardType,
  this.textInputAction,
  this.textCapitalization = TextCapitalization.none,
  this.style,
  this.strutStyle,
  this.textAlign = TextAlign.start,
  this.textAlignVertical,
  this.textDirection,
  this.readOnly = false,
  ToolbarOptions toolbarOptions,
  this.showCursor,
  this.autofocus = false,
  this.obscureText = false,
  this.autocorrect = true,
  this.maxLines = 1,
  this.minLines,
  this.expands = false,
  this.maxLength,
  this.maxLengthEnforced = true,
  this.onChanged,
  this.onEditingComplete,
  this.onSubmitted,
  this.inputFormatters,
  this.enabled,
  this.cursorWidth = 2.0,
  this.cursorRadius,
  this.cursorColor,
  this.keyboardAppearance,
  this.scrollPadding = const EdgeInsets.all(20.0),
  this.dragStartBehavior = DragStartBehavior.start,
  this.enableInteractiveSelection = true,
  this.onTap,
  this.buildCounter,
  this.scrollController,
  this.scrollPhysics,
}) 
```

decoration：用于设置输入框相关的样式

- icon：设置左边显示的图标
- labelText：在输入框上面显示一个提示的文本
- hintText：显示提示的占位文字
- border：输入框的边框，默认底部有一个边框，可以通过InputBorder.none删除掉
- filled：是否填充输入框，默认为false
- fillColor：输入框填充的颜色

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
    return Container(
      padding: EdgeInsets.all(20),
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          TextFieldDemo()
        ],
      ),
    );
  }
}

class TextFieldDemo extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _TextFieldDemoState();
}

class _TextFieldDemoState extends State<TextFieldDemo> {
  @override
  Widget build(BuildContext context) {
    return TextField(
      decoration: InputDecoration(
        icon: Icon(Icons.people),
        // labelText: "username",
        hintText: "请输入用户名",
        border: InputBorder.none,
        filled: true, // 颜色是否填充
        fillColor: Colors.lightGreen
      ),
      onChanged: (value) {
        print("onChanged: $value");
      },
      onSubmitted: (value) {
        print("onSubmitted: $value");
      },
    );
  }
}
```

### TextField的controller 

可以给TextField添加一个控制器（Controller），可以使用它设置文本的初始值，也可以使用它来监听文本的改变；
事实上，如果我们没有为TextField提供一个Controller，那么会Flutter会默认创建一个TextEditingController的，这个结论可以通过阅读源码得到：

```dart
@override
void initState() {
  super.initState();
  // ...其他代码
  if (widget.controller == null)
    _controller = TextEditingController();
}
```

```dart
class TextFieldDemo extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _TextFieldDemoState();
}

class _TextFieldDemoState extends State<TextFieldDemo> {
  final textEditingController = TextEditingController();

  @override
  void initState() {
    super.initState();
    // 设置默认值
    textEditingController.text = "Hello world";

    // 监听文本框
    textEditingController.addListener(() {
      print("--- textEditingController: ${textEditingController.text}");
    });
  }

  @override
  Widget build(BuildContext context) {
    return TextField(
      controller: textEditingController,
      decoration: InputDecoration(
        icon: Icon(Icons.people),
        // labelText: "username",
        hintText: "请输入用户名",
        border: InputBorder.none,
        filled: true, // 颜色是否填充
        fillColor: Colors.lightGreen
      ),
      onChanged: (value) {
        print("onChanged: $value");
      },
      onSubmitted: (value) {
        print("onSubmitted: $value");
      },
    );
  }
}
```

