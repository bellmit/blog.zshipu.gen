
---
title: Python基础：Python文件操作
author: 知识铺
date: 2020-10-25 20:09:11+08:00
tags: [python]
---
# Python文件操作



文件处理是任何 Web 应用程序的重要组成部分。

Python 具有多个用于创建、读取、更新和删除文件的函数。

* * *

## 文件处理

<font _mstmutation="1" _msthash="103727" _msttexthash="105502150">使用 Python 中的文件的关键功能是该函数。</font>```open()```

<font _mstmutation="1" _msthash="103922" _msttexthash="64696268">函数采用两个参数;_文件名_和_模式_。</font>```open()```

打开文件有四种不同的方法（模式）：

```"r"```<font _mstmutation="1" _msthash="220428" _msttexthash="245121240">- 读取 - 默认值。打开文件进行读取，如果文件不存在，则出现错误</font>

```"a"```<font _mstmutation="1" _msthash="220701" _msttexthash="195387283">- 追加 - 打开文件进行追加，如果文件不存在，则创建该文件</font>

```"w"```<font _mstmutation="1" _msthash="220974" _msttexthash="190085818">- 写入 - 打开文件进行写入，如果文件不存在，则创建该文件</font>

```"x"```<font _mstmutation="1" _msthash="221247" _msttexthash="168548315">- 创建 - 创建指定的文件，如果文件存在，则返回错误</font>

此外，您可以指定文件应作为二进制模式还是文本模式处理

```"t"```<font _mstmutation="1" _msthash="220870" _msttexthash="45163573">- 文本 - 默认值。文本模式</font>

```"b"```<font _mstmutation="1" _msthash="221143" _msttexthash="87660872">- 二进制 - 二进制模式（例如图像）</font>

* * *

## 语法

要打开文件以读取该文件，就足以指定文件的名称：
```
 f = open("demofile.txt")
```
上述代码与以下代码相同：
```
 f = open("demofile.txt", "rt")
```
<font _mstmutation="1" _msthash="104494" _msttexthash="157475344">因为对于读取和文本是默认值，因此不需要指定它们。</font>```"r"``````"t"```

**注：**确保文件存在，否则您会收到错误。


