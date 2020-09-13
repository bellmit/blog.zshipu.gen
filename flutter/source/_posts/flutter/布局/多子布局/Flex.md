---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Flex
author: 知识铺
weight: -1
---

# Flex

Row组件和Column组件都继承自Flex组件。

- Flex组件和Row、Column属性主要的区别就是多一个direction。
- 当direction的值为Axis.horizontal的时候，则是Row。
- 当direction的值为Axis.vertical的时候，则是Column。

在学习Row和Column之前，我们先学习`主轴`和`交叉轴`的概念。  
因为Row是一行排布，Column是一列排布，那么它们都存在两个方向，并且两个Widget排列的方向应该是对立的。  
它们之中都有主轴（MainAxis）和交叉轴（CrossAxis）的概念: 

- 对于Row来说:
    - 主轴（MainAxis）即横向X轴
    - 交叉轴（CrossAxis）即纵向Y轴
- 对于Column来说
    - 主轴（MainAxis）即纵向Y轴
    - 交叉轴（CrossAxis）即横向X轴

