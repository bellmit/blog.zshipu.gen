
---
title: Python基础：Python语法
author: 知识铺
date: 2020-10-25 14:27:46+08:00
tags: [python]
---
# Python语法



* * *

[执行 Python 语法](#execute_python_syntax) [Python 缩进](#python_indentation) [Python 变量](#python_variables) [Python 注释](#python_comments) [练习](#exercises)

<a id="execute_python_syntax"></a>
## 执行 Python 语法

正如我们在上一页中学到的，Python 语法可以通过直接在命令行中写入来执行：
```
 >>> print("Hello, World!")
Hello, World!
```
或者，在服务器上创建 python 文件，使用 .py 文件扩展名，并在命令行中运行该文件：
```
 C:\Users\_Your Name_>python myfile.py
```
* * *

<a id="python_indentation"></a>
## Python 缩进

缩进是指代码行开头的空格。

在其他编程语言中，代码中的缩进仅用于可读性，则 Python 中的缩进非常重要。

Python 使用缩进来指示代码块。

### 例子
```
 if 5 > 2:
  print("Five is greater than two!")
```

如果跳过缩进，Python 将为您提供错误：

### 例子

语法错误：
```
 if 5 > 2:
print("Five is greater than two!")
```

作为程序员，空格数由您决定，但它必须至少为一个。

### 例子
```
 if 5 > 2:
 print("Five is greater than two!") 
if 5 > 2:
        print("Five is greater than two!") 
```

您必须在同一代码块中使用相同数量的空格，否则 Python 会给您一个错误：

### 例子

语法错误：
```
 if 5 > 2:
 print("Five is greater than two!")
        print("Five is greater than two!")

```
* * *

* * *

<a id="python_variables"></a>
## Python 变量

在 Python 中，当您为其分配值时，将创建变量：

### 例子

Python 中的变量：
```
 x = 5
y = "Hello, World!"

```
Python 没有声明变量的命令。

您将在 Python 变量章节中[了解有关变量的详细了解](python_variables.asp)。

* * *

<a id="python_comments"></a>
## 评论

Python 具有用于代码中文档的注释功能。

注释以 #开始，Python 将呈现行的其余部分为注释：

### 例子

Python 中的注释：
```
 #This is a comment. print("Hello, World!")

```
<a id="exercises"></a>

* * *

## 用练习测试自己

## 运动：

插入下面的代码缺失部分以输出"你好世界"。
```
 ("Hello World")
```

