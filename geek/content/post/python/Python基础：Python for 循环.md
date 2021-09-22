
---
title: Python基础：Python for 循环
author: 知识铺
date: 2020-10-25 18:51:51+08:00
tags: [python]
---
# Python for 循环



## Python for 循环

for循环用于在序列（列表、元组、字典、集或字符串）上迭代。

这与其他编程语言中的 for关键字不同，它的工作方式更像其他面向对象的编程语言中的一个引用器方法。

使用for循环，我们可以执行一组语句，一次用于列表、元组、集等中的每一项。

### 例子

在水果列表中打印每个水果：
```
 fruits = ["apple", "banana", "cherry"]
for x in fruits:
  print(x)

```

for循环不需要事先设置索引变量。

* * *

## 循环通过字符串

即使字符串也是可重复的对象，它们包含一系列字符：

### 例子

遍历"香蕉"一词中的字母：
```
 for x in "banana":
  print(x)

```

* * *

## 中断语句

使用break语句，我们可以在循环遍历所有项之前停止循环：

### 例子

<font _mstmutation="1" _msthash="220246" _msttexthash="50754834">当"香蕉"时退出循环：</font>```x```
```
 fruits = ["apple", "banana", "cherry"]
for x in fruits:
  print(x)
  if x == "banana":
    break 

```

### 例子

<font _mstmutation="1" _msthash="220467" _msttexthash="175067763">当是"香蕉"时退出循环，但这次中断出现在打印之前：</font>```x```
```
 fruits = ["apple", "banana", "cherry"]
for x in fruits:
  if x == "banana":
    break
  print(x)

```

* * *

* * *

## 继续声明

使用continue 语句，我们可以停止循环的当前迭代，并继续下一个：

### 例子

不要打印香蕉：
```
 fruits = ["apple", "banana", "cherry"]
for x in fruits:
  if x == "banana":
    continue
  print(x)

```

* * *

## 范围（） 函数

<font _mstmutation="1" _msthash="46592" _msttexthash="252233020">要循环浏览一组指定数量的代码，我们可以使用范围（） 函数，</font>

范围（）函数返回一系列数字，默认情况下从 0 开始，以 1（默认情况下）为增量，以指定数字结束。

### 例子

使用范围（） 函数：
```
 for x in range(6):
  print(x)

```

请注意，范围（6）不是 0 到 6 的值，而是值 0 到 5。

范围（）函数默认为 0 作为起始值，但可以通过添加参数来指定起始值：范围（2，6），这意味着值从 2 到 6（但不包括 6）：

### 例子

使用开始参数：
```
 for x in range(2, 6):
  print(x)

```

范围（）函数默认将序列增量为 1，但可以通过添加第三个参数：范围（2、30、3 ）**来指定**增量值：

### 例子

将序列与 3 递增（默认值为 1）：
```
 for x in range(2, 30, 3):
  print(x)

```

* * *

## 否则在 For 循环

<font _mstmutation="1" _msthash="105443" _msttexthash="157559623">循环中的关键字指定在循环完成后要执行的代码块：</font>```else``````for```

### 例子

打印从 0 到 5 的所有数字，并在循环结束时打印消息：
```
 for x in range(6):
  print(x)
else:
  print("Finally finished!")

```

* * *

## 嵌套循环

嵌套循环是循环中的循环。

"内部循环"将在"外部循环"的每个迭代中执行一次：

### 例子

打印每个水果的每个形容词：
```
 adj = ["red", "big", "tasty"]
fruits = ["apple", "banana", "cherry"]

for x in adj:
  for y in fruits:
    print(x, y)

```

* * *

## 传递语句

```for```<font _mstmutation="1" _msthash="105820" _msttexthash="382214248">循环不能为空，但如果由于某种原因有一个没有内容的循环，请放入 语句以避免收到错误。</font>```for``````pass```

### 例子
```  
 for x in [0, 1, 2]:
pass

```

