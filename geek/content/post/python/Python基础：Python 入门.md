
---
title: Python基础：Python 入门
author: 知识铺
date: 2020-10-25 14:25:39+08:00
tags: [python]
---
# Python 入门


## Python 安装

许多 PC 和 Mac 将安装 python。

要检查是否安装了 Python 在 Windows PC 上，请在开始栏中搜索 Python 或在命令行 （cmd.exe） 上运行以下内容：
```
 C:\Users\_Your Name_>python --version
```
要检查您是否在 Linux 或 Mac 上安装了 python，然后在 linux 上打开命令行或在 Mac 上打开终端并键入：
```
 python --version
```
如果您发现您的计算机上没有安装 python，那么您可以从以下网站免费下载它[：https://www.python.org/](https://zshipu.com/t?url=https://www.python.org/)

* * *

## Python 快速入门

Python 是一种解释性编程语言，这意味着作为开发人员，您将 Python （.py） 文件写入文本编辑器，然后将这些文件放入要执行的 python 解释器中。

运行 python 文件的方法在命令行上是这样的：
```
 C:\Users\_Your Name_>python helloworld.py
```
其中helloworld.py"是您的 python 文件的名称。

让我们编写第一个 Python 文件，称为 helloworld.py，可以在任何文本编辑器中完成。
```
helloworld.py

 print("Hello, World!")
```
[自己试试 |](trypython.asp?filename=demo_helloworld)

就这么简单保存文件。打开命令行，导航到保存文件的目录，然后运行：
```
 C:\Users\_Your Name_>python helloworld.py
```
输出应为：
```
 Hello, World!
```
恭喜你，您已经编写并执行了您的第一个 Python 程序。

* * *

* * *

## Python 命令行

要在 python 中测试少量代码，有时在文件中不编写代码是最快和最容易的。之所以能够这样做，是因为 Python 可以作为命令行本身运行。

在 Windows、Mac 或 Linux 命令行上键入以下内容：
```
 C:\Users\_Your Name_>python
```
<font _mstmutation="1" _msthash="46592" _msttexthash="164525894">或者，如果"python"命令不起作用，您可以尝试"py"：</font>
```
 C:\Users\_Your Name_>py
```
从那里你可以写任何python，包括我们在教程前面的hello世界示例：
```
 C:\Users\_Your Name_>python
Python 3.6.4 (v3.6.4:d48eceb, Dec 19 2017, 06:04:45) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello, World!")
```
这将在命令行中写"你好，世界！
```
 C:\Users\_Your Name_>python
Python 3.6.4 (v3.6.4:d48eceb, Dec 19 2017, 06:04:45) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello, World!")
Hello, World!
```
每当在 python 命令行中完成时，只需键入以下内容即可退出 python 命令行接口：
```
 exit()
```

