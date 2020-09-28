
title: web网站：优化网站速度的 8 个提示
author: 知识铺
date: 2020-09-17 14:36:02
tags: web
---
 您是否考虑过网站的性能、内容加载速度以及网页的响应时间？

当为真实用户构建任何产品时，所有这些事情都应该是您的首要任务。

即使网站延迟一到两秒钟，也会极大地影响用户体验和网站流量。
考虑任何大公司，如亚马逊或优步，只是1秒的延迟在他们的网站上可以让他们失去成百上千的客户，一个相当大的数字我知道。现在尝试对您的网站或应用应用相同的应用。

只要处理一些事项并遵循一些最佳实践，您就可以使您的网站更快，您将看到产品性能的显著改善。

现在，让我们看看这些小细节，你可以专注于提高您的网站的性能是什么。

### [](#1-optimize-your-media-files-size-and-format)<font _mstmutation="1" _msthash="290225" _msttexthash="46088822">1\. 优化媒体文件大小和格式</font>

<font _mstmutation="1" _msthash="277381" _msttexthash="1566167837">我们都把图像和媒体文件在我们的页面，使其更有吸引力，但图像和gif文件，你放在您的网站必须下载浏览器显示给你的用户，所以如果你把大尺寸**的图像在你的网站上，它肯定会使您的网站慢。**</font>

因此，建议使用一些外部图片工具来调整图像的大小，并在不降低文件质量的情况下减小图像的大小。对于页面的优化加载时间，最好坚持使用某些标准文件格式，如 jpg、png 等图像格式。

此外，不要试图使用图像来显示一些文本内容;更喜欢使用文本代替， 因为图像将增加不必要的加载时间， 甚至不会帮助在 Seo 。

这些工具可以帮助您实现以下目标：

*   [https://compressor.io/](https://zshipu.com/t?url=https://compressor.io/)
*   [https://github.com/google/brotli](https://zshipu.com/t?url=https://github.com/google/brotli)
*   [https://tinypng.com/](https://zshipu.com/t?url=https://tinypng.com/)
*   [https://www.gimp.org/](https://zshipu.com/t?url=https://www.gimp.org/)

### [](#2-avoid-using-inline-js-and-css-files)<font _mstmutation="1" _msthash="304330" _msttexthash="41887365">2\. 避免使用内联 JS 和 CSS 文件</font>

在外部文件中为您的网站编写 JS 和 CSS 代码是一个很好的做法。不仅外部文件更易于维护，而且浏览器也会缓存它们，以节省进一步加载的时间。

如果在单独的 CSS 和 JS 文件中定义所有内容，浏览器将发现更轻松地将样式和功能应用于页面。

### [](#3-write-cleaner-html)<font _mstmutation="1" _msthash="305266" _msttexthash="25536615">3\. 编写更简洁的 HTML</font>

大多数时候，我们的作用是在我们的页面上添加不必要的 HTML，并在 CSS 快速实现相同效果时，用不同类型的标题、强和斜体标记填充它。因此，不要把大量的代码放在HTML文件上，而是尽量保持简单**，使用CSS**替代方法，这样你的页面会更简洁，加载起来也更舒服。但它的成本是，一些旧的浏览器可能不支持一些CSS属性，所以请确保您照顾所有浏览器，而编写CSS。

### [](#4-load-javascript-files-asynchronously-or-at-the-end-of-the-page)<font _mstmutation="1" _msthash="305890" _msttexthash="92170754">4\. 异步加载 JavaScript 文件或在页面末尾</font>

在正文标记关闭之前将脚本标记放在一起，以便加载网页的整个内容部分后加载 javascript 文件始终是一种好的做法。或者，如果要将这些放在正文上方，请确保在**脚本标记中放入"延迟"属性**，以确保在加载完所有内容后加载文件。它允许浏览器在开始使用 JS 之前呈现所有内容。

此外，您可以使用异步 javascript，以便它与内容并行加载，并且不会干扰网站的流。Ajax 可以帮助您实现此目的，以便我们可以更新该页面的某些部分，而不是在用户操作时重新加载整个页面。您还可以在脚本标记上设置异步属性以异步方式加载文件。

### [](#5-utilizing-the-browser-caching-feature)<font _mstmutation="1" _msthash="304005" _msttexthash="41789280">5\. 利用浏览器缓存功能</font>

网站上的许多文件不会经常随着时间而变化
，Web 缓存是 Web 浏览器缓存文件供以后使用时，这样当用户重新访问您的网站时，浏览器就不必从头开始加载所有内容。浏览器可以缓存的内容包括 CSS 文件、JavaScript 文件和图像。

因此，请确保创建一个网站，充分利用缓存功能、本地存储、cookies 和服务器缓存。

这大大缩短了服务器响应时间，用户可以一次又一次地访问您的网站，并且每次都会改善用户体验。

如果您想详细了解如何利用浏览器缓存，请查看这些文章。

*   [https://betterexplained.com/articles](https://zshipu.com/t?url=https://betterexplained.com/articles/how-to-optimize-your-site-with-http-caching/)
*   [https://www.codebyamir.com/blog](https://zshipu.com/t?url=https://www.codebyamir.com/blog/a-web-developers-guide-to-browser-caching)
*   [https://varvy.com/pagespeed](https://zshipu.com/t?url=https://varvy.com/pagespeed/leverage-browser-caching.html)

### [](#6-minify-and-combine-your-files)<font _mstmutation="1" _msthash="305877" _msttexthash="87035572">6\. 放大缩小字体功能 放大缩小字体功能</font>

您放在页面上的所有文件必须由浏览器下载才能呈现，因此通过**减少文件数量，您会自动使渲染速度更快。**考虑页面上的 Html、CSS 和 JavaScript 文件的数量。它们都会增加网站每次用户访问您的网页时发出的请求数。

您可以通过"缩小"和合并文件来减少此数字。明化文件可减小每个文件的大小，合并文件可减少文件数。

分明文件涉及删除不必要的格式、空白和代码。有很多在线工具可以帮助您实现结果。每个不必要的代码都会增加页面的大小，因此使用最小文件加载页面至关重要。这可确保您的页面尽可能干净。

如果您的网站使用多个 CSS 和 JavaScript 文件，您可以将它们合并为一个文件并实现相同的结果。

如果您想优化文件，请查看这些出色的工具：

*   我强烈建议使用[Gulp](https://zshipu.com/t?url=https://gulpjs.com/)来最小化和优化您的文件， 所以请检查出来。
*   [宇一压缩机](https://zshipu.com/t?url=https://yui.github.io/yuicompressor/)
*   [乌格利菲斯](https://zshipu.com/t?url=https://github.com/mishoo/UglifyJS)
*   [cssnano](https://zshipu.com/t?url=https://github.com/cssnano/cssnano)

### [](#7-using-the-right-hosting-option-and-service-for-your-product)<font _mstmutation="1" _msthash="305240" _msttexthash="103153596">7\. 为您的产品使用正确的托管选项和服务</font>

当你为自己做项目或演示的目的，这是好去免费的托管选项，而不是支付域名和托管服务。不过，一旦你开始为现实世界开发吸引大量流量的应用程序，最好转到良好的付费托管服务，而不是选择最便宜的选择。阅读不同平台的评论，并选择最适合您需求的平台。

一些流行的托管服务是：

*   蓝主机
*   主机云
*   梦想主机
*   戈达迪主机
*   站点地面

### [](#8-use-an-online-tool-like-lighthouse)<font _mstmutation="1" _msthash="306488" _msttexthash="39263757">8\. 使用灯塔等在线工具</font>

网站完成后，您可以在线使用任何页面速度分析工具。如果你正在使用铬，那么有一个灯塔**工具存在于铬**开发工具，它给你分析你的网页性能，也提供了一些提示，你可以提高你的网页的性能，所以给它一个尝试。

就是这样。这些都是一些最佳实践，如果你开始使用你的网页，将执行好得多。

* * *

