
title: Web技术：Web个人站点加载极速优化
author: 知识铺
date: 2020-09-20 18:33:51
tags: 
---
 我这个周末的项目是加快我的个人[网站](https://zshipu.com/t?url=https://alvinlim.me/)。我决定在谷歌灯塔上成绩不及格后，就[决定为此工作](https://zshipu.com/t?url=https://developers.google.com/web/tools/lighthouse)。经过一系列急需的优化后，网站现在加载速度明显加快，其灯塔分数也大为提高：



我现在将分享我实现的关键优化，加速了我的网站：

**优化图像**

我网站的早期版本有一个3MBJPEG文件，我用作完整的背景图像。我想保持相同的外观，这意味着我不得不用比JPEG更好的压缩格式替换这个图像。我考虑过新的[AVIF 格式](https://zshipu.com/t?url=https://jakearchibald.com/2020/avif-has-landed/)， 但不幸的是， 它目前没有很好地支持：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--AyBpPjOt--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fb7ugi60nurfu3mjmagy.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--AyBpPjOt--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fb7ugi60nurfu3mjmagy.png)

因此，我选择将现有的 JPEG 和 PNG 图像替换为 WebP 图像，因为 WebP 格式更受支持：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--RPIR1w2l--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6l4updzlspftobfd1lkn.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--RPIR1w2l--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6l4updzlspftobfd1lkn.png)

除了更改图像格式，我还确保在我的网站中使用的图像是完全相同的尺寸，因为他们将在屏幕上显示。

例如，我以前使用的肖像图像的尺寸比网站上显示的 200x200 小圆形图像大得多。这不仅意味着宝贵的毫秒将被浪费下载这个不必要的大文件，浏览器也会浪费时间调整图像的大小。通过部署正确尺寸的图像，将保存毫秒。

**删除不必要的 JavaScript**

除了需要优化我的图像，灯塔还表示，我可以通过删除不必要的JavaScript脚本进一步优化我的网站。我有3个JS脚本在我的网站上运行 - 一个虚拟选项卡生成器;谷歌分析脚本;和谷歌 Recaptcha 脚本。

我决定保持虚拟选项卡生成器，因为我喜欢它如何增强我的网站。我决定删除谷歌分析脚本，因为我意识到，我不需要它，因为我没有使用我的个人网站的功能，如电子商务。

我同样选择从我的 FormSpree 联系人表单中删除[Google ReCaptcha 脚本](https://zshipu.com/t?url=https://formspree.io/)，并调整了表单的设置，以使用在 FormSpree 上托管的 ReCaptcha 功能。删除这些第三方 JavaScript 脚本可显著缩短浏览器加载和呈现网站的时间。

**转储 CDN**

在优化之前，我的网站使用3个CDN-[谷歌字体](https://zshipu.com/t?url=https://fonts.google.com/)[，字体真棒](https://zshipu.com/t?url=https://fontawesome.com/)，[和引导](https://zshipu.com/t?url=https://getbootstrap.com/)。用本地托管资产替换这些资产可显著节省时间。

_谷歌字体_

<font _mstmutation="1" _msthash="292409" _msttexthash="1395929301">为了取代使用谷歌字体CDN，我下载了我需要的字体，并使用[字体松鼠](https://zshipu.com/t?url=https://www.fontsquirrel.com/tools/webfont-generator)将它们转换为网络字体。然后，我移动 woff2 字体文件到我在网站项目目录中创建的文件夹，并在我的 CSS 文件中声明它们。</font>```fonts```

<font _mstmutation="1" _msthash="292708" _msttexthash="562255018">例如，我在我的网站中使用的谷歌字体之一[是正义。](https://zshipu.com/t?url=https://fonts.google.com/specimen/Righteous?query=righteous)我通过声明您的面部（包括位置）@font将它导入到 CSS 文件中：</font>

 <code>@font-face {
  font-family: "Righteous";
  src: url(fonts/righteous-regular-webfont.woff2);
  font-display: swap;
}</code> 

<font _mstmutation="1" _msthash="290602" _msttexthash="174315843">并在相应的 CSS 组件中使用，在这种情况下，横幅：</font>

 <code>.banner h1 {
  ...
  font-family: "Righteous", cursive;
  ...
}</code> 

_字体真棒_

在优化之前，我的网站依靠[字体真棒](https://zshipu.com/t?url=https://fontawesome.com/)，以获得LinkedIn，谷歌和GitHub图标在页脚使用。为了优化这一点，我[切换到Fonastic，](https://zshipu.com/t?url=http://fontastic.me/)它允许我下载这些图标作为一个单一的字体文件，我可以在本地托管。（当您下载此字体文件时，Fontastic 将为您提供适当的 CSS 和 HTML 代码段，以插入代码以显示图标。

_引导_

我以前在我的网站上包括了 Bootstrap 来调整其布局，但我决定，这个好处并没有证明成本用于从其 CDN 下载 Bootstrap 和在浏览器中呈现 Bootstrap 类的时间。删除引导后，我发现我只需要花一点时间来调整HTML和CSS，以获得我想要的外观。

**速度更快的网站**

这些优化早就应该了，除了我的网站从灯塔获得的分数更高，好处可以在一个明显更快的网站感受到。我还测试了我的网站在HubSpot[的网站分级](https://zshipu.com/t?url=https://website.grader.com/)器，这给它一个更高的成绩比它收到的优化之前：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--KDqx3LtN--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/55n16ne96duo7f4sug8a.jpg)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--KDqx3LtN--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/55n16ne96duo7f4sug8a.jpg)
