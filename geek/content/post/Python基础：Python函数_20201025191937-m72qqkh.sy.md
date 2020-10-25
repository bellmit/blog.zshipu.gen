---
title: Python基础：Python函数
author: 知识铺
date: 2020-10-25 18:53:55+08:00
tags: [python]
---

# Python函数

函数是仅在调用时运行的代码块。

您可以将数据（称为参数）传递到函数中。

因此，函数可以返回数据。

---

## 创建函数

在 Python 中，函数使用def 关键字定义：

### 例子

```
 def my_function():
  print("Hello from a function")
```

---

## 调用函数

若要调用函数，请使用函数名称后跟括号：

### 例子

```
 def my_function():
  print("Hello from a function")

**my_function()**

```

---

## 参数

信息可以作为参数传递到函数中。

参数在函数名称之后在括号内指定。您可以根据需要添加尽可能多的参数，只需用逗号分隔它们。

下面的示例具有一个带一个参数（fname）的函数。调用函数时，我们传递一个名字，该名字在函数内用于打印全名：

### 例子

```
 def my_function(**fname**):
  print(fname + " Refsnes")

my_function(**"Emil"**)
my_function(**"Tobias"**)
my_function(**"Linus"**)

```

_在_Python 文档中，_参数通常_缩短为 args。

---

---

## 参数还是参数？

术语_参数__和_参数可用于同一件事：传递到函数中的信息。

从函数的角度来看：

参数是函数定义中括号内列出的变量。

参数是调用函数时发送到该函数的值。

---

## 参数数

默认情况下，必须使用正确的参数数调用函数。这意味着，如果函数需要 2 个参数，则必须使用 2 个参数调用该函数，而不是更多参数，而不是更少参数。

### 例子

此函数需要 2 个参数，并获取 2 个参数：

```
 def my_function(fname, lname):
  print(fname + " " + lname)

my_function("Emil", "Refsnes")

```

<font _mstmutation="1" _msthash="46592" _msttexthash="176644299">如果尝试使用 1 或 3 个参数调用该函数，将收到错误：</font>

### 例子

此函数需要 2 个参数，但仅得到 1 个参数：

```
 def my_function(fname, lname):
  print(fname + " " + lname)

my_function("Emil")

```

---

## 任意参数，*args

<font _mstmutation="1" _msthash="104858" _msttexthash="246300938">如果不知道将传递到函数中的参数数，请在函数定义中添加参数名称之前。</font>``*``

这样，函数将收到一_元参数_，并可以相应地访问项：

### 例子

<font _mstmutation="1" _msthash="221767" _msttexthash="100195667">如果参数数未知，请添加参数名称之前的</font>``*``

```
 def my_function(*kids):
  print("The youngest child is " + kids[2])

my_function("Emil", "Tobias", "Linus")

```

_在 Python_文档中，任意_参数通常缩短为_*args。

---

## 关键字参数

还可以发送具有键 =_值_语法_的_参数。

这样，参数的顺序并不重要。

### 例子

```
 def my_function(child3, child2, child1):
  print("The youngest child is " + child3)

my_function(child1 = "Emil", child2 = "Tobias", child3 = "Linus")

```

在 Python_文档中，_关键字参数短语_通常缩短为_kwargs。

---

## 任意关键字参数，**kwargs

<font _mstmutation="1" _msthash="105820" _msttexthash="377145067">如果不知道将传递到函数中的关键字参数数，请添加两个星号：在函数定义的参数名称之前。</font>``**``

这样，函数将收到参数_字典_，并可以相应地访问项：

### 例子

<font _mstmutation="1" _msthash="220857" _msttexthash="211236103">如果关键字参数的数量未知，请添加参数名称前的双精度值：</font>``**``

```
 def my_function(**kid):
  print("His last name is " + kid["lname"])

my_function(fname = "Tobias", lname = "Refsnes")

```

_在 Python 文档中_，任意_Kword 参数通常缩短为 **kwargs。_

---

## 默认参数值

下面的示例演示如何使用默认参数值。

如果我们调用没有参数的函数，它将使用默认值：

### 例子

```
 def my_function(**country = "Norway"**):
  print("I am from " + country)

my_function("Sweden")
my_function("India")
my_function()
my_function("Brazil")

```

---

## 将列表作为参数传递

您可以将任何数据类型的参数发送到函数（字符串、数字、列表、字典等），该函数将被视为函数中的相同数据类型。

例如，如果将列表作为参数发送，则当列表到达函数时，它仍将是列表：

### 例子

```
 def my_function(food):
  for x in food:
    print(x)

fruits = ["apple", "banana", "cherry"]

my_function(fruits) 

```

---

## 返回值

<font _mstmutation="1" _msthash="105989" _msttexthash="94536572">若要让函数返回值，请使用 语句：</font>``return``

### 例子

```
 def my_function(x):
  **return 5 * x** 
print(my_function(3))
print(my_function(5))
print(my_function(9))

```

---

## 传递语句

``function``<font _mstmutation="1" _msthash="105196" _msttexthash="361827024">定义不能为空，但如果您由于某种原因具有无内容的定义，请放入 语句以避免收到错误。</font>``function``````pass``

### 例子

```
 def myfunction():
  pass

```

---

## 递 归

Python 还接受函数递归，这意味着定义的函数可以调用自身。

递归是一个常见的数学和编程概念。这意味着函数调用自己。这样做的好处是，您可以循环浏览数据以得出结果。

开发人员应该非常小心递归，因为它很容易滑入编写一个从不终止的函数，或者使用过多的内存或处理器电源的函数。但是，当正确写入时，递归可以是一种非常高效且数学上优雅的编程方法。

在此示例中，tri_recursion（）是一个函数，我们已定义它来调用自身（"递归"）。我们使用k变量作为数据，每次我们递归时都会递值 （-1） 。当条件不大于 0 时（即当条件为 0 时），递归结束。

对于一个新的开发人员来说，它可能需要一些时间来找出它到底是如何工作的，最好的发现方式是测试和修改它。

### 例子

递归示例

```
 def tri_recursion(k):
  if(k > 0):
    result = k + tri_recursion(k - 1)
    print(result)
  else:
    result = 0
  return result

print("\n\nRecursion Example Results")
tri_recursion(6) 

```
