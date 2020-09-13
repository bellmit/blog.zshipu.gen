
title: 从零开始 - 第 2 部分 - SVG 魔术在 Flutter
author: 知识铺
date: 2020-09-13 19:04:53
tags: flutter
---
  

* * *

## 内容

*   [绘制饼干](#drawing-the-cookie)
*   [在 Flutter 中绘制 SVG](#drawing-svgs-in-flutter)
*   [预加载 SVG](#preload-svgs)
*   [动态更新 SVG](#updating-svgs-dynamically)
*   [得分](#scoring)
    *   [提取参考线路径](#extracting-guide-paths)
    *   [时间复杂性和 k-d 树](#time-complexity-and-k-d-trees)
    *   [计算分数](#calculating-the-score)


![](https://d33wubrfki0l68.cloudfront.net/abc4a24476856b318c5fbca77a47499f59a3f978/6f020/images/posts/2020-05-01/app.jpg)

好吧， 所以我的游戏的前提是你有饼干， 你可以装饰。在游戏模式下，你遵循"引导路径"，并获得点，你有多接近。

查看右侧的图像。

问题是结冰是粘的。它并不完全跟随你的手指， 你需要把它塑造成到位 （深入到该算法即将推出） 。

## 绘制饼干

因此，首先我必须画一个cookie，但我希望文件格式满足以下：

*   直观地显示 Cookie（很明显）
*   包含用户尝试匹配的引导路径数据
*   可扩展到任何屏幕大小

如果我使用普通映像，则它不可伸缩，并且无法存储参考线路径数据。那我能做什么？SVG 到救援！😎

[如果您不熟悉，请阅读 SVG](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/Scalable_Vector_Graphics)在此处的是什么;但本质上，_他们描述_如何绘制图像，而不是只是存储图像像[JPG](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/JPEG)或[PNG。](Portable_Network_Graphics)

它们也是XML文件，这意味着它们通常很小，可以存储任何你想要的数据！

以下是我的一个 Cookie 的基本 SVG 结构。

``` 
 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
    <path class="shadow" d="..." opacity="0.1" />
    <path class="edge" d="..." fill="#edc78d" />
    <path class="base" d="..." fill="#fad294" />
    <path class="target" d="..." fill="none" stroke="#a2824c" stroke-dasharray="20" stroke-linecap="round" stroke-linejoin="round" stroke-width="8" />
    ...
</svg>
``` 

![](https://d33wubrfki0l68.cloudfront.net/173b8ded6b27a61fdc0184c5f83160a976ab821c/03eaf/images/posts/2020-05-29/cookie.jpg)

因此，此文件不仅绘制 Cookie 本身，我可以在运行时执行很酷的事情，如：

*   更改元素的值。曲奇颜色现在可以动态了！
*   显示/隐藏元素。我可以在"zen 模式"中隐藏引导路径。
*   提取指南路径数据，我用于对路径的跟踪进行评分。

上图显示了一个示例 Cookie，该示例具有用户遵循的参考路径。

## 在 Flutter 中绘制 SVG

因此，要在 Flutter 中绘制 SVG，[请使用flutter_svg](https://zshipu.com/t?url=https://pub.dev/packages/flutter_svg)包。从文件渲染一个简单的 SVG，像这样：

``` 
 import 'package:flutter_svg/svg.dart';

class MyWidget extends StatelessWidget {
    Widget build(BuildContext context) {
        return SvgPicture.asset("path/to/svg/asset");
    }
}
``` 

<font _mstmutation="1" _msthash="425854" _msttexthash="151837881">确保使用要使用的资产（文件或文件夹）更新文件。</font>```pubspec.yaml```

``` 
 assets:
- path/to/svg/assets/
``` 

## 预加载 SVG

有时，复杂的 SVG 可能需要时间来加载。当库收到 SVG 来呈现它时，它必须从磁盘读取文件，解析所有信息，然后动态呈现它。

结果是，有时 SVG 会闪烁到屏幕上后，其他一切加载。这发生在我的教程页面上， 玷污了经验。没有人想要内容跳来跳去。

那么，我们如何防止这种情况呢？预 压！

值得庆幸的是，SVG 库缓存 SVG，以便未来的渲染速度非常快。

下面是一个有用的函数，我用于预加载它们：

``` 
 import 'package:flutter_svg/flutter_svg.dart';

Future<SvgPicture> loadSvg(BuildContext context, String path) async {
  var picture = SvgPicture.asset(path);
  await precachePicture(picture.pictureProvider, context);
  return picture;
}
``` 

例如，我在输入教程屏幕之前使用此选项。我从主页预加载前几个 SVG，然后在用户启动教程后加载其余内容。结果是一个快速的体验。

<font _mstmutation="1" _msthash="426218" _msttexthash="73310783">使用以下功能启动一些预加载：</font>```Future.wait()```

``` 
 Future.wait([
    loadSvg(context, "svg_1.svg"),
    loadSvg(context, "svg_2.svg"),
    ...
]);
``` 

## 动态更新 SVG

好的， 所以我们可以渲染一个 Svg， 但我们如何可以操纵他们飞行？我[进入flutter_svg代码](https://zshipu.com/t?url=https://pub.dev/packages/flutter_svg)， 自己弄清楚这一点。

查看视频， 看到我动态更新各种 Svg， 如：

*   大饼干和饼干按钮的颜色
*   引导路径的显示/隐藏
*   左下角按钮的描边厚度
*   左下角按钮的描边和填充颜色

为了达到这个目的，我劫持了SVG解码过程，如下所示：

*   我包装SVG字符串转换函数
*   我使用原始 SVG 字符串，并解析为 XML 对象
*   纵 XML 来施展我的魔法（比如更新颜色）
*   我创建一个独特的哈希， 封装我做了操作
*   我将 XML 转换为字符串，然后将字符串 + 哈希发送回我包装的原始函数

我在这里[创建了一个要点，](https://zshipu.com/t?url=https://gist.github.com/kangabru/aedf632fbe5991141398e760001c2a3f)它这样做 （需要[xml](https://zshipu.com/t?url=https://pub.dev/packages/xml)包） 。

以下是我如何在我的一个按钮中使用它， 它动态地更改 SVG 颜色：

``` 
 class ZenButtonCookie extends StatelessWidget {
  final CookieColor color; // My internal color object. Adapt this for your needs.
  const ZenButtonCookie(this.color);

  @override
  Widget build(BuildContext context) {
    return SvgOverride(
      "path/to/svg.svg",
      hash(path, color),
      (elem) => processElement(elem, color),
    );
  }

  // Ensure the hash uniquely identifies the transformations you will do
  static hash(String svgPath, CookieColor color) => hashValues(svgPath, color?.base, color?.edge);

  // Do manipulation magic here
  static processElement(XmlElement elem, CookieColor color) {
    var setAttr = SvgOverride.setAttr;
    var getHex = SvgOverride.getHex;

    switch (elem.getAttribute('class')) {
      case 'base':
        setAttr(elem, "fill", getHex(color?.base));
        break;
      case 'edge':
        setAttr(elem, "fill", getHex(color?.edge));
        break;
    }
  }
}
``` 

这里的哈希很重要。如果我们仅按文件名缓存，则库不会重新呈现更改，因为我们进行更改（因为返回了旧的 SVG）。

如果我们提供随机哈希，则 SVG_将始终_在屏幕更新时重新呈现。这可能像我上面解释的一样慢。

无论如何，现在你可以更新SVG，因为它的渲染！因此，当您更改输入时（例如，当您更新颜色时）SVG_会更新_并正确缓存。

## 得分

![](https://d33wubrfki0l68.cloudfront.net/efb80f5a36d2316afdcffa6f8a72cdac1317d3ea/e136a/images/posts/2020-05-29/score.jpg)

这一节有点偏离主要主题，但我认为它仍然很有趣。

### 提取参考线路径

就像我之前说过的，我希望我的 SVG 包含用于评分的引导路径数据。

我已经向您展示了如何呈现参考线路径（当然，这只是一个 SVG 元素），但现在我将展示如何提取该数据进行评分计算。

<font _mstmutation="1" _msthash="427323" _msttexthash="276759249">我需要做的只是从 Cookie SVG 文件（具有 类的元素）中提取引导路径元素。</font>```target```

首先，我从磁盘读取 SVG 文件作为字符串，如下：

``` 
 import 'package:flutter/services.dart';

Future<String> readFile(String filePath, {isTest: false}) async {
    return isTest
        ? new File(filePath).readAsString()
        : rootBundle.loadString(filePath);
}
``` 

我转换为 XML 并筛选出指南路径元素（需要[xml](https://zshipu.com/t?url=https://pub.dev/packages/xml)包）。

``` 
 import 'package:xml/xml.dart';

// How I read SVG files
Future<XmlDocument> readSvg(String filePath, {isTest: false}) async {
  var content = await readFile(filePath, isTest: isTest);
  var xmlRoot = parse(content);
  return xmlRoot;
}

// How I filter out specific elements
Iterable<XmlElement> getXmlWithClass(XmlDocument root, String classId) {
  return root.descendants
      .whereType<XmlElement>()
      .where((p) => p.getAttribute('class') == classId)
      .toList();
}
``` 

<font _mstmutation="1" _msthash="429208" _msttexthash="222207908">现在，我可以提取引导路径元素，我必须将它们转换为实际对象。</font>```Path```

好消息是 SVG 库在幕后这样做。坏消息是，它不暴露这些方法。

<font _mstmutation="1" _msthash="429962" _msttexthash="140084672">我最终将[此文件复制到](https://zshipu.com/t?url=https://github.com/dnfield/flutter_svg/blob/master/lib/src/svg/parser_state.dart)公开函数的项目中。完美！</font>```xmlToPath```

<font _mstmutation="1" _msthash="426933" _msttexthash="622921377">评分前的最后一步是将对象转换为坐标（对象）列表。我们基本上沿着路径走，具有一定的步进大小，像这样：</font>```Path``````Offset```

``` 
 /// Convert a path into a list of offsets.
List<Offset> pathToCoords(Path path, [double pixelGap = 2]) {
    var metrics = path.computeMetrics();
    if (metrics.length == 0) return [];

    var coords = <Offset>[]
    var metric = path.computeMetrics().first;

    double position = 0;
    while (position < metric.length) {
        var tangent = metric.getTangentForOffset(position);
        coords.add(tangent.position);
        position += pixelGap;
    }

    return coords;
}
``` 

唷！在我们甚至可以开始实际得分位之前， 这是很多工作要做。

### 时间复杂性和 k-d 树

此时，我有"引导路径"和用户的"绘制路径"。要计算分数，我必须比较它们。容易吧？

那么，这些路径可以有很多坐标，每个，和蛮力解将让我比较一个路径的每一个点与每一个点。这是超慢， 所以我需要一个更好的方法。

<font _mstmutation="1" _msthash="429195" _msttexthash="357566170">我的解决方案是为每条路径[建立一个 k-d](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/K-d_tree)树并进行比较。这将解决方案归结为 。快得多！</font>```n^2``````n log(n)```

我[使用此包](https://zshipu.com/t?url=https://pub.dev/packages/kdtree)来完成这项工作。使用有点尴尬， 但完成工作。

要让您了解我保存的操作数，请说每个路径都有一个适度的 100 坐标。

<font _mstmutation="1" _msthash="430326" _msttexthash="79074723">在蛮力比较时，将计算操作总计。</font>```n^2``````100 x 100``````10,000```

<font _mstmutation="1" _msthash="427297" _msttexthash="1056566043">k-d 树插入并随着时间的推移进行搜索。正如你会看到在一分钟内，我必须建立2棵树，然后搜索每棵树对对方。这意味着我做4个操作，总共计算。节省 70%！</font>```log(n)``````n log(n)``````3000```

<font _mstmutation="1" _msthash="427674" _msttexthash="312078468">如果我们将每个坐标扩展到 1000 个坐标，则这些数字将分别到达和到达。节省 96% ！</font>```1,000,000``````40,000```

当然，这些数字不是确切的数字，但它们让您了解优化的速度和可扩展性。

### 计算分数

终于可以得分了！我所做的是从这两个操作的最大距离：

*   将参考路径的每个点与绘制的路径树进行比较
*   将绘制路径的每个点与参考路径树进行比较

低距离 = 路径更近 = 分数越高！


* * *
