
title: 从零开始 - 第 1 部分 - 我如何建立我的游戏与 Flutter 在 1 个月
author: 知识铺
date: 2020-09-13 18:59:50
tags: flutter
---
 

 

* * *

## 内容

*   [那么什么是Flutter呢？](#so-what-is-flutter)
    *   [我怎么想的？](#what-do-i-think-of-it)
    *   [开始](#getting-started)
    *   [工具](#tooling)
    *   [Vscode 好东西](#vscode-goodies)
*   [给我看代码！](#show-me-the-code)
    *   [_一_切都是小部件](#everything-is-a-widget)
    *   [酷炫操作员](#cool-operators)
    *   [混合是真棒](#mixins-are-awesome)
    *   [扩展课程](#extend-your-classes)
    *   [直接在列表中使用逻辑](#use-logic-directly-in-lists)
    *   [语言怪癖](#language-quirks)
*   [总之](#in-summary)
    *   [来了...](#coming-up)
    *   [隔离更新](#quarantine-update)

* * *



## 那么什么是Flutter呢？

想要构建跨平台移动应用程序？[Flutter](https://zshipu.com/t?url=https://flutter.dev/)Flutter可以做到这一点。它运动一些很酷的功能，如：

*   支持 Android 和 iOS（测试版[中](https://zshipu.com/t?url=https://flutter.dev/web)[支持 Web](https://zshipu.com/t?url=https://flutter.dev/desktop)和桌面）。
*   使用底层 skia 库进行[快速的本机渲染](https://zshipu.com/t?url=https://skia.org/)。
*   类似于 React 的有状态开发工作流。
*   数以[百计的顶级小部件](https://zshipu.com/t?url=https://www.youtube.com/playlist?list=PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG)，船舶开箱即用。

### 我怎么想的？

👌<font _mstmutation="1" _msthash="427388" _msttexthash="757097536">总的来说，我印象非常深刻。我最初担心它不适合游戏， 但这个概念很快就被证明是错误的。它处理了我到目前为止扔给它的所有东西。</font>

用户绘制时进行实时处理、SVG 的私密操作以及整体渲染速度等关键功能都很容易实现。全面的小部件库和动画支持使 Flutter 更加甜美地使用。

### 开始

想要开始吗？查看以下链接：

*   [安装](https://zshipu.com/t?url=https://flutter.dev/docs/get-started/install)。
*   [文档](https://zshipu.com/t?url=https://flutter.dev/docs)。
*   观看他们的[YouTube 频道](https://zshipu.com/t?url=https://www.youtube.com/channel/UCwXdFgeE9KYzlDdR7TG9cMw/videos)，观看有关各种主题的摘要视频。
*   宾格他们的["本周小工具 "](https://zshipu.com/t?url=https://www.youtube.com/playlist?list=PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG)播放列表， 包括所有主要小部件的简短而翔实的视频。

### 工具

![](https://d33wubrfki0l68.cloudfront.net/06e3f4bd80018efa9189e89e07c6b963a978b418/fbe7d/images/posts/2020-05-15/emulator.png)

工具也很棒。有几个选项，但我建议开发与[VSCode。](https://zshipu.com/t?url=https://code.visualstudio.com/)作为开发体验，您可以期待：

*   只需点击保存，就热重新加载应用。
*   在桌面上启动和调试手机模拟器。
*   包管理器具有[良好的可用](https://zshipu.com/t?url=https://pub.dev/)包集合。
*   Flutter VSCode 扩展充满了伟大的小接触，使开发愉快。

![](https://d33wubrfki0l68.cloudfront.net/7a8859faa0f6db9310f06df3bf258c18aea494fc/10fc6/images/icons/vscode.png)

请考虑使用这些 VSCode 扩展：

*   （强制性）[飞溅](https://zshipu.com/t?url=https://marketplace.visualstudio.com/items?itemName=dart-code.flutter)和[Flutter](https://zshipu.com/t?url=https://marketplace.visualstudio.com/items?itemName=dart-code.dart-code)。请查看[本指南](https://zshipu.com/t?url=https://flutter.dev/docs/development/tools/vs-code)以充分利用它们。
*   使用[真棒Flutter片段](https://zshipu.com/t?url=https://marketplace.visualstudio.com/items?itemName=nash.awesome-flutter-snippets)生成常见的代码模式。
*   使用[支架对着色](https://zshipu.com/t?url=https://marketplace.visualstudio.com/items?itemName=coenraads.bracket-pair-colorizer-2)器轻松地可视化嵌套小部件。

![](https://d33wubrfki0l68.cloudfront.net/555a1057c719e979cefd78281b9f69af74ae9145/43478/images/icons/flutter.png)

要考虑使用的一些 Flutter 包是：

*   [提供程序](https://zshipu.com/t?url=https://pub.dev/packages/provider)将状态传递给深嵌套子项。
*   [用于本地](https://zshipu.com/t?url=https://pub.dev/packages/sqflite)SQLite 数据库的 Sqflite（sqflite_common_ffi用于测试）。[](https://zshipu.com/t?url=https://pub.dev/packages/sqflite_common_ffi)
*   用于常见[API](https://zshipu.com/t?url=https://pub.dev/publishers/flutter.dev/packages)功能的官方 Flutter 包，如相机支持、应用内购买和其他好东西。
*   [火基](https://zshipu.com/t?url=https://github.com/FirebaseExtended/flutterfire)包满足火基需求。

总的来说，谷歌在方便开发该平台方面做得非常出色。你真的可以快速轻松地使用漂亮的应用程序。


### Vscode 好东西

Flutter 扩展充满了漂亮的小接触。

 ![](https://d33wubrfki0l68.cloudfront.net/4478e3698a209266b323f6f03eb0f45b75ae62f1/463fa/images/posts/2020-05-15/nesting.jpg) 嵌套小部件的匹配括号可能很难找到。幸好 Flutter 扩展会自动标记它们。

 ![](https://d33wubrfki0l68.cloudfront.net/df7d4de51c79e9d6d49a235ce313c20f35af9b0d/d8f9b/images/posts/2020-05-15/popup.jpg) <font _mstmutation="1" _msthash="785681" _msttexthash="528488935">在嵌套小部件上用于一些有用的操作。请注意，"删除"删除外部小部件，但保留在子屏幕中。比手动操作快得多。</font>```Ctrl .```

 ![](https://d33wubrfki0l68.cloudfront.net/13ef79375b1e9cc0bb912088b0942ec15b1f8b1d/81c2a/images/posts/2020-05-15/colors.jpg) 图标和颜色出现在侧边栏中。悬停在他们身上也带来了更多信息。

* * *

## 给我看代码！

好吧， 那么实际使用什么感觉呢？飞[镖](https://zshipu.com/t?url=https://dart.dev/)是这里的首选语言。感觉有点像在 Typescript 中编码， React， 也许洒了 C# 。我认为它结合了所有这些更好的元素。

如果您对异步用法、有状态组件和内联函数感到自在，那么您就觉得在家。你对 OO[编程概念的了解](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/Object-oriented_programming)也会派上用场。

我强烈建议您简单地运行飞[镖语言功能](https://zshipu.com/t?url=https://dart.dev/samples#functions)，看看如何共同的事情是如何做。需要注意的是，构造[函数在](https://zshipu.com/t?url=https://dart.dev/samples#classes)Dart 中非常独特，需要学习。

### _一_切都是小部件

我的意思是一切诸如[填充](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Padding-class.html)、[对齐](https://zshipu.com/t?url=https://api.flutter.dev/flutter/painting/Alignment-class.html)小部件，甚至动画[都是](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/AnimatedContainer-class.html)通过包装其他小部件来完成的。

 ```
 // An example of how padding is applied
Padding(
    padding: EdgeInsets.only(top: 20),
    child: MyWidget(...),
),
```


### 酷炫操作员

<font _mstmutation="1" _msthash="426959" _msttexthash="144596374">有用的运算符，如空条件和空的开箱即用的装船。</font>```?.``````??```

内联函数的工作方式类似于 Javascript。

 ```
 // Assign a variable with an arrow function
setImage((Image image) => _image = image);

// Assign a variable with an inline function
setImage((Image image) {
    _image = image;
});
```


<font _mstmutation="1" _msthash="428090" _msttexthash="204063431">Dart 也有很酷的运算符，允许您将对象引用链接到任何地方。</font>```..```

 ```
 // Creates an object and assigns variables without
// traditional().method().chaining()
var paint = Paint()
    ..strokeCap = StrokeCap.round
    ..strokeJoin = StrokeJoin.round;
    ```


<font _mstmutation="1" _msthash="428844" _msttexthash="53197664">或者使用 来分割和返回整数。</font>```~/```

 ```
 var var1 = 100 / 33; // 3.0303....
var var2 = 100 ~/ 33; // 3 (int)
```


使用设置并在类中获取变量。

 ```
 bool _isValid;
bool get isValid => _isValid;
bool set isValid(bool isValid) {
    _isValid = isValid;
    updateStuff();
}
```


### 混合是真棒

<font _mstmutation="1" _msthash="427323" _msttexthash="1067437215">a 可用于封装可重用的逻辑。我使用这些所有的时间动画，计时器逻辑等，这是派上用场的地方。一个简单的混合处理计时器安全，轻松地可能看起来像：</font>```mixin```

 ```
 /// A mixin to safely handle timers in stateful widgets
mixin EasyTimer<T extends StatefulWidget> on State<T> {

  // Internal timers hidden from parent class
  List<Timer> _timers = [];

  // A public accessor used by parent widgets
  setTimer(Timer timer) => _timers.add(timer);

  // Make use of parent methods and variables
  @override
  void dispose() {
    super.dispose();

    // Safely stop timers when the widget closes
    _timers.forEach((t) => t.cancel());
  }
}
```


 ```
 // Use the mixin like this
class _MyWidgetState extends State<MyWidget> with EasyTimer {
    ...
    setTimer(...);
    ...
}
```


现在，您的所有计时器都在后台安全管理！混合素非常适合这些类型的模式。

### 扩展课程

使用[扩展方法](https://zshipu.com/t?url=https://dart.dev/guides/language/extension-methods)扩展狗屎。

 ```
 // Add a method directly to all strings
extension NumberParsing on String {
  int parseInt() => int.parse(this);
}

// Use it like this
var myNum = "12345".parseInt();
```


### 直接在列表中使用逻辑

在创建控件逻辑时，直接在列表中抛出控制逻辑。

 ```
 var widgets = [
    MyWidget(),
    ...otherWidgets, // spread em
    if (something) MyWidget(), // if em
    for (var item in items) MyWidget(), // for em
];
```


### 语言怪癖

大多数数学运算都是数字本身的方法。

 ```
 100.floor();
100.abs();
100.toInt();
100.clamp(0, 10);
```


键入通常是好的，但使用数字类型时请小心！

 ```
 // This compiles but throws an error
num myInt = 1; // Uses a generic num type
double myDouble = myInt; // Throws type error

// You have to force the type instead
double myDouble = myInt.toDouble(); // 👍 

* * *

希望你可以看到有一些很酷的功能，当开发 Flutter 应用程序。整个平台一直很高兴使用，它使应用程序创建的乐趣再次对我来说。

## 总之

这是 Flutter 的快速概述，以及您可以转到从哪里开始使用它。我希望你现在有更好的想法，你可以期待什么。在这里得出结论，是一些更先进的资源，我发现非常有帮助，得到启发和开始。

*   [Flutter 的方式](https://zshipu.com/t?url=https://www.youtube.com/watch?v=8abMF1Y2Xnk)- 一个频道展示惊人的应用程序设计与代码！
*   [这个视频](https://zshipu.com/t?url=https://www.youtube.com/watch?v=q0BBk9gDGT8)由"乐趣与Flutter"解释如何使用 Flutter 动画。
