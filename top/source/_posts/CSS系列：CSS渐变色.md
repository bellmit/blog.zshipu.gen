
title: CSS系列：CSS渐变色
author: 知识铺
date: 2020-09-20 19:09:31
tags: 
---
 什么是渐变？
渐变是淡入另一种颜色的一种颜色。此颜色可以淡入不同的方向，例如：顶部、底部、左侧、右侧、对角线 e.t.c。此效果可以通过使用 CSS 渐变来完成。
根据 W3 学校，CSS 定义了两种类型的梯度：

1.  线性梯度
2.  激进渐变

线性渐变（向下/向上/向左/右/对角）
理解这个概念的最简单方法是线性渐变函数沿直线过渡两种或两种多种颜色，因此名称是线性的。
在创建线性渐变时，应至少指定两种颜色才能工作，并且选择器为背景图像。
语法：
背景图像：线性渐变（方向、颜色1、颜色2、...）;

我将用一些例子来更好地理解：

示例 1
方向 - 从上到下（这是默认值）。
我将开始在我的索引.html 中创建一个 div，并将一个内容放入内部，因为

<font _mstmutation="1" _msthash="196781" _msttexthash="116821302">标记不起作用，除非它包含内容。
索引.html：</font>

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--CYXklARK--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/rtjhwets7dqtzsg6vwit.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--CYXklARK--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/rtjhwets7dqtzsg6vwit.PNG)

<font _mstmutation="1" _msthash="290017" _msttexthash="22405773">然后在我的CSS里</font>
[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--MDmtmVI5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/u31ai3ycic00otrcq0bn.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--MDmtmVI5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/u31ai3ycic00otrcq0bn.PNG)

<font _mstmutation="1" _msthash="290316" _msttexthash="13353795">结果：</font>
[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--N_UB6lkq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/btruiv99igx0wsyxh12l.jpg)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--N_UB6lkq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/btruiv99igx0wsyxh12l.jpg)

示例 2
方向 - 从左到右

<font _mstmutation="1" _msthash="290914" _msttexthash="24193299">在 CSS 文件中，</font>
[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--JoFgAv_m--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/vobadywnwe7625e1o08o.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--JoFgAv_m--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/vobadywnwe7625e1o08o.PNG)

<font _mstmutation="1" _msthash="291213" _msttexthash="13353795">结果：</font>
[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--AUIcd3LU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6eg6w2n2i4gaplj07rry.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--AUIcd3LU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6eg6w2n2i4gaplj07rry.PNG)

示例 3
方向
- 对角线：您可以通过指定水平和垂直起始位置对角线进行渐变。

<font _mstmutation="1" _msthash="291811" _msttexthash="24193299">在 CSS 文件中，</font>
[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--nxtpKvfo--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/0nmpe38n6t04fn7qiw5w.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--nxtpKvfo--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/0nmpe38n6t04fn7qiw5w.PNG)

<font _mstmutation="1" _msthash="292110" _msttexthash="13353795">结果：</font>
[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--e0LB9o_A--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/i61mz8z7xjmisna0pat2.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--e0LB9o_A--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/i61mz8z7xjmisna0pat2.PNG)



