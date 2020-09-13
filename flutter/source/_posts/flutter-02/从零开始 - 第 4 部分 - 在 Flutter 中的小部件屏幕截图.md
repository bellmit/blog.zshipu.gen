
title: 从零开始 - 第 4 部分 - 在 Flutter 中的小部件屏幕截图
author: 知识铺
date: 2020-09-13 19:10:12
tags: flutter
---
  

* * *

## 内容

*   [小部件屏幕截图](#widget-screenshots)
    *   [你在谈论什么？](#what-are-you-talking-about)
    *   [如何做到这一点](#how-to-do-it)
*   [放大镜](#magnifying-glass)
    *   [你在谈论什么？](#what-are-you-talking-about-1)
    *   [如何做到这一点](#how-to-do-it-1)

* * *

嘿， 布鲁上个月，我推出了我的第一个应用程序结冰成瘾 - 我今年正在构建的12个启动项目之一。这个系列深入探讨我是如何构建的。

刚刚开始与 Flutter？[在此处查看第一个帖子](/2020/05/15/zero-to-hero-1.html)。否则，在我的两个应用程序中试用此帖子的功能。

  [![Project photo](https://d33wubrfki0l68.cloudfront.net/f06e33fce84bdb5bb27eb2017be560b2f1043487/12aa5/images/projects/icing-addict.jpg) 
 结冰成瘾](https://zshipu.com/t?url=https://icing-addict.kangabru.xyz/) [![Project photo](https://d33wubrfki0l68.cloudfront.net/32d330dd37f475782ce9e9dc184dcbe9b5149d99/9af39/images/projects/squiggle-snek.jpg) 
 斯奎格 · 斯内克](https://zshipu.com/t?url=https://play.google.com/store/apps/details?id=com.kangabru.squiggle_snake) 

* * *

  订阅

* * *

## 小部件屏幕截图

### 你在谈论什么？

![](https://d33wubrfki0l68.cloudfront.net/c0bf91b6a6f720ca17cb3bac18a4e0d1abb71457/d39cb/images/posts/2020-06-19/screenshot.jpg)

我的"结冰成瘾"应用是所有关于创建美丽的Cookies，因此，重要的是，用户能够分享他们的创作。

我允许用户拍摄和共享其 Cookie 的图像，从而做到这一点。

有两种方法可以做到这一点 -_渲_染图像，或_截屏_图像。

在这种情况下渲染将意味着我采取饼干，颜色，装饰等，并在屏幕外画布上重建图像。

![](https://d33wubrfki0l68.cloudfront.net/836e140eac37958bfebe4c3e8b891885d6fb96f5/aeff5/images/posts/2020-06-19/pre-screenshot.jpg)

通过这样做，我可以生成任何大小的高质量图像。只是做起来比较复杂。

相反，我选择采取实时应用程序的截图。现在的手机都挤满了像素， 所以没问题。

不过，诀窍是不要捕获 Cookie 周围的应用 UI。我只想要最后图像中的饼干和装饰品。

我的技术允许我轻松截屏特定的_小部件_，并忽略我不想包括的小部件。

### 如何做到这一点

[我做了这个混合，](https://zshipu.com/t?url=https://gist.github.com/kangabru/23770a466e9366f21ea8d12d22b6f12e)这使得这个超级容易， 并公开以下方法：

*   ```screenshotThis```<font _mstmutation="1" _msthash="640523" _msttexthash="62804404">- 只需环绕您想要截屏的东西。</font>
*   ```takeScreenshot({Color, Rect})```<font _mstmutation="1" _msthash="640978" _msttexthash="124921901">- 返回具有可选背景颜色和裁剪的屏幕截图图像。</font>

请查看以下代码，了解此操作。

 <code>import 'package:flutter/material.dart';
import 'screenshot.dart'; // See my related gist for this code

class ScreenshotExample extends StatefulWidget {
  @override
  ScreenshotExampleState createState() => ScreenshotExampleState();
}

class ScreenshotExampleState extends State<ScreenshotExample> with Screenshot {
  @override
  Widget build(BuildContext context) {
    return Container(
      color: Colors.blue,
      child: Stack(children: [
        screenshotThis(
          StuffYouWantToScreenshot(),
        ),
        StuffYouDontWantToScreenshot(),
      ]),
    );
  }

  doScreenshotStuff() async {
    var screenshot = await takeScreenshot();
    // [screenshot.image] is a StatelessWidget you can render
    // [screenshot.pngBytes] is the raw image you can save/share
  }
}</code> 

<font _mstmutation="1" _msthash="426231" _msttexthash="114494666">请注意，我用于包装的小部件，我想截图。</font>```screenshotThis```

<font _mstmutation="1" _msthash="426608" _msttexthash="181258974">在我的示例中，只有小部件在图像中可见，并且 将被忽略。</font>```StuffYouWantToScreenshot``````StuffYouDontWantToScreenshot```

<font _mstmutation="1" _msthash="426985" _msttexthash="335560095">其一缺点是背景颜色（在此示例中）也不可见。相反，您可以为呼叫提供背景颜色。</font>```Colors.blue``````takeScreenshot()```

一切很酷， 对吧？

## 放大镜

### 你在谈论什么？

在移动应用上绘图的一个问题，是您的手指在绘图时确实在进行。

如果你试图做任何精确的事情 （比如玩我的游戏， 有利于准确性）， 你不能总是看到你在哪里画画。

为了解决这个问题，我构建了一个"放大镜"功能。它只是显示用户他们正在绘制，但旁边的手指，而不是在它下面。

此功能的工作方式与屏幕截图完全相同。唯一的区别是，它是在用户绘制时动态完成的。

![](https://d33wubrfki0l68.cloudfront.net/e773c3cc6bffb0ff6ab89ae3c8d88a6d0c40003b/2b571/images/posts/2020-06-19/magnifying_glass.jpg)

### 如何做到这一点

[看看我在这里的要点，](https://zshipu.com/t?url=https://gist.github.com/kangabru/883835ff2c160ef84d71a7552904c08d)其中包含另一个混合公开以下方法：

*   ```magnifyThis```<font _mstmutation="1" _msthash="640107" _msttexthash="62790000">- 只需环绕您想要放大的东西。</font>
*   ```magnifyingGlass([Color])```<font _mstmutation="1" _msthash="640562" _msttexthash="500271655">- 实际放大镜小部件，用于呈现可选的背景颜色（请参阅上一节，了解为什么您可能需要此内容）。</font>
*   ```showMagGlass(bool)```<font _mstmutation="1" _msthash="641017" _msttexthash="54074657">- 显示/隐藏放大镜小部件。</font>
*   ```updateMaGlassPosition(Offset)```<font _mstmutation="1" _msthash="641472" _msttexthash="29077308">- 更新小部件位置。</font>

使用它如下：

 <code>import 'package:flutter/material.dart';
import 'magnifying_glass.dart'; // See my related gist for this code

class MagnifyExample extends StatefulWidget {
  @override
  MagnifyExampleState createState() => MagnifyExampleState();
}

class MagnifyExampleState extends State<MagnifyExample> with MagnifyingGlass {
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanDown: (DragDownDetails details) => showMagGlass(true),
      onPanUpdate: (DragUpdateDetails details) => updateMagGlassPosition(details.localPosition),
      onPanEnd: (DragEndDetails details) => showMagGlass(false),
      child: Stack(children: [
        magnifyThis(
          StuffYouWantToMagnify(),
        ),
        magnifyingGlass(Colors.white),
      ]),
    );
  }
}</code> 

因此，正如您所看到的，它的工作方式类似于屏幕截图示例。

<font _mstmutation="1" _msthash="426582" _msttexthash="264648748">只需用 来包装您想要放大的东西，就使用 来渲染小部件，您就可以走了。</font>```magnifyThis``````magnifyingGlass()```

<font _mstmutation="1" _msthash="426959" _msttexthash="184305511">然后，在用户绘制时，我使用 来显示、隐藏和更新放大镜。</font>```GestureDetector```

<font _mstmutation="1" _msthash="427336" _msttexthash="567592870">只需确保将小部件_放在呼叫_之外。如果不是，你会得到一个时髦的镜像效果，如在视频中。很酷的效果， 虽然。</font>```magnifyingGlass()``````magnifyThis```

* * *

嗯， 今天就是这样。调谐下周， 我去看看结冰算法本身。应该是一个有趣的！再见🤙

  订阅
