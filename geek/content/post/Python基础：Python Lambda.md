
---
title: Python基础：Python Lambda
author: 知识铺
date: 2020-10-25 18:56:31+08:00
tags: [python]
---
# Python Lambda


lambda 函数是一个小的匿名函数。

lambda 函数可以接受任何数量的参数，但只能有一个表达式。

* * *

## 语法

 lambda _arguments_ : _expression_

执行表达式并返回结果：

### 例子

<font _mstmutation="1" _msthash="220480" _msttexthash="74227335">向 参数 添加 10，并返回结果：</font>```a```
```
 x = lambda a : a + 10
print(x(5))

```

Lambda 函数可以具有多数个参数：

### 例子

<font _mstmutation="1" _msthash="220922" _msttexthash="74341046">将参数与参数相乘并返回结果：</font>```a``````b```
```
 x = lambda a, b : a * b
print(x(5, 6))

```

### 例子

<font _mstmutation="1" _msthash="221143" _msttexthash="59657650">总结参数 、和 并返回结果：</font>```a``````b``````c```
```
 x = lambda a, b, c : a + b + c
print(x(5, 6, 2))

```

* * *

* * *

## 为什么要使用 Lambda 函数？

当您将 lambda 用作另一个函数中的匿名函数时，可以更好地显示 lambda 的功率。

您是具有一个采用一个参数的函数定义，该参数将乘以一个未知数字：

 def myfunc(n):
  return lambda a : a * n

使用该函数定义使函数始终使发送的数量翻倍：

### 例子
```
 def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)

print(mydoubler(11))

```

或者，使用相同的函数定义来使始终将发送_的数量三_倍的函数：

### 例子
```
 def myfunc(n):
  return lambda a : a * n

mytripler = myfunc(3)

print(mytripler(11))

```

或者，使用相同的函数定义使两个函数，在同一程序中：

### 例子
```
 def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)
mytripler = myfunc(3)

print(mydoubler(11))
print(mytripler(11))

```

当需要匿名函数的短时间时，请使用 lambda 函数。

