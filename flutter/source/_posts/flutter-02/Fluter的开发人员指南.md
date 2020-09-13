
title: Fluter的开发人员指南
author: 知识铺
date: 2020-09-13 17:13:43
tags: 
---
 自从这是期待已久的发射，Flutter已经引起了很多的关注，我们也很兴奋！我希望大量的非游戏应用程序将过渡到Flutter， 在预期中， 因此， 我们正在训练我们的团队。

由于有新的，但很少，资源分散在互联网上学习飘飘 - 我们已经编译了我们的 Flutter 教程，让开发人员离开他们的脚，并开始开发 Flutter 的应用程序。

在初学者的 Flutter 指南中，我们将介绍：

*   Flutter：什么，如何，为什么？
*   设置Flutter
*   飞镖基础知识
*   Flutter基础知识
*   部件
*   布局
*   交互式小部件
*   设计应用：窗体、手势和图像
*   列表和导航
*   网络
*   JSON 和序列化
*   依赖性管理
*   状态管理
*   测试（单元和集成）

# [](https://zshipu.com/t?url=#flutter-what-how-and%C2%A0why)<font _mstmutation="1" _msthash="289380" _msttexthash="78816751">Flutter：什么，如何，为什么？</font>

什么是Flutter，它有什么不同？请记住这一点 - Flutter 专为任何具有屏幕的设备工作而构建，并适用于：

*   ios 和安卓系统
*   Web 和桌面（Mac、Windows 和 Ubuntu） - 甚至支持 PWA
*   自动
*   树莓派（POC 阶段）

查看谷歌的这段视频;这是一个伟大的地方得到一个掌握 - 比较本机开发，混合应用程序开发，反应本机开发，最后[，Flutter应用程序开发](https://zshipu.com/t?url=https://www.solutelabs.com/flutter-app-development-services)。

以下是新版 Flutter 和 Dart 编程语言的发布最新消息 -

  [![Milind Mevada](https://res.cloudinary.com/practicaldev/image/fetch/s--30fhcgVh--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://miro.medium.com/fit/c/96/96/2%2AuXblXMvv7YLLjiDiZobkVw.png)](https://zshipu.com/t?url=https://blog.solutelabs.com/google-launched-flutter-sdk-1-2-and-dart-programming-language-2-2-8ebab5500fb)  [## 谷歌推出 Flutter SDK 1.2 和飞镖编程语言 2.2 |由米林德·梅瓦达 »学习 v/s 忘记 |索卢特实验室

### <font _mstmutation="1" _msthash="837044" _msttexthash="93799368">米林德·梅瓦达 • 2019年4月1日~ 3分钟 阅读</font>
 ![Medium Logo](https://res.cloudinary.com/practicaldev/image/fetch/s--KBvj_QRD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://practicaldev-herokuapp-com.freetls.fastly.net/assets/medium_icon-90d5232a5da2369849f285fa499c8005e750a788fdbf34f5844d5f2201aae736.svg)<font _mstmutation="1" _msthash="1125293" _msttexthash="397644">blog.solutelabs.com</font>](https://zshipu.com/t?url=https://blog.solutelabs.com/google-launched-flutter-sdk-1-2-and-dart-programming-language-2-2-8ebab5500fb) 

# [](https://zshipu.com/t?url=#setting-up%C2%A0flutter)<font _mstmutation="1" _msthash="303784" _msttexthash="13976898">设置Flutter</font>

Flutter 设置起来相对简单，具体取决于您使用的操作系统;你可以看看这个官方 Flutter 教程中的步骤：

[https://flutter.dev/docs/get-started/install](https://zshipu.com/t?url=https://flutter.dev/docs/get-started/install)

但万一，你遇到的东西，看看这里[：https://github.com/flutter/flutter/wiki/Workarounds-for-common-issues#flutter-installation](https://zshipu.com/t?url=https://github.com/flutter/flutter/wiki/Workarounds-for-common-issues#flutter-installation)

我们要求你在飞镖之前设置 Flutter 的原因是因为当你安装 Flutter 时， 你安装飞镖太， 虽然你可以单独安装飞镖， 这将是一个不必要的步骤.Flutter 将决定使用哪个飞镖版本，因此安装不同的飞镖版本也将是模棱两可的。

下载并解压缩 Flutter 后，在控制台上运行 flutter 命令时应看到类似这样的内容：

[![flutter development](https://res.cloudinary.com/practicaldev/image/fetch/s--Z0NRoy7O--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AaIAn1ORPEBwUY1krrd8iDA.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--Z0NRoy7O--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AaIAn1ORPEBwUY1krrd8iDA.png)

如果您是移动开发[的新人](https://zshipu.com/t?url=https://www.solutelabs.com/mobile-app-development)，您还需要下载[Xcode 和](https://zshipu.com/t?url=https://developer.apple.com/xcode/) [Android Studio（](https://zshipu.com/t?url=https://developer.android.com/studio/index.html)以及工具链）。设置 Flutter 后，基架新项目只是一个命令。

# [](https://zshipu.com/t?url=#dart-basics)<font _mstmutation="1" _msthash="303459" _msttexthash="24145199">飞镖基础知识</font>

Flutter 使用[飞镖语言](https://zshipu.com/t?url=https://dart.dev)构建应用。要了解为什么 Flutter 使用飞镖， 请查看我以前的博客， 并到部分 - **Flutter 是如何出生的**

  [![Karan Shah](https://res.cloudinary.com/practicaldev/image/fetch/s--EXMS1_El--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://miro.medium.com/fit/c/96/96/2%2Ayozc3QDZFjhfqvTv30VFOg.png)](https://zshipu.com/t?url=https://blog.solutelabs.com/flutter-for-your-next-product-idea-everything-you-need-to-know-f5179a925524)  [## 为您的下一个"产品"创意而飘荡 [您需要了解的一切]由卡兰·沙阿 »学习 v/s 忘记 |索卢特实验室

### <font _mstmutation="1" _msthash="837681" _msttexthash="78190684">卡兰沙阿 • 2020 年 5 月 25日 = 12 分钟阅读</font>
 ![Medium Logo](https://res.cloudinary.com/practicaldev/image/fetch/s--KBvj_QRD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://practicaldev-herokuapp-com.freetls.fastly.net/assets/medium_icon-90d5232a5da2369849f285fa499c8005e750a788fdbf34f5844d5f2201aae736.svg)<font _mstmutation="1" _msthash="1125930" _msttexthash="397644">blog.solutelabs.com</font>](https://zshipu.com/t?url=https://blog.solutelabs.com/flutter-for-your-next-product-idea-everything-you-need-to-know-f5179a925524) 

飘逸和铬使用相同的渲染引擎 - SKIA。它无需与本机 API 交互，而是控制屏幕上的每个像素，从而获得远离旧行李以及性能所需的自由。

一定[给官方](https://zshipu.com/t?url=https://flutter.dev/docs/resources/faq#why-did-flutter-choose-to-use-dart)文档读一读， 但我发现这个善于解释飞镖

[为什么Flutter使用飞镖](https://zshipu.com/t?url=https://hackernoon.com/why-flutter-uses-dart-dd635a054ebf)

P. s. 您可以跟进他们的媒体帐户的[飞镖更新](https://zshipu.com/t?url=https://medium.com/dartlang)

现在，你知道为什么[谷歌](https://zshipu.com/t?url=https://en.m.wikipedia.org/wiki/Google)选择飞镖 - 所以让我们把你的手弄脏！

### [](https://zshipu.com/t?url=#learn-dart)<font _mstmutation="1" _msthash="306501" _msttexthash="13764452">学习飞镖</font>

看看飞镖语言的官方文档[，旅游，](https://zshipu.com/t?url=https://dart.dev/guides/language/language-tour)和他们的语言[样本](https://zshipu.com/t?url=https://dart.dev/samples)。

一旦你有一个概述[，http://jpryan.me/dartbyexample/，](https://zshipu.com/t?url=http://jpryan.me/dartbyexample/)做所有的例子宗教。

### [](https://zshipu.com/t?url=#practice-practice-practice)<font _mstmutation="1" _msthash="304616" _msttexthash="51817857">练习，练习，练习！</font>

在[DartPad](https://zshipu.com/t?url=https://dartpad.dartlang.org/)上编辑代码，以获得更好的抓地力。我相信你很快就会启动并运行！

[![My First Hello, World! in Dart](https://res.cloudinary.com/practicaldev/image/fetch/s--mdZmTXeW--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2Aj5k-sQWAqf0LHl_SUR3_Gg.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--mdZmTXeW--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2Aj5k-sQWAqf0LHl_SUR3_Gg.png)

之后， 你完成了飞镖例， 头到外在主义， 并完成他们的飞镖轨道。很时髦，所以万一它满了，你也可以做练习轨道。

[飞镖 |Exercism](https://zshipu.com/t?url=https://exercism.io/tracks/dart)

# [](https://zshipu.com/t?url=#flutter-basics)<font _mstmutation="1" _msthash="305630" _msttexthash="22369373">Flutter基础知识</font>

现在你熟悉了飞镖， 终于是时候继续飞溅了

[![penguin gif](https://res.cloudinary.com/practicaldev/image/fetch/s--DcjGaPC5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AjHSZ0_y9aoas3UxUMkRMZw.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--DcjGaPC5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AjHSZ0_y9aoas3UxUMkRMZw.gif)

让我们从这里的技术概述开始：

[技术概述](https://zshipu.com/t?url=https://flutter.dev/docs/resources/technical-overview)

<font _mstmutation="1" _msthash="291174" _msttexthash="90244310">和脚手架一个新的Flutter应用程序与：</font>

 <code>$ flutter create app_name</code> 

你应该看到类似的东西：

[![android studio](https://res.cloudinary.com/practicaldev/image/fetch/s--nV911Awg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2A3KBHP-3nKyS3XP8bTma2Yw.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--nV911Awg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2A3KBHP-3nKyS3XP8bTma2Yw.png)

打开 Android 工作室上的项目， 下载模拟器， 和 Android 版本， 如果还没有完成， 并运行项目 - 和等 voila！

[![Flutter demo](https://res.cloudinary.com/practicaldev/image/fetch/s--qCyMYCjg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AdA0ntm5vz0xGyDYsp2-f7g.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--qCyMYCjg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AdA0ntm5vz0xGyDYsp2-f7g.png)

了解应如何构建项目目录，并了解哪些文件用于哪个目的

[Flutter项目结构](https://zshipu.com/t?url=https://dev.to/jay_tillu/flutter-project-structure-1lhe)

现在，您已经设置了飘飘，是时候做所有开发人员都做的事情了！使用其他人的代码😆 - 我的意思是设置包文件： pubspec， 写在 Yaml

[pubspec 文件](https://zshipu.com/t?url=https://dart.dev/tools/pub/pubspec)

### [](https://zshipu.com/t?url=#widgets)<font _mstmutation="1" _msthash="305214" _msttexthash="5477992">部件</font>

> _记住 - 一切都是 Flutter 中的小部件_

如果您没有像我们之前询问的您那样阅读技术概述，请返回并阅读:)你会得到一个公平的想法，什么是小部件。小部件有两种口味：**_无状态_****_和有状态_**

无状态小部件是那些状态不会像按钮或图像一样更改的小部件。如名称状态，当在屏幕上执行操作时，它不会更改其状态。

查看短视频系列，以及 Google 提供[的文档](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/StatelessWidget-class.html)，以深入探讨（我附上该系列中的第一个视频）。

当小部件需要保持某些状态，如[PageView](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/PageView-class.html)中的当前页面时，当前选择的选项卡位于[底部导航](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/PageView-class.html)栏中，有状态的小部件是正确的选择。

有状态的小工具可以保持小部件的当前状态。状态小部件具有状态生成方法，它每次显式[调用](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/State-class.html)setState 时调用 ，而不是小部件**_生成方法_**。

同样，请查看此处有状态小部件的文档（里面有视频） ：

[状态的Widget类](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/StatefulWidget-class.html)

Flutter 1.9 在[GDD 中国](https://zshipu.com/t?url=https://developers.googleblog.com/2019/09/flutter-news-from-gdd-china-flutter1.9.html?m=1)发布，具有许多新功能和标志，社区正在成倍增长（现在不能忽视中国）

## [](https://zshipu.com/t?url=#layouts-in%C2%A0flutter)<font _mstmutation="1" _msthash="305240" _msttexthash="19881719">Flutter 中的布局</font>

正如我们前面讨论的，一切都是 Flutter 中的小部件 - 包括布局模型。

在此处查看文档：

[Flutter 中的布局](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/layout)

行、列和网格等小部件是布局小部件（我们在屏幕上看不到），可帮助其他可见小部件排列、约束和对齐。

> ⏰实验室的时间： 写你的[_第一个 Flutter 应用程序： 第 1 部分_](https://zshipu.com/t?url=https://codelabs.developers.google.com/codelabs/first-flutter-app-pt1/#0)

## [](https://zshipu.com/t?url=#and-some-more%C2%A0widgets)<font _mstmutation="1" _msthash="307112" _msttexthash="33571928">还有一些小工具！</font>

Flutter附带一套强大的基本小部件，如文本[，列](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Text-class.html)[，](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Column-class.html)[行，](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Row-class.html)[堆栈](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Stack-class.html)和[容器](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Container-class.html)。基本小部件将帮助您创建自定义视图。您可以。

如果你的应用遵循[材料设计准则，Flutter](https://zshipu.com/t?url=https://material.io/design/guidelines-overview/)在默认情况下有很多要涵盖的。Flutter 提供了多个支持材料设计的小部件。它包括小部件，如[材料应用程序](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/MaterialApp-class.html)，[应用栏](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/AppBar-class.html)[，脚手架](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/Scaffold-class.html)等。

[![Material Navigation Drawer (https://material.io/components/navigation-drawer/#)](https://res.cloudinary.com/practicaldev/image/fetch/s--3tEXyTQ7--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/0%2ANibO5ZD4c_QJMAHR.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--3tEXyTQ7--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/0%2ANibO5ZD4c_QJMAHR.png)

飘飘还包括以 iOS 为中心的[Cupertino 组件](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/widgets/cupertino)包。它涵盖了小部件，如[库比蒂诺应用程序](https://zshipu.com/t?url=https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)[，库比蒂诺导航酒吧](https://zshipu.com/t?url=https://api.flutter.dev/flutter/cupertino/CupertinoNavigationBar-class.html)等。

[![Cupertino NavigationBar (https://developer.apple.com/design/human-interface-guidelines/ios/bars/navigation-bars/)](https://res.cloudinary.com/practicaldev/image/fetch/s--8DrYiFpv--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/0%2A3GR_8PDpRyl4Tvmv.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--8DrYiFpv--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/0%2A3GR_8PDpRyl4Tvmv.png)

## [](https://zshipu.com/t?url=#interactive-widgets)<font _mstmutation="1" _msthash="306163" _msttexthash="18292885">交互式小部件</font>

到目前为止，我们已经看到在屏幕上显示信息或排列其他小部件的小部件。对于真正的应用程序，同样重要的是使应用程序互动，并获得用户的各种形式，如手势，点击等用户的意见。

为此，Flutter 具有状态数字，如复选框、收音机、[滑块、](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/Slider-class.html)[墨水井](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/InkWell-class.html)[](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/Checkbox-class.html)[、窗体](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Form-class.html)[和文本字段](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/TextField-class.html)等。 [](https://zshipu.com/t?url=https://api.flutter.dev/flutter/material/Radio-class.html)这些小部件足以保持其状态（例如，我们在 TextField 中输入的文本，无论是否选中检查列表）。

转到下面的示例，将收藏夹/非收藏夹功能添加到应用。

[向 Flutter 应用添加交互性](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/interactive)

> ⏰_时间：写你的_[_第一个Flutter应用程序：第2部分_](https://zshipu.com/t?url=https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2/#0)
> 
> _正如您到达这里， 你应该**清楚什么是小部件？**和**小工具的类型**_

现在，你一定好奇在 Flutter 中有什么小部件可用？

因此，这里是一个小部件目录，检查所有的小部件，使 Flutter 开发放松和乐趣😍

[小部件目录](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/widgets)

## [](https://zshipu.com/t?url=#flutter-cookbook)<font _mstmutation="1" _msthash="306150" _msttexthash="15005653">Flutter食谱</font>

在这里，我们开始，是时候学习 Flutter 真正的应用程序。我的意思是具有多个屏幕、图像、网络依赖项等的应用。

所以，让我们开始吧。

## [](https://zshipu.com/t?url=#designing-an%C2%A0app)<font _mstmutation="1" _msthash="307086" _msttexthash="21948719">设计应用程序</font>

请查看下面的应用插图。

[![-----------------](https://res.cloudinary.com/practicaldev/image/fetch/s--5a56KpL---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AFVbUPfA8Q03E7_old_Yajw.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--5a56KpL---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AFVbUPfA8Q03E7_old_Yajw.gif)

这个简单看起来的应用程序有这些功能👇

1.  导航抽
    屉[https://flutter.dev/docs/cookbook/design/drawer](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/design/drawer)

2.  小吃
    [https://flutter.dev/docs/cookbook/design/snackbars](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/design/snackbars)

3.  自定义字体（文本有其自己的样式
    [😉）https://flutter.dev/docs/cookbook/design/package-fonts](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/design/package-fonts)

4.  基于[方向](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/widgets/text)的文本（横向中更大的字体
    [）https://flutter.dev/docs/cookbook/design/orientation](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/design/orientation)

5.  并且，多个选项卡
    [https://flutter.dev/docs/cookbook/design/tabs](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/design/tabs)

> _**请注意：定向**构建器与设备的方向无关。相反，它通过比较父小部件可用的宽度和高度来计算当前方向。要确定设备的方向，您可以参考**MediaQuery.of（上下文） 方向**_

## [](https://zshipu.com/t?url=#forms)<font _mstmutation="1" _msthash="306137" _msttexthash="4752878">形式</font>

Flutter 具有**表单**小部件，可帮助构建一个表单，该表单可以有效地管理窗体的基本要求，例如，窗体的状态、验证等。请查看以下文档中的完整公会。

[食谱](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook#forms)

## [](https://zshipu.com/t?url=#gestures)<font _mstmutation="1" _msthash="307073" _msttexthash="4492865">手势</font>

为了获得用户输入和一些时间，使应用程序超级互动，我们最大限度地使用手势。Flutter 具有预构建的小部件来涵盖这一点。

1.  添加材质波纹
    [https://flutter.dev/docs/cookbook/gestures/ripples](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/gestures/ripples)

2.  手柄水龙头
    [https://flutter.dev/docs/cookbook/gestures/handling-taps](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/gestures/handling-taps)

3.  轻扫
    [至https://flutter.dev/docs/cookbook/gestures/dismissible](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/gestures/dismissible)

## [](https://zshipu.com/t?url=#images)<font _mstmutation="1" _msthash="308009" _msttexthash="4178018">图像</font>

为了让应用程序美观和吸引人，我们使用图像。Flutter 提供了一**个**图像小部件，用于在各种来源的 Flutter 应用中显示图像。

1.  显示来自网络的图像

[显示来自互联网的图像](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/images/network-image)

1.  使用占位符和淡入动画显示图像

[使用占位符淡入图像](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/images/fading-in-images)

1.  有时，从网络加载映像并缓存在本地存储中使其下次快速可用非常方便。

[使用缓存的图像](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/images/cached-images)

## [](https://zshipu.com/t?url=#showing-more-data-using%C2%A0list)<font _mstmutation="1" _msthash="320658" _msttexthash="39517426">使用列表显示更多数据</font>

为了容纳更多的数据，我们使用列表来显示它们。列表可以是水平或线性的。

Flutter 具有[网格视图和](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/GridView-class.html)[列表视图](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/ListView-class.html)。这些是具有不同承包商的基本小部件，用于标识如何使用它们。

1.  创建网格列表

[创建网格列表](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/lists/grid-lists)

1.  水平创建列表

[创建水平列表](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/lists/horizontal-list)

1.  该列表可以具有不同类型的项目。例如，标题和项目。在此处查看如何在 ListView 中涵盖此类案例。

[创建具有不同类型的项目的列表](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/lists/mixed-list)

1.  使用 SliverList 浮动应用条和嵌套滚动

[在列表上方放置一个浮动应用栏](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/lists/floating-app-bar)。

#### [](https://zshipu.com/t?url=#dont-forget-to-check-out-this-awesome-article-by-emily-fortuna-to-understand-slivers-in%C2%A0depth)_别忘了看看艾米莉 ·[福图纳](https://zshipu.com/t?url=https://medium.com/flutter/slivers-demystified-6ff68ab0296f)的这篇令人敬畏的文章， 深入地了解斯李弗_

1.  有时，我们将预定义的任意项放在列表中。例如，设置类别。在 ListView 中，您可以将自定义项（以小部件的形式）传递给其子项。

[使用列表](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/lists/basic-list)

1.  有时，列表包含的项目比屏幕的视口更多。在这种情况下，一次生成所有项是没有意义的。Flutter 具有_**ListView.Builder，**_它使用惰性呈现方法高效地创建列表项。

[使用长列表](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/lists/long-lists)

如果列表中有更多的项目，并且希望将它们分页。这是我找到的一篇好👇

  [![Aakash D. Mehta](https://res.cloudinary.com/practicaldev/image/fetch/s--9GfWi_OX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://miro.medium.com/fit/c/96/96/0%2AIHvwEaxGsJzYFJXj.jpg)](https://zshipu.com/t?url=https://blog.solutelabs.com/paginate-your-data-in-flutter-7744995febd1)  [## 飞溅列表查看无限滚动的分页 （指南） |学习 v/s 忘记 |索卢特实验室

### <font _mstmutation="1" _msthash="869141" _msttexthash="87738430">Aakash D. Mehta = 2020 年 5 月 25日 = 3 分钟阅读</font>
 ![Medium Logo](https://res.cloudinary.com/practicaldev/image/fetch/s--KBvj_QRD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://practicaldev-herokuapp-com.freetls.fastly.net/assets/medium_icon-90d5232a5da2369849f285fa499c8005e750a788fdbf34f5844d5f2201aae736.svg)<font _mstmutation="1" _msthash="1164072" _msttexthash="397644">blog.solutelabs.com</font>](https://zshipu.com/t?url=https://blog.solutelabs.com/paginate-your-data-in-flutter-7744995febd1) 

## [](https://zshipu.com/t?url=#navigating-between-screens-aka%C2%A0routes)<font _mstmutation="1" _msthash="320632" _msttexthash="60304738">在屏幕之间导航， 又名路由</font>

大多数应用都包含多个屏幕，以组织良好的方式显示数据。

在 Flutter 中，我们可以使用导航器执行与导航[相关的操作](https://zshipu.com/t?url=https://api.flutter.dev/flutter/widgets/Navigator-class.html)。
请查看下图以了解 Flutter 如何管理多个路由，稍后，我们将讨论如何在它们之间来回导航。

[![-----------------](https://res.cloudinary.com/practicaldev/image/fetch/s--whiFAqMI--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AoqlVDLGspU6203J22EQPZg.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--whiFAqMI--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AoqlVDLGspU6203J22EQPZg.png)

1.  导航到新屏幕并返回

[导航到新屏幕并返回](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/navigation/navigation-basics)

1.  将数据传递到新屏幕并检索结果。

[将数据发送到新屏幕](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/navigation/passing-data)

[从屏幕返回数据](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/navigation/returning-data)

> _到目前为止，我们所看到的是适合小型项目。但是，当项目增长时，我们希望在一个位置管理所有路由。此外，我们可能需要解决以下问题_
> 
> 1.  我们有多少条路线？
> 2.  如何初始化每条路线？
> 3.  每条路线都需要哪些数据？等。。

1.  为了有效地管理所有这些，Flutter 指定了路由。

[使用命名路由导航](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/navigation/named-routes)

1.  在命名路由中传递参数。

[将参数传递给命名路由](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/navigation/navigate-with-arguments)

导航到新屏幕时，此动画如何？

[![Hero animation (https://flutter.dev/docs/cookbook/navigation/hero-animations)](https://res.cloudinary.com/practicaldev/image/fetch/s--fCYN1lo0--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://cdn-images-1.medium.com/max/800/0%2AgK4EzVCEIToPH_Rh.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--fCYN1lo0--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://cdn-images-1.medium.com/max/800/0%2AgK4EzVCEIToPH_Rh.gif)

1.  在屏幕上为小部件设置动画

[在屏幕上为小部件设置动画](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/navigation/hero-animations)

## [](https://zshipu.com/t?url=#networking)<font _mstmutation="1" _msthash="320606" _msttexthash="6343467">网络</font>

我们现在遇到大多数应用程序，通常连接到第三方服务器，并发出请求到服务器提取或发布数据。

在 Flutter 中， 我们可以使用 Http 作为第三方酒吧做这样的事情。

[http飞镖包](https://zshipu.com/t?url=https://pub.dev/packages/http)

1.  从网络获取数据

[从互联网获取数据](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/networking/fetch-data)

1.  发出经过身份验证的请求

[发出经过身份验证的请求](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/networking/authenticated-requests)

1.  使用 Web 套接字

[使用 Web 袜子](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/networking/web-sockets)

[Flutter 有更多的酒吧可用， 这样做的更高效。别忘了看看下面的酒吧。](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/networking/web-sockets)

[迪奥 |飞镖包](https://zshipu.com/t?url=https://pub.dev/packages/dio)

[直升机 |飞镖包](https://zshipu.com/t?url=https://pub.dev/packages/chopper)

## [](https://zshipu.com/t?url=#using-json-and-serialization)<font _mstmutation="1" _msthash="321893" _msttexthash="21599617">使用 JSON 和序列化</font>

在 Flutter 中，我们通常有两种 JSON 序列化策略。使用代码生成手动解析和自动序列化。

> _运行时[反射](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/Reflection_(computer_programming))在 Flutter 中被禁用，因此我们不能有像[GSON、Jackson](https://zshipu.com/t?url=https://github.com/google/gson)[或 Moshi](https://zshipu.com/t?url=https://github.com/FasterXML/jackson-core) [这样的库](https://zshipu.com/t?url=https://github.com/square/moshi)_

在此处查看两种策略的完整指南：

[JSON 和序列化](https://zshipu.com/t?url=https://flutter.dev/docs/development/data-and-backend/json)

对于手动解析，不要忘记查看此在线工具，以自动生成模型类的样板。

[以任何语言即时解析 Json |快速类型](https://zshipu.com/t?url=https://app.quicktype.io/)

## [](https://zshipu.com/t?url=#data-persistence)<font _mstmutation="1" _msthash="321230" _msttexthash="14100424">数据持久性</font>

有时，我们需要将数据保留在本地内存中，以在需要时快速可用。

1.  如果数据存储在键值对中的数据量相对较小。请考虑[使用共享首选项](https://zshipu.com/t?url=https://pub.dev/packages/shared_preferences)。下面是使用 Flutter 实现相同目标的详细指南。

[在磁盘上存储密钥值数据](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/persistence/key-value)

1.  您还可以在磁盘上读取和写入文件。

[读取和写入文件](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/persistence/reading-writing-files)

1.  <font _mstmutation="1" _msthash="485147" _msttexthash="243112077">如果应用需要保留大量数据，并且还需要查询它们。建议使用[SQLite 数据库](https://zshipu.com/t?url=https://www.sqlite.org/index.html)</font>

Flutter 应用程序可以使用 Sqlite 数据库通过[sqflite](https://zshipu.com/t?url=https://pub.dev/packages/sqflite)酒吧。

[使用 SQLite 保留数据](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/persistence/sqlite)

为了便于使用，反应性持久性，请查看酒吧下方。摩尔是围绕平方石的包装。

[moor_flutter |Flutter包装](https://zshipu.com/t?url=https://pub.dev/packages/moor_flutter)

## [](https://zshipu.com/t?url=#dependency-management)<font _mstmutation="1" _msthash="321867" _msttexthash="16859310">依赖性管理</font>

我们在应用程序中使用这么多的酒吧。这是跨应用进行集体工作和共享代码，而无需从头开始开发所有内容的一种有效方式。

你可以从这里找到所有有用的包。

[飞镖包](https://zshipu.com/t?url=https://pub.dev/)

使用多个酒吧时，您可能会面临版本解析中的冲突等问题。您可以在使用酒吧时在这里找到所有要遵循的最佳实践。

[使用包](https://zshipu.com/t?url=https://flutter.dev/docs/development/packages-and-plugins/using-packages)

而且，有了这一切，您现在已经完成了 Flutter 食谱。👏

# [](https://zshipu.com/t?url=#an-art-of-state-management)<font _mstmutation="1" _msthash="323869" _msttexthash="26045851">国家管理的艺术</font>

### [](https://zshipu.com/t?url=#introduction)<font _mstmutation="1" _msthash="321802" _msttexthash="5211505">介绍</font>

在典型的应用中，在 Point-A 所做的更改反映了 Point-B 的一些更改的常见用例。这就是所谓的状态管理。也可以通过下图理解。

[![Alt text of image](https://i.giphy.com/media/TFIZ2EBWVGHt59txzK/giphy.gif)](https://zshipu.com/t?url=https://i.giphy.com/media/TFIZ2EBWVGHt59txzK/giphy.gif)

Flutter 有多种方法可以有效地管理应用的状态。根据项目规模，我们可以决定适当的技术。

在这里，我们将讨论一些可能的国家管理技术。

1.  **设置状态方式**

[向 Flutter 应用添加交互性](https://zshipu.com/t?url=https://flutter.dev/docs/development/ui/interactive)

  [![Agung Surya](https://res.cloudinary.com/practicaldev/image/fetch/s--_vEFXLJC--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://miro.medium.com/fit/c/96/96/0%2AgDdGMXvkmtAuZ7Ha.)](https://zshipu.com/t?url=https://medium.com/@agungsurya/basic-state-management-in-google-flutter-6ee73608f96d)  [## 谷歌飘飘的基本状态管理 |由阿贡苏里亚 »中等

### <font _mstmutation="1" _msthash="872781" _msttexthash="81313999">Agung Surya • 2018年7月23日~ 4分钟 阅读</font>
 ![Medium Logo](https://res.cloudinary.com/practicaldev/image/fetch/s--KBvj_QRD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://practicaldev-herokuapp-com.freetls.fastly.net/assets/medium_icon-90d5232a5da2369849f285fa499c8005e750a788fdbf34f5844d5f2201aae736.svg)<font _mstmutation="1" _msthash="1167712" _msttexthash="5103527">中等</font>](https://zshipu.com/t?url=https://medium.com/@agungsurya/basic-state-management-in-google-flutter-6ee73608f96d) 

1.  继承的小部件

查看以下视频以了解**"什么是继承小部件？"**

此外，请查看此处的完整文章列表。

[状态管理方法列表](https://zshipu.com/t?url=https://flutter.dev/docs/development/data-and-backend/state-mgmt/options#inheritedwidget--inheritedmodel)

### [](https://zshipu.com/t?url=#remember-themeofcontext-and-navigatorofcontext-you-used-earlier-that-is-using-the-same-inherited-widget-concept-to-access-data-down-in-the-widget%C2%A0tree)_还记得你之前用过的 "主题 "（上下文）;" 和 "导航器" 吗？这是使用相同的继承小部件概念来访问小部件树中的数据。_

1.  提供程序包

提供程序[是](https://zshipu.com/t?url=https://pub.dev/packages/provider)DI（依赖注入）和状态管理的混合体，这些管理是使用小部件构建的。

提供商的官方文档太好，无法理解它。

[提供程序 - 飞镖 API 文档](https://zshipu.com/t?url=https://pub.dev/documentation/provider/latest/)

1.  BLOC 模式

[BLoC](https://zshipu.com/t?url=https://bloclibrary.dev/#/)是 Dart 的简单、轻量级和高度可测试的可预测状态管理库。

这里是一个官方指南：[集团](https://zshipu.com/t?url=https://bloclibrary.dev/#/)

<font _mstmutation="1" _msthash="305592" _msttexthash="232293360">我还发现了这个良好的视频系列解释 Bloc 模式 （[与附带的文章系列](https://zshipu.com/t?url=https://resocoder.com/2019/10/26/flutter-bloc-library-tutorial-1-0-0-stable-reactive-state-management/)</font>)

> _业内还有其他流行的国家管理技术。像[雷杜克斯](https://zshipu.com/t?url=https://flutter.dev/docs/development/data-and-backend/state-mgmt/options#redux)[和莫比克斯](https://zshipu.com/t?url=https://flutter.dev/docs/development/data-and-backend/state-mgmt/options#mobx)。_

## [](https://zshipu.com/t?url=#testing)<font _mstmutation="1" _msthash="320633" _msttexthash="6268977">测试</font>

当应用程序增长时，很难测试每个功能，然后它出现回归。在这种情况下，自动化测试是要走的路。它有助于确保应用在发布之前按预期执行。
因此，我们不会陷入这种境地。😆

[![](https://i.giphy.com/media/de5bARu0SsXiU/giphy.gif)](https://zshipu.com/t?url=https://i.giphy.com/media/de5bARu0SsXiU/giphy.gif)

自动化测试分为三类

*   单元_[测试](https://zshipu.com/t?url=https://flutter.dev/docs/testing#unit-tests)_测试单个函数、方法或类。

*   *[小部件测试](https://zshipu.com/t?url=https://flutter.dev/docs/testing#widget-tests)（在其他 UI 框架中称为组件测试）测试单个小部件。

*   *[集成测试](https://zshipu.com/t?url=https://flutter.dev/docs/testing#integration-tests)测试完整的应用或应用的很大一部分。

在此处查看 Flutter 中的测试简介

[测试 Flutter 应用程序](https://zshipu.com/t?url=https://flutter.dev/docs/testing)

## [](https://zshipu.com/t?url=#unit-testing)<font _mstmutation="1" _msthash="319969" _msttexthash="12031968">单元测试</font>

单元测试的目标是使用 Stub/mock 依赖项测试特定的代码单元。验证代码在不同方案中是否正常工作。单元测试非常快，不需要实际设备执行。

[单元测试简介](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/testing/unit/introduction)

在执行 Unit 测试时，任何依赖类都应可注入，以便我们可以注入依赖的模拟或假实现，并验证是否一切正常。Flutter 具有一[个模拟](https://zshipu.com/t?url=https://pub.dev/packages/mockito)框架，可帮助创建模拟或假实现。

[模拟飞镖包](https://zshipu.com/t?url=https://pub.dev/packages/mockito)

## [](https://zshipu.com/t?url=#widget-testing)<font _mstmutation="1" _msthash="321594" _msttexthash="17123860">小部件测试</font>

小部件测试（在 Flutter 中）是一种 UI 测试技术。
小部件测试的目标是测试特定的小部件 UI 是否看起来与预期一样，并且它是交互式的。小部件测试不需要物理设备。

我们还可以测试小部件的属性，如颜色、大小、字体系列等。
我们还可以执行用户事件，如点击、手势、输入文本等。

[小部件测试简介](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/testing/widget/introduction)

## [](https://zshipu.com/t?url=#integration-testing)<font _mstmutation="1" _msthash="319956" _msttexthash="14050387">集成测试</font>

集成测试工作成对。这里的目标是测试多个单元如何协同工作。集成测试发生在真正的设备或仿真器上。

我们可以发射一系列用户交互事件，并期望正确执行 UI 呈现或单元代码。

[集成测试简介](https://zshipu.com/t?url=https://flutter.dev/docs/cookbook/testing/integration/introduction)

## [](https://zshipu.com/t?url=#bdd-behaviordriven-development)<font _mstmutation="1" _msthash="321581" _msttexthash="41328001">BDD：行为驱动型开发</font>

当利益相关者具有很强的技术技能时，TDD 或单元测试会有所帮助。BDD 就是从最终用户的角度编写测试用例。这是用自然的英语写的。

测试用例可以以以下格式
**编写：给定**：场景开头的初始上下文，在一个或多个子句中;
**当**： 触发方案的事件;
**然后**：预期结果，在一个或多个子句中。

在内部，行为测试用例可以是单元测试、小部件测试或两者的组合。

BDD 有助于从最终用户的角度理解软件功能，并成为一种功能文档。

Flutter 有一[个 gherkin，](https://zshipu.com/t?url=https://cucumber.io/docs/bdd/better-gherkin/)帮助我们编写行为测试用例。

[盖尔金 |飞镖包](https://zshipu.com/t?url=https://pub.dev/packages/gherkin)

* * *

本指南涵盖了所有基础知识，您需要知道，从Flutter开始，开发您的应用程序！我们希望这有助于你的旅程飘飘。
