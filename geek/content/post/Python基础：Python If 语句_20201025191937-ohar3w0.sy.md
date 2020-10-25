---
title: Python基础：Python If 语句
author: 知识铺
date: 2020-10-25 18:48:06+08:00
tags: [python]
---

# Python If 语句

## Python 条件和 If 语句

Python 支持数学中通常的逻辑条件：

* 等于： a = b
* 不等于： a ！ = b
* 小于： < b
* 小于或等于：<= b
* 大于：a > b
* 大于或等于：>= b

这些条件可以通过多种方式使用，最常见的是"if 语句"和循环。

使用 if 关键字编写"if语句"。

### 例子

If 语句：

```
 a = 33
b = 200
if b > a:
  print("b is greater than a")

```

在此示例中，我们使用两个变量a和b，它们用作 if 语句的一部分，以测试b是否大于。由于a为33，b为200，我们知道 200 大于 33，因此我们打印以筛选"b 大于 a"。

## 压 痕

Python 依靠缩进（行开头的空格）来定义代码中的范围。其他编程语言通常使用大括号来用于此目的。

### 例子

if 语句，不缩进（将引发错误）：

```
 a = 33
b = 200
if b > a:
print("b is greater than a") # you will get an error

```

---

---

## 埃利夫

elif关键字是 python 的方式，用于表示"如果以前的条件不正确，则尝试此条件"。

### 例子

```
 a = 33
b = 33
if b > a:
  print("b is greater than a")
elif a == b:
  print("a and b are equal") 

```

在此示例中，a等于b，因此第一个条件不正确，但 elif 条件为true，因此我们打印以筛选"a 和 b 相等"。

---

## 还

else 关键字捕获未被上述条件捕获的任何东西。

### 例子

```
 a = 200
b = 33
if b > a:
  print("b is greater than a")
elif a == b:
  print("a and b are equal")
else:
  print("a is greater than b") 

```

在此示例中，a大于b，因此第一个条件不正确，elif条件也不正确，因此我们去 else条件并打印以筛选"a 大于 b"。

<font _mstmutation="1" _msthash="103896" _msttexthash="45277999">您还可以有一个没有 ：</font>``else``````elif``

### 例子

```
 a = 200
b = 33
if b > a:
  print("b is greater than a")
else:
  print("b is not greater than a") 

```

---

## 短手如果

如果只有一个语句要执行，可以把它放在与 if 语句相同的行上。

### 例子

一行 if 语句：

```
 if a > b: print("a is greater than b")

```

---

## 短手如果...还

如果只有一个语句要执行，一个用于 if，另一个用于其他语句，您可以将所有语句都放在同一行上：

### 例子

一行如果其他语句：

```
 a = 2
b = 330
print("A") if a > b else print("B")

```

此技术称为**"三元运算符"**或**"条件表达式"。**

也可以在同一行上有多个其他语句：

### 例子

一行如果其他语句，有 3 个条件：

```
 a = 330
b = 330
print("A") if a > b else print("=") if a == b else print("B")

```

---

## 和

和 关键字是逻辑运算符，用于组合条件语句：

### 例子

<font _mstmutation="1" _msthash="222430" _msttexthash="63377587">测试 是否大于 ，如果大于 ，</font>``a``````b``````c``````a``

```
 a = 200
b = 33
c = 500
if a > b and c > a:
  print("Both conditions are True") 

```

---

## 或

<font _mstmutation="1" _msthash="104845" _msttexthash="131312285">关键字是逻辑运算符，用于组合条件语句：</font>``or``

### 例子

<font _mstmutation="1" _msthash="221533" _msttexthash="30849715">测试 是否大于 或大于</font>``a``````b``````a``````c``

```
 a = 200
b = 33
c = 500
if a > b or a > c:
  print("At least one of the conditions is True") 

```

---

## 嵌套如果

<font _mstmutation="1" _msthash="105820" _msttexthash="91012129">语句中可以有语句，这称为_嵌套语句_。</font>``if``````if``````if``

### 例子

```
 x = 41

if x > 10:
  print("Above ten,")
  if x > 20:
    print("and also above 20!")
  else:
    print("but not above 20.")

```

---

## 传递语句

``if``<font _mstmutation="1" _msthash="105027" _msttexthash="399714315">语句不能为空，但如果您由于某种原因有一个没有内容的语句，请放入 语句以避免收到错误。</font>``if``````pass``

### 例子

```
 a = 33
b = 200

if b > a:
  pass

```
