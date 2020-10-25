
---
title: Python基础：Python类和对象
author: 知识铺
date: 2020-10-25 19:25:18+08:00
tags: [python]
---
# Python类和对象



## Python 类/对象

Python 是一种面向对象的编程语言。

Python 中的几乎所有内容都是一个对象，其属性和方法。

类就像对象构造函数，或用于创建对象的"蓝图"。

* * *

## 创建类

<font _mstmutation="1" _msthash="104117" _msttexthash="77059762">若要创建类，请使用 关键字 ：</font>```class```

### 例子

创建名为 MyClass 的类，其属性名为 x：
```
 class MyClass:
  x = 5

```

* * *

## 创建对象

现在，我们可以使用名为 MyClass 的类来创建对象：

### 例子

创建名为 p1 的对象，并打印 x 的值：
```
 p1 = MyClass()
print(p1.x)

```

* * *

## __init__（） 功能

上面的示例是类和对象最简单的形式，在实际应用程序中并不真正有用。

为了理解类的含义，我们必须理解内置的__init__（） 函数。

所有类都有一个名为 __init__（）的函数，在启动类时始终执行该函数。

使用 __init__）函数将值分配给对象属性，或在创建对象时执行所需的其他操作：

### 例子

创建名为 Person 的类，使用 __init__（） 函数为名称和年龄分配值：
```
 class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("John", 36)

print(p1.name)
print(p1.age)

```

<font _mstmutation="1" _msthash="221520" _msttexthash="169165035">**注：**每次使用类创建新对象时，都会自动调用该函数。</font>```__init__()```

* * *

* * *

## 对象方法

对象还可以包含方法。对象中的方法是属于对象的函数。

让我们在 Person 类中创建一个方法：

### 例子

插入打印问候语的函数，并在 p1 对象上执行：
```
 class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def myfunc(self):
    print("Hello my name is " + self.name)

p1 = Person("John", 36)
p1.myfunc()

```

<font _mstmutation="1" _msthash="221728" _msttexthash="178402744">**注：**参数是类当前实例的引用，用于访问属于类的变量。</font>```self```

* * *

## 自我参数

<font _mstmutation="1" _msthash="104468" _msttexthash="152278022">参数是类当前实例的引用，用于访问属于类的变量。</font>```self```

<font _mstmutation="1" _msthash="104663" _msttexthash="354171727">它不必被命名，你可以调用它任何你喜欢的，但它必须是类中任何函数的第一个参数：</font>```self```

### 例子

使用单词_mysillyobjject_和_abc_而不是_自我_：
```
 class Person:
  def __init__(mysillyobject, name, age):
    mysillyobject.name = name
    mysillyobject.age = age

  def myfunc(abc):
    print("Hello my name is " + abc.name)

p1 = Person("John", 36)
p1.myfunc()

```

* * *

## 修改对象属性

您可以修改对象的属性，像这样：

### 例子

将 p1 的年龄设置为 40：
```
 p1.age = 40

```

* * *

## 删除对象属性

<font _mstmutation="1" _msthash="104845" _msttexthash="84568757">可以使用 关键字删除对象的属性：</font> ```del```

### 例子

从 p1 对象中删除年龄属性：
```
 del p1.age

```

* * *

## 删除对象

<font _mstmutation="1" _msthash="105820" _msttexthash="69597424">您可以使用 关键字删除对象：</font>```del```

### 例子

删除 p1 对象：
```
 del p1

```

* * *

## 传递语句

```class```<font _mstmutation="1" _msthash="105027" _msttexthash="361827024">定义不能为空，但如果您由于某种原因具有无内容的定义，请放入 语句以避免收到错误。</font>```class``````pass```

### 例子

```
 class Person:  
    pass

```


