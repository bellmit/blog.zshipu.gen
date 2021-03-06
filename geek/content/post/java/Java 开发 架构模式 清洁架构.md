---
title: Java 开发 架构模式 清洁架构
author: 知识铺
date: 2021-10-02 11:33:33
tags: [架构]
---


![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110021133649.jpg)



虽然这些架构的细节都有些不同，但它们非常相似。它们都有相同的目标，即解耦。它们都通过将软件划分为层来实现这种分离。每个层至少有一层用于业务规则，另一层用于接口。

这些架构中的每一个都产生以下系统：

1. 独立于框架。架构并不依赖于一些充满功能的软件库的存在。这允许您使用工具等框架，而不必将系统塞进其有限的约束中。
2. 可测试。无需UI、数据库、Web Server 或任何其他外部元素即可测试业务规则。
3. 独立于 UI。UI 可以轻松更改，而无需更改系统的其他部分。例如，Web UI 可以替换为控制台 UI，而无需更改业务规则。
4. 独立于数据库。您可以换出甲骨文或 SQL 服务器，换成蒙古、大表、沙发或其他东西。您的业务规则不受数据库约束。
5. 独立于任何外部机构。事实上，你的商业规则根本不了解外部世界。

本文顶部的图表是将所有这些架构集成到单个可操作构想中的尝试。

## 依赖规则

同心圆表示软件的不同区域。一般来说，你走得越远，软件就越高。外圈是机制。内圈是政策。

使这个架构起作用的首要规则是*依赖规则*。此规则说源*代码依赖只能**指向内。*内圈里什么也不知道外圈里的东西。特别是，外圈中声明的某物的名称不得由内圈中的代码提及。这包括，功能，类。变量，或任何其他命名的软件实体。

同样，外圈中使用的数据格式不应由内圈使用，特别是如果这些格式是由外圈中的框架生成的。我们不希望外圈中的任何东西影响内圈。

## *实体*

实体概括了*企业范围*的业务规则。实体可以是具有方法的对象，也可以是一组数据结构和功能。只要实体可以被企业中的许多不同的应用程序使用，这并不重要。

如果您没有企业，并且只是编写单个应用程序，则这些实体是应用程序的业务对象。它们概括了最笼统和最高级别的规则。当外部变化时，它们变化的可能性最小。例如，您不会期望这些对象受到页面导航或安全性更改的影响。任何特定应用程序的任何操作更改都不应影响实体层。

## 使用案例

此层中的软件包含*应用程序特定*的业务规则。它封装并实施系统的所有使用案例。这些使用案例协调了数据流向实体，并指示这些实体使用其*企业范围的业务*规则来实现使用案例的目标。

我们预计此层的变化不会影响实体。我们也不期望此层受到数据库、UI 或任何常见框架等外部性变化的影响。这一层与此类问题隔离开来。

不过*，我们*预计应用程序操作的更改*将*影响使用案例，从而影响此层中的软件。如果用例的详细信息发生变化，则此层中的某些代码肯定会受到影响。

## 接口适配器

此层中的软件是一组适配器，可将数据从最方便的使用案例和实体格式转换为对数据库或 Web 等外部机构最方便的格式。例如，正是这一层将完全包含 GUI 的 MVC 架构。演示者、视图和控制器都属于此处。这些模型可能只是从控制器传递到使用案例的数据结构，然后从使用案例传回演示者和视图。

同样，数据也从实体和使用案例最方便的形式转换为最方便使用任何持久性框架的形式。即数据库。这个圈子的内在代码不应该知道任何关于数据库。如果数据库是 SQL 数据库，则所有 SQL 应限制在此层，特别是与数据库有关此层的部分。

此外，此层中还有任何其他必要的适配器，用于将数据从某些外部形式（如外部服务）转换为使用案例和实体使用的内部表单。

## 框架和驱动程序。

最外层通常由数据库、Web 框架等框架和工具组成。通常，除了向内与下一个圆圈通信的胶水代码外，您不会在此层中编写太多代码。

此层是所有详细信息的去处。网络是一个细节。数据库是一个细节。我们把这些东西放在外面，在那里它们不会造成什么伤害。

## 只有四个圆圈？

不，圆圈是示意图。你可能会发现，你需要的不仅仅是这四个。没有规则说你必须总是只有这四个。但是，*依赖规则*始终适用。源代码依赖性总是指向内。当您向内移动时，抽象水平会增加。最外层的圆是低层混凝土细节。当您向内移动时，软件变得更加抽象，并封装了更高级别的政策。内圈最一般。

## 跨越边界。

在图表的右下角，是我们如何跨越圆界的一个例子。它显示控制器和演示者与下一层中的使用案例进行通信。注意控制流。它从控制器开始，通过使用案例移动，然后最终在演示者中执行。还要注意源代码依赖性。他们每个人都指向内向使用案例。

我们通常使用[依赖反转原则](http://en.wikipedia.org/wiki/Dependency_inversion_principle)来解决这一明显的矛盾。例如，在 Java 等语言中，我们会安排界面和继承关系，以便源代码依赖性反对在边界的正确点进行控制。

例如，考虑使用案例需要呼叫演示者。但是，此呼叫不得直接，因为这将违反*依赖规则*：内圈不能提及外圈中的名称。因此，我们有使用案例调用界面（此处显示为使用案例输出端口），并让外圈中的演示者实现它。

同样的技术用于跨越架构中的所有边界。我们利用动态多态性创建源代码依赖性，反对控制流，以便无论控制流向哪个方向，我们都能遵守*依赖规则*。

## 什么数据跨越了界限。

通常跨越边界的数据是简单的数据结构。如果您愿意，您可以使用基本结构或简单的数据传输对象。或者数据可以简单地作为函数调用中的参数。或者你可以把它打包成哈沙普， 或者把它构造成一个物体。重要的是，孤立、简单的数据结构会跨越边界。我们不想欺骗和通过*实体*或数据库行。我们不希望数据结构有任何违反依赖*规则的依赖性*。

例如，许多数据库框架会返回一个方便的数据格式来响应查询。我们可以称之为行结构。我们不想将行结构向内穿过边界。这将违反*依赖规则*，因为它会迫使一个内圈了解一个外圈。

因此，当我们将数据传递到边界时，它总是以最方便的形式进入内圈。

## 结论

遵守这些简单的规则并不难，并会节省你很多头痛的未来。通过将软件分离成层，并符合*依赖规则*，您将创建一个内在可测试的系统，并具有所有意味着的好处。当系统的任何外部部分过时时（如数据库或 Web 框架）时，您可以以最小的大惊小怪来替换这些过时的元素。



