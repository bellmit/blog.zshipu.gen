
title: 从零开始 - 第 3 部分 - 真棒动画在 Flutter
author: 知识铺
date: 2020-09-13 19:08:01
tags: flutter
---
  

* * *

## 内容

*   [概述](#overview)
    *   [动画基础知识](#animation-basics)
    *   [要点参考](#gist-references)
*   [缩放动画](#scale-animations)
    *   [标志](#logo)
    *   [记分卡](#score-card)
    *   [弹出](#popup)
    *   [大小](#size)
    *   [弹出按钮](#popping-buttons)
*   [过渡动画](#transition-animations)
    *   [英雄过渡](#hero-transition)
    *   [淡入](#fade-in)
    *   [滑入](#slide-in)
*   [其他动画](#other-animations)
    *   [内容滑块](#content-slider)
    *   [列表滑块](#list-slider)
    *   [按钮状态切换](#button-state-toggle)

* * *

嘿， 布鲁上个月，我推出了我的第一个应用程序结冰成瘾 - 我今年正在构建的12个启动项目之一。这个系列深入探讨我是如何构建的。

刚刚开始与 Flutter？在此处查看第一个帖子或游戏本身：

  [![Project photo](https://d33wubrfki0l68.cloudfront.net/897a33b25c9053e1df6fbefa8f54bc8f90a07203/e15ca/images/posts/2020-05-15/banner.jpg) 
 零到英雄 - 第 1 部分 - 我如何建立我的游戏与 Flutter 在 1 个月。](/2020/05/15/zero-to-hero-1) [![Project photo](https://d33wubrfki0l68.cloudfront.net/f06e33fce84bdb5bb27eb2017be560b2f1043487/12aa5/images/projects/icing-addict.jpg) 
 结冰成瘾](https://zshipu.com/t?url=https://icing-addict.kangabru.xyz/) 

* * *

  订阅

* * *

## 概述

好吧， 所以这篇文章旨在展示我如何使用动画在我的 Flutter 应用程序。

我有大量的例子，其中包括视频，高级概述和代码，让你开始。

如果您有任何问题，请一如一地联系。我们开始吧！

### 动画基础知识

我的帖子旨在激励你，让你开始。因此，我不会进入动画代码的细微细节。

而是使用这些链接来获取有关 Flutter 动画的更多信息（无论如何，它们做的更好）：

*   [官方文档将](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/animations)良好的视频和演示。
*   [这个视频](https://zshipu.com/t?url=https://www.youtube.com/watch?v=q0BBk9gDGT8)由"乐趣与Flutter"解释如何使用 Flutter 动画。

### 要点参考

我已经上传了一些小三，我会参考整个这篇文章。这些是：

*   [动画混合](https://zshipu.com/t?url=https://gist.github.com/kangabru/dbe256f2d6e6e8d357a523ad7f2ce21b)
    *   ```StateDelay```<font _mstmutation="1" _msthash="1064180" _msttexthash="203472074">- 提供常见的计时器功能和实用程序方法，以有状态的小部件。</font>
    *   ```FirstLoad```<font _mstmutation="1" _msthash="1064765" _msttexthash="146275012">- 运行在小部件首次加载时需要初始化上下文的函数。</font>
*   [动画小部件](https://zshipu.com/t?url=https://gist.github.com/kangabru/3a6c394081fc6610ac92870857ae8ced)
    *   ```AnimatedInt```<font _mstmutation="1" _msthash="1064635" _msttexthash="40920113">- 隐式动画对给定值的 int。</font>
    *   ```AnimatedScale```<font _mstmutation="1" _msthash="1065220" _msttexthash="78405054">- 隐式缩放具有可选延迟的小部件。</font>
*   [列表选取器](https://zshipu.com/t?url=https://gist.github.com/kangabru/5ed6754e50fb9c36a096b16160afcbc7)- 可滚动列表，在加载时将动画处理到位。

* * *

## 缩放动画

让我们从缩放动画开始。我用这些弹出元素， 并很好地弹出。

结合这些与延迟，你已经有了一个伟大的组合，使元素脱颖而出👌

### 标志

你在我的应用程序看到的第一件事是飞溅屏幕。我想为什么不让它流行起来呢？

正如你可以看到的标志动画很好地加载。

我宁愿没有一个飞溅屏幕， 但我用它来加载我的主屏幕资产之前， 显示他们。

我就是这样做的：

*   徽标是 SVG，但 Flutter 不支持 SVG 动画，但😥
*   相反，我将徽标 SVG 拆分为 4 个部分（文本和 3 个形状）。
*   每个图像的大小和定位都完全相同。
*   我使用比例动画和延迟为每个零件设置动画。
*   其结果是一个很酷的，动态的标志动画👌

<font _mstmutation="1" _msthash="428116" _msttexthash="231082891">我使用我的 和 代码来实现此目的。注意，我也使用[上周的帖子的功能](/2020/05/29/zero-to-hero-2.html#preload-svgs)。</font>```AnimateScale``````FirstLoad``````loadSvg```

 <code>import 'package:flutter/widgets.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'animation_mixins.dart'; // See my code reference for this gist
import 'animation_widgets.dart'; // See my code reference for this gist

class AnimatedLogo extends StatefulWidget {
  @override
  _AnimatedLogoState createState() => _AnimatedLogoState();
}

class _AnimatedLogoState extends State<AnimatedLogo> with FirstLoad {
    bool _isVisible = false;

    /// Preload svgs before animating
    loadSvgs() => Future.wait([
            loadSvg(context, LOGO_RIGHT),
            loadSvg(context, LOGO_LEFT),
            loadSvg(context, LOGO_MID),
            loadSvg(context, LOGO_TEXT),
        ]).then((_) => setState(() => _isVisible = true));

    @override
    Widget build(BuildContext context) {
        onFirstLoad(loadSvgs); // I need context to be initialised so can't use initState

        return Visibility(
            visible: _isVisible,
            child: ConstrainedBox(
                constraints: BoxConstraints(maxHeight: 200),
                child: Stack(
                children: [
                    _AnimatedStar(LOGO_RIGHT, DELAY_3),
                    _AnimatedStar(LOGO_LEFT,  DELAY_2),
                    _AnimatedStar(LOGO_MID,   DELAY_1),
                    _AnimatedStar(LOGO_TEXT, 0),
                ],
            )));
    }
}

class _AnimatedStar extends AnimatedScale {
  _AnimatedStar(String svgPath, int delay)
      : super(
          child: SvgPicture.asset(svgPath),
          curve: Curves.elasticOut,
          delay: Duration(milliseconds: delay),
          duration: Duration(milliseconds: DURATION),
        );
}</code> 

### 记分卡

好吧，这里有些事情。

*   弹出窗口动画进入视图
*   星星连续动画
*   分数增量

我将专注于星星和得分动画在这里。查看弹出窗口动画的下一节。

<font _mstmutation="1" _msthash="427349" _msttexthash="308909484">要动画的分数数，我使用我的函数。它只是一个小部件，你可以使用像。超级容易。</font>```AnimatedInt``````AnimatedInt(value: 99)```

<font _mstmutation="1" _msthash="427726" _msttexthash="332761650">星星和我的主徽标动画很相似。我使用我的小部件在每个星SVG，并错开延迟创建效果。</font>```AnimatedScale```

* * *

  订阅

* * *

### 弹出

我使用弹出窗口来显示与某些屏幕相关的内容。

我喜欢弹出它们，以提供有用的视觉上下文，你可以看到。

要创建此效果，我只需包装内置弹出窗口并应用比例过渡。

请查看下面的代码。

 <code>import 'package:flutter/material.dart';

// Creates a popup with the given widget, a scale animation, and faded background.
Future<T> showPopupDialog<T>(BuildContext context, Widget child) {
    return showGeneralDialog<T>(
        context: context,
        barrierColor: Colors.black54,
        transitionDuration: const Duration(milliseconds: 200),
        barrierDismissible: false,
        useRootNavigator: true,
        pageBuilder: (BuildContext buildContext, _, __) =>
            SafeArea(child: Builder(builder: (BuildContext context) => child)),
        transitionBuilder: (context, animation, _, child) {
            return ScaleTransition(
                scale: CurvedAnimation(parent: animation, curve: Curves.decelerate),
                child: child,
            );
        },
    );
}</code> 

### 大小

有时，当屏幕加载时，内容未就绪。我喜欢将内容跳转到视图中，而不是让内容跳转到视图中。

您可以在视频中看到，在页面加载后，分数会稍微加载。容器的动画很好，以适应这一点。

<font _mstmutation="1" _msthash="426946" _msttexthash="412019790">为此，我包装内置小部件中的内容。现在，当内容更改大小时，任何父容器都将设置动画！</font>```AnimatedSize```

 <code>import 'package:flutter/widgets.dart';

class GrowbleContainer extends StatefulWidget {
    final Widget child:
    GrowbleContainer({this.child});
    createState() => GrowbleContainerState();
}

class GrowbleContainerState extends State<GrowbleContainer> with TickerProviderStateMixin {
    @override
    Widget build(BuildContext context) {
        return AnimatedSize(
            vsync: this, // Provided by TickerProviderStateMixin
            duration: Duration(milliseconds: 200),
            curve: Curves.fastOutSlowIn,
            child: widget.child,
        );
    }
}</code> 

### 弹出按钮

我在整个应用中使用一个通用按钮，我动态地显示/隐藏该按钮。

我想他们进来和出去会更好， 你可以看到。

比让他们突然出现更酷， 不是吗？

<font _mstmutation="1" _msthash="429585" _msttexthash="271211694">您可以通过使用我的小部件包装小部件并像这样动态更新比例来实现此目的。</font>```AnimatedScale```

 <code>import 'package:flutter/material.dart';
import 'animation_widgets.dart'; // See my code reference for this gist

class PoppingContainer extends StatefulWidget {
  final Widget child;
  final bool visible;
  PoppingContainer({
    this.child,
    this.visible = true,
  });

  @override
  State<StatefulWidget> createState() => PoppingContainerState();
}

class PoppingContainerState extends State<PoppingContainer> {
  @override
  Widget build(BuildContext context) {
    return AnimatedScale(
      tweenInit: Tween(begin: 1.0, end: 1.0),
      tween: Tween(begin: 0.0, end: widget.visible ? 1.0 : 0.0), // Update scale dynamically
      duration: Duration(milliseconds: 600),
      curve: Curves.elasticOut,
      child: widget.child,
    );
  }
}</code> 

* * *

## 过渡动画

本节介绍如何使用过渡使屏幕之间的导航更有趣。

### 英雄过渡

Flutter 的一个惊人的功能是 "英雄" 动画支持。这是元素将在两个单独的屏幕之间转换的地方。

我的视频显示一个示例，其中我的 Cookie 在选择屏幕和游戏屏幕之间进行动画处理。

它是如此令人难以置信的容易实现，你没有任何借口不使用它！

<font _mstmutation="1" _msthash="427297" _msttexthash="198950167">实际上，你只需要用每个屏幕上的小部件包装一个通用小部件。</font>```Hero```

 <code>Hero(
    tag: "some_unique_string_id",
    child: YourWidget(),
),</code> 

动画是自动完成的，并处理缩放和👌

请注意，在一个屏幕上不能有多个具有相同 ID 的小部件（如视频中的 Cookie 选择屏幕）。

在我的情况下，我使用级别名称，以便每个 ID 是唯一的，但仍可在选择和游戏屏幕使用。

### 淡入

在上面的英雄动画视频中，您会注意到有一个淡入淡出的过渡也是怎么回事。

您可以轻松实现此功能，如下所示：

 <code>import 'package:flutter/widgets.dart';

/// Fades to a new route rendering the given widget.
class FadeRoute<T> extends PageRouteBuilder<T> {
    FadeRoute(Widget page)
        : super(
            pageBuilder: (_, __, ___) => page,
            transitionDuration: const Duration(milliseconds: 600),
            transitionsBuilder: (context, animation, secondaryAnimation, child) =>
                FadeTransition(opacity: animation, child: child),
            );
}

/// Simple wrapper which fades to a new route rendering the given widget.
Future<T> fadeToRoute<T>(BuildContext context, Widget page) =>
    Navigator.push<T>(context, FadeRoute<T>(page));

// Use manually like this
Navigator.push(context, FadeRoute(MyWidget()));

// Or use the wrapper like this
fadeToRoute(context, MyWidget());</code> 

### 滑入

滑动也很容易做到。此代码从屏幕左侧滑入和滑出

 <code>import 'package:flutter/widgets.dart';

/// Slide right to a new route rendering the given widget.
class RightSlideRoute<T> extends PageRouteBuilder<T> {
    RightSlideRoute(Widget page)
        : super(
            pageBuilder: (_, __, ___) => page,
            transitionsBuilder: (_, animation, __, child) => SlideTransition(
                  position: Tween<Offset>(
                    begin: const Offset(-1, 0),
                    end: Offset.zero,
                  ).animate(animation),
                  child: child,
                ));
}

/// Simple wrapper which slide right to a new route rendering the given widget.
Future<T> slideToRoute<T>(BuildContext context, Widget page) =>
    Navigator.push<T>(context, RightSlideRoute<T>(page));

// Use manually like this
Navigator.push(context, RightSlideRoute(MyWidget()));

// Or use the wrapper like this
slideToRoute(context, MyWidget());</code> 

* * *

  订阅

* * *

## 其他动画

以下是我在应用中使用动画的一些其他方法。

### 内容滑块

当您可以在图像之间滑动时，为什么要在图像之间翻转？

我使用一个伟大的库[flutter_swiper](https://zshipu.com/t?url=https://pub.dev/packages/flutter_swiper)它提供了各种滑动魔术。

在这里你可以看到我用它来在内容之间导航。您也可以与它互动！

<font _mstmutation="1" _msthash="445029" _msttexthash="353806648">这里还有一件事是我如何为背景动画。我使用内置的，只需在滑块更新时更新颜色即可。</font>```AnimatedContainer```

此代码显示如何设置滑块小部件，并在幻灯片时为背景设置动画：

 <code>import 'package:flutter/material.dart';
import 'package:flutter_swiper/flutter_swiper.dart';

class SwiperExample extends StatefulWidget {
  final List<String> images;
  final List<Color> colors;
  SwiperExample({this.images, this.colors});

  @override
  SwiperExampleState createState() => SwiperExampleState();
}

class SwiperExampleState extends State<SwiperExample> {
  int _imageIndex = 0;

  @override
  Widget build(BuildContext context) {
    var color = widget.colors[_imageIndex % widget.colors.length];

    return AnimatedContainer(
      color: color,
      duration: Duration(milliseconds: 1500),
      child: Swiper(
        loop: true,
        autoplay: true,
        autoplayDelay: _TRANSITION_DURATION,
        onIndexChanged: (index) => setState(() => _imageIndex = index),
        itemCount: widget.images.length,
        itemBuilder: (BuildContext context, int index) {
          var image = widget.images[index];
          return Image.asset(image);
        },
      ),
    );
  }
}</code> 

### 列表滑块

我构建了一个自定义颜色选取器，我的应用程序。这是一个简单的可滚动列表，你可以在视频中看到。

我启动时有一个问题， 用户没有意识到列表是可滚动的！

所以我添加了一个不错的小动画，表示有更多的颜色可供选择。

如您所看到的，加载列表时小部件微微滚动。

<font _mstmutation="1" _msthash="445016" _msttexthash="287209286">看看我[的列表滑块要点，](https://zshipu.com/t?url=https://gist.github.com/kangabru/5ed6754e50fb9c36a096b16160afcbc7)其中包含小部件。像使用任何其他列表一样使用它： 。</font>```ListPicker(children: <Widget>[...])```

<font _mstmutation="1" _msthash="445406" _msttexthash="285591839">它基本上包装内置小部件，并在加载时执行滚动。正确是有点棘手， 但值得。</font>```SingleChildScrollView```

### 按钮状态切换

我创建了我自己的按钮小部件，以实现我后要的特定风格。

不幸的是， 这意味着我也得滚自己的动画！

你可以在视频中看到，我有一个微妙的按下状态动画，用户点击按钮。

<font _mstmutation="1" _msthash="444223" _msttexthash="269639994">要实现这一点，我使用小部件并调整阴影大小和边距，使其看起来按下。</font>```AnimatedContainer```

查看创建阴影外观的此代码，并在按下或不按下时对它进行动画。

 <code>import 'dart:math';
import 'package:flutter/material.dart';

const double _SHADOW_SIZE_MIN = 2.0;
const double _SHADOW_SIZE_MAX = 6.0;

class ShadowContainer extends StatelessWidget {
  final Widget child;
  final bool isPressed;
  final EdgeInsetsGeometry padding, margin;

  ShadowContainer({
    @required this.child,
    this.isPressed: false,
    this.padding = const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
    this.margin = const EdgeInsets.fromLTRB(5, 5, 5, 10),
  });

  @override
  Widget build(BuildContext context) {

    // Make the shadow large when normal and small when pressed
    var shadowOffset = isPressed ? _SHADOW_SIZE_MIN : _SHADOW_SIZE_MAX;

    // Adjust the button down when pressed and up when normal
    var marginOffset = isPressed ? _SHADOW_SIZE_MAX - _SHADOW_SIZE_MIN : 0;
    var marginTop = EdgeInsets.only(top: marginOffset);
    var marginBot = EdgeInsets.only(bottom: marginOffset);

    return AnimatedContainer(
        child: child,
        padding: padding,
        margin: margin.add(marginTop).subtract(marginBot),
        duration: Duration(milliseconds: 30),
        decoration: new BoxDecoration(boxShadow: [
          BoxShadow(
              color: Colors.black,
              offset: Offset.fromDirection(pi / 2, shadowOffset))
        ]));
  }
}</code> 

* * *

就是这样！希望你学到了一些东西或受到启发，将动画添加到你的应用。

一旦你得到他们的窍，Flutter动画是相当简单的实现。你所有你需要做的就是开始！

一如既往，如有疑问，请一直伸出援手，下次见！

  订阅
