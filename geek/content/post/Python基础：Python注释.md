
---
title: Python基础：Python注释
author: 知识铺
date: 2020-10-25 14:29:22+08:00
tags: [python]
---
# Python注释


* * *

注释可用于解释 Python 代码。

注释可用于使代码更具可读性。

注释可用于在测试代码时阻止执行。

* * *

## 创建注释

<font _mstmutation="1" _msthash="103922" _msttexthash="79053247">注释以 开头，Python 将忽略它们：</font>```#```

### 例子
```
 #This is a comment print("Hello, World!")
```
注释可以放在行的末尾，Python 将忽略行的其余部分：

### 例子
```
 print("Hello, World!") #This is a comment

```
注释不必是文本来解释代码，它也可以用来防止 Python 执行代码：

### 例子
```
 #print("Hello, World!") print("Cheers, Mate!")

```
* * *

* * *

## 多行注释

Python 没有多行注释的语法。

<font _mstmutation="1" _msthash="104689" _msttexthash="111395921">要添加多行注释，可以为每行插入 一个：</font>```#```

### 例子
```
 #This is a comment #written in #more than just one line print("Hello, World!")

```
或者，不完全如预期，您可以使用多行字符串。

由于 Python 将忽略未分配给变量的字符串文本，因此可以在代码中添加多行字符串（三重引号），并将注释放在代码中：

### 例子

 """
This is a comment
written in
more than just one line
"""
```
print("Hello, World!")
```
只要字符串未分配给变量，Python 就会读取代码，但随后忽略它，并且您已经进行了多行注释。


* * *

## 用练习测试自己

## 运动：

Python 中的注释是用特殊字符编写的，哪一个？
```
 This is a comment
```
