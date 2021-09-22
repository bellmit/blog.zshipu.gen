
---
title: 为什么你应该先学习 JavaScript 原理 （不是最热门的框架）
author: 知识铺
date: 2021-02-25 20:24:15+08:00
tags: []
---

# [](#no-winners-in-the-crazy-frameworks-race)<font _mstmutation="1" _msthash="288483" _msttexthash="48696115">疯狂框架竞赛中无优胜者</font>

在过去的五年里，我一直在疯狂地追逐JavaScript图书馆和框架之间最热门的比赛。也许在某个时候，我们都问自己，我们应该学习哪个Javascript框架，评估利弊，为什么，为什么，等等。我一直是那场比赛的受害者， 也许你也是。当然，我不知道这是否发生在你身上，但我一直在疯狂地追逐最热门的Javascript框架或图书馆，寻找趋势，比较，如何学习它们，因为业界要求他们。
这场疯狂的比赛根本没有赢家，因为它永无止境。就是这样！昨天你正在学习骨干.js，jQuery，挖空.js，琥珀.js，然后角JS，现在ReactJS，下一个.js，Vue.js，所有角的味道。今天， 出现了 Ext Js 和奥雷利亚， 新的。明天还会有另一个出现。框架阵列列表是无穷无尽的。

请，请，请不要急于学习。不要追逐最热门的新 JavaScript 框架或库。首先，将宝贵的时间投入到理解和关注引擎上：核心概念和 Javascript 原则。我们将在这篇文章中讨论它，我会给你一些理由，钥匙和资源，以帮助您获得掌握的JS知识。

# [](#so-i-shouldnt-learn-a-js-framework)<font _mstmutation="1" _msthash="289380" _msttexthash="54854774">所以我不应该学习JS框架？</font>

不，不，我不是这么说的事实上，你应该学习它们——但是不要把宝贵的时间浪费在他们身上。我的意思是时间有限，我们应该明智地投资于真正重要的事情。我知道有一个坚持的诱惑，学习更现代的工具，框架，图书馆，其中一些上面列出。这是因为全世界——你的同事、论坛、平台、你关注的社区——都在吹嘘他们拥有的新酷的东西，以及你能多么容易地实现你的发展目标。你试过吗？我想你们不止一个人有过这种诱惑， 并且已经倒下了。我理解为什么会这样。作为开发人员，我们需要跟上技术的最新发展。

我应该认识到，几年前我被这种诱惑带走了。请记住，框架的目的是让您真正加快发展历程，获得速度。它负责复杂性和抽象性，为您提供一条加快编码过程的捷径。但这并不意味着你会掌握并成为一个强大，知识渊博的JS开发人员。这意味着你会知道该怎么做， 但不是为什么或如何工作的东西在引擎盖下。
我也知道，就像生活中的一切一样，我的观点也会有诋毁者和恋人。这篇文章只是一个指南，一条建议。它基于我的个人经验和大量的投诉，我在编程讨论平台上看到LinkedIn，雷迪特，Dev.to，媒体，Facebook群组等。

# [](#what-happens-if-you-dont-understand-how-javascript-works)<font _mstmutation="1" _msthash="290277" _msttexthash="137529990">如果你不明白 JavaScript 是如何工作的， 会发生什么</font>

也许你很清楚你最喜欢的JS框架。但是，没有谎言，有一些日子，事情变得黑暗，因为意想不到的行为，错误和例外开始出现。作为我的队友，索哈姆说，"这真是一件疯狂的事！嘿！休斯顿，我们有一个问题——有些事情并不像我们预期的那样有效！是时候花很多时间搜索， 搜索纯粹的 JavaScript 代码， 试图找出为什么这种奇怪的行为正在发生。因此，您开始挖掘，您在酷框架中保存的学习时间将开始减少。以下是对 JS 的可靠理解将节省您的一天的时间。否则，你会感到压力很大，在理解它发生的原因方面没有任何成功。

# [](#what-really-matters-the-javascript-core-concepts-and-principles)<font _mstmutation="1" _msthash="303160" _msttexthash="129378522">什么才是真正重要的？JavaScript核心概念和原则</font>

为了读一本好书，我将只触及一些核心概念。其余的，我只是列出，这样你就可以记住他们。在我的下一件作品中，我们将深入了解它们中的每一个包裹的内容。

### [](#javascript-engine-execution-context-and-call-stack)<font _mstmutation="1" _msthash="304330" _msttexthash="90607777">JavaScript 引擎、执行上下文和呼叫堆栈</font>

这篇文章的主要目的之一是引导你到真正重要的东西，核心JavaScript的概念，原则和基本原理。当我谈论基本面时，我不只是在谈论了解它的语法、变量、数据类型、循环和功能。我真的在谈论那个，再加上更复杂的概念。因此，我们应该开始学习的第一件事是 JavaScript 引擎的工作原理、执行的步骤、列克星的含义、解析、代码生成阶段以及执行上下文是什么（包括其类型，以及如何以及何时创建执行上下文）。

### [](#scope)<font _mstmutation="1" _msthash="304954" _msttexthash="5367089">范围</font>

以上只是核心概念的一小部分， 我们需要感到舒服， 说我们是 JavaScript 的主人。之后，我们应重点了解范围、全球范围、局部范围、功能和区块范围。了解不同类型的示波器的工作原理以及何时创建它们将允许您预测和确定给定场景中的输出。

### [](#closures)<font _mstmutation="1" _msthash="305578" _msttexthash="5702983">闭 包</font>

闭合只是能够记住其执行上下文的另一个函数内部的函数。这个概念是相当棘手的，即使对于经验丰富的和经验丰富的JS开发人员。长期以来，我一直试图全面掌握关闭的概念。看起来可能很容易，但并非易事。有时我们甚至不知道我们处于关闭的前面。如果您对关闭有良好的理解，您可以阅读和理解更复杂的代码。例如，您可以深入到您最喜爱的框架的源代码，并开始了解其代码。

### [](#an-array-list-of-more-javascript-core-concepts)<font _mstmutation="1" _msthash="306202" _msttexthash="79573962">更多 JavaScript 核心概念的阵列列表</font>

要开始，上述概念是伟大的。远不止这些。正如我以前向你承诺的那样，下一个概念将只考虑在心中。你应该能够理解 JavaScript 引擎如何对待异步， 因为， 如你所知， Js 是一个单线程编程语言。此外，我们需要熟悉和自信的其他核心概念包括原型、继承、回调、承诺、功能编程概念和功能组合。

#### [](#and-of-course-you-should-also-be-caught-up-on-the-latest-ecmascript-specifications-es6-es7-es8-es9-es10-esnext-and-beyond)<font _mstmutation="1" _msthash="304278" _msttexthash="232619465">当然，您也应该赶上最新的 ECMAScript 规格：ES6、ES7、ES8、ES9、ES10、ES.next...和超越。</font>

# [](#where-and-how-to-master-those-concepts)<font _mstmutation="1" _msthash="303771" _msttexthash="55476538">在哪里以及如何掌握这些概念</font>

在学习过程中
应用 80/20 规则这篇文章还旨在阻止您学习最热门的 JavaScript 框架，并敦促您保持冷静，学习 JavaScript 的核心概念。
正如我们以前讨论过的那样，新的框架和图书馆将随之而来，然后消失。这就是我们近年来所看到的。一个好的方法是建立一个良好的学习系统，如果你想赶上趋势。这就是所谓的 80/20 规则：投入并集中 80% 的时间学习核心概念，每天挖掘更多内容。然后将剩余的 20% 投资在最热、最酷的工具上。

您应该阅读以下资源，而不是担心 JS 框架/库的学习趋势。关于他们最重要的事情是，有些人是免费的！所以，没有更多的借口！

[清洁代码： 敏捷软件工艺](https://zshipu.com/t?url=https://www.amazon.com/gp/product/0132350882/?tag=mustr-20)
[手册实用程序员： 从旅行者到主](https://zshipu.com/t?url=https://www.amazon.com/gp/product/0132350882/?tag=mustr-20)
[编程 JavaScript 应用程序](https://zshipu.com/t?url=https://books.google.com.sv/books/about/Programming_JavaScript_Applications.html?id=jUfnAwAAQBAJ&source=kp_book_description&redir_esc=y)
[， 你还不知道 Js](https://zshipu.com/t?url=https://github.com/getify/You-Dont-Know-JS)
[JavaScript： 好部分](https://zshipu.com/t?url=https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)

# [](#reasons-to-learn-the-core-principles-of-javascript)<font _mstmutation="1" _msthash="305019" _msttexthash="57885334">学习JavaScript核心原则的理由</font>

#### [](#you-are-the-master-of-js)<font _mstmutation="1" _msthash="306150" _msttexthash="15457962">你是JS的主人</font>

如果你是JavaScript核心和基本原理的掌握者，学习一个新的框架将是你的一块蛋糕，因为你只需要学习它的语法和一些内部特征，你可以很容易地消化。如果您了解纯 JavaScript，则不需要可能不符合您长期目标的工具包。

#### [](#better-code)<font _mstmutation="1" _msthash="306774" _msttexthash="15349165">更好的代码</font>

如果您知道发动机的工作原理、如何预测函数在给定情况下的行为方式，或者示波器的工作原理，我敢说，当事情不能如预期的那样工作时，您将节省时间。此外，您创建更好、更高代码质量的可能性更大。

