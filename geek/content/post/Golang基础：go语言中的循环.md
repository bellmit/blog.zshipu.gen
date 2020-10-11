
---
title: Golang基础：go语言中的循环
author: 知识铺
date: 2020-10-11 21:56:25
tags: [golang]
---
循环允许您重复代码。有不同类型的循环，其中之一是 for 循环。对于[Go（golang）中的循环](https://zshipu.com/t?url=https://golang.org/)，与 Python 更类似于 C/Java。在 Python 中，语法是

 <code>for i in range(1,10):</code> 

在 C/Java 中，语法为

 <code>for (i = 1; i <= 10; i++) {</code> 

但在Golang

 <code>for i := 1; i <= 10; i++ {</code> 

因此，它受到这些语言的启发。

## [](#for-loop-explained)<font _mstmutation="1" _msthash="290550" _msttexthash="19263959">For 循环解释</font>

在上面的程序中，它是什么意思？
首先变量 i 的初始值为 1。

 <code>i := 1;</code> 

条件语句将检查 i <= 10。

 <code>i <= 10;</code> 

如果这是真的，它将停止循环。如果没有，则在循环内继续。
帖子语句每次迭代都会向 i 添加 1 个。

 <code>i++</code> 

换句话说，i= 与 i = i = 1 相同

## [](#example)<font _mstmutation="1" _msthash="305305" _msttexthash="4284137">例子</font>

<font _mstmutation="1" _msthash="292110" _msttexthash="106546388">一个从 1 到 10 的 for 循环计数的程序变为：</font>

 <code>package main

import (  
    "fmt"
)

func main() {  
    for i := 1; i <= 10; i++ {
        fmt.Printf(" %d",i)
    }
}</code> 

其他的东西是加载去， 导入 fmt 模块和主循环。
您也可以在Golang使用时循环](https://zshipu.com/t?url=https://golangr.com/while/)

**相关链接：**

*   [Golang官方网站](https://zshipu.com/t?url=https://golang.org/)
*   [转到教程](https://zshipu.com/t?url=https://golangr.com/)

