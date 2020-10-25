
---
title: Python基础：Python数据类型
author: 知识铺
date: 2020-10-25 14:34:10+08:00
tags: [python]
---
# Python数据类型

* * *

## 内置数据类型

在编程中，数据类型是一个重要的概念。

变量可以存储不同类型的数据，不同类型的变量可以处理不同的事情。

默认情况下，Python 具有以下内置的数据类型，这些类别：

| 文本类型： | ```str``` |
| 数字类型： | ```int```<font _mstmutation="1" _msthash="752284" _msttexthash="8580">, ,</font>```float``````complex``` |
| 序列类型： | ```list```<font _mstmutation="1" _msthash="752700" _msttexthash="8580">, ,</font>```tuple``````range``` |
| 映射类型： | ```dict``` |
| 设置类型： | ```set```<font _mstmutation="1" _msthash="753532" _msttexthash="4004">,</font>```frozenset``` |
| 布尔类型： | ```bool``` |
| 二进制类型： | ```bytes```<font _mstmutation="1" _msthash="754364" _msttexthash="8580">, ,</font>```bytearray``````memoryview``` |

* * *

## 获取数据类型

<font _mstmutation="1" _msthash="104312" _msttexthash="131868971">您可以使用 以下函数获取任何对象的数据类型：</font>```type()```

### 例子

打印变量 x 的数据类型：
```
 x = 5
print(type(x))

```

* * *

## 设置数据类型

在 Python 中，在将值分配给变量时设置数据类型：

<style>#dtref td:nth-child(1) { font-family: Consolas,"courier new"; font-size: 110%; }</style>

| Example | Data Type |
| x = "Hello World" | str | 
| x = 20 | int | 
| x = 20.5 | float | 
| x = 1j | complex | 
| x = ["apple", "banana", "cherry"] | list | 
| x = ("apple", "banana", "cherry") | tuple | 
| x = range(6) | range | 
| x = {"name" : "John", "age" : 36} | dict | 
| x = {"apple", "banana", "cherry"} | set | 
| x = frozenset({"apple", "banana", "cherry"}) | frozenset | 
| x = True | bool | 
| x = b"Hello" | bytes | 
| x = bytearray(5) | bytearray | 
| x = memoryview(bytes(5)) | memoryview | 

* * *

* * *

## 设置特定数据类型

如果要指定数据类型，可以使用以下构造函数：

| Example | Data Type |
| x = str("Hello World") | str | 
| x = int(20) | int | 
| x = float(20.5) | float | 
| x = complex(1j) | complex | 
| x = list(("apple", "banana", "cherry")) | list | 
| x = tuple(("apple", "banana", "cherry")) | tuple | 
| x = range(6) | range | 
| x = dict(name="John", age=36) | dict | 
| x = set(("apple", "banana", "cherry")) | set | 
| x = frozenset(("apple", "banana", "cherry")) | frozenset | 
| x = bool(5) | bool | 
| x = bytes(5) | bytes | 
| x = bytearray(5) | bytearray | 
| x = memoryview(bytes(5)) | memoryview | 



* * *


