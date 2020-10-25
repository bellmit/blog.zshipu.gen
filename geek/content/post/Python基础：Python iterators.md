
---
title: Python基础：Python iterators
author: 知识铺
date: 2020-10-25 19:33:42+08:00
tags: [python]
---
# Python iterators



## Python iterators

活动器是包含可计数值数的对象。

遍历器是可遍历的对象，这意味着您可以遍历所有值。

<font _mstmutation="1" _msthash="95628" _msttexthash="356178485">从技术上讲，在 Python 中，一个数据器是实现引用器协议的对象，它由方法和 组成。</font>```__iter__()``````__next__()```

* * *

## 可移动器与可移动

列表、元组、字典和集都是可重复的对象。它们是可重复_的容器_，您可以从中获取一个可调器。

<font _mstmutation="1" _msthash="104312" _msttexthash="136553391">所有这些对象都有一个用于获取数据器的方法：</font>```iter()```

### 例子

从元组返回一个数据器，并打印每个值：
```
 mytuple = ("apple", "banana", "cherry")
myit = iter(mytuple)

print(next(myit))
print(next(myit))
print(next(myit)) 

```

甚至字符串都是可重复的对象，可以返回一个串：

### 例子

字符串也是可重复的对象，包含一系列字符：
```
 mystr = "banana"
myit = iter(mystr)

print(next(myit))
print(next(myit))
print(next(myit))
print(next(myit))
print(next(myit))
print(next(myit)) 

```

* * *

## 循环通过迭代器

<font _mstmutation="1" _msthash="103909" _msttexthash="109479825">我们还可以使用循环来迭代可迭代对象：</font>```for```

### 例子

迭代元组的值：
```
 mytuple = ("apple", "banana", "cherry")

for x in mytuple:
  print(x)

```

### 例子

迭代字符串的字符：
```
 mystr = "banana"

for x in mystr:
  print(x)

```

<font _mstmutation="1" _msthash="104494" _msttexthash="261964248">循环实际上创建一个迭代器对象，并为每个循环执行下一个（） 方法。</font>```for```

* * *

* * *

## 创建数据器

<font _mstmutation="1" _msthash="104091" _msttexthash="155861329">若要将对象/类创建为活动器，必须实现方法和对象。</font>```__iter__()``` ```__next__()```

<font _mstmutation="1" _msthash="104286" _msttexthash="548540174">正如您在 Python[类/对象章节中学到的，](python_classes.asp)所有类都有一个名为 的函数，它允许您在创建对象时执行一些初始化。</font>```__init__()```

<font _mstmutation="1" _msthash="104481" _msttexthash="364848068">该方法的行为类似，可以执行操作（初始化等），但必须始终返回数据器对象本身。</font>```__iter__()```

<font _mstmutation="1" _msthash="104676" _msttexthash="179450128">该方法还允许您执行操作，并且必须返回序列中的下一项。</font>```__next__()```

### 例子

创建一个返回数字的器，从 1 开始，每个序列将增加 1（返回 1，2，3，4，5 等）：
```
 class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    x = self.a
    self.a += 1
    return x

myclass = MyNumbers()
myiter = iter(myclass)

print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))

```

* * *

## 停止使用

<font _mstmutation="1" _msthash="105651" _msttexthash="327624076">如果有足够的下一个（） 语句，或者它在循环中使用，则上述示例将永远继续。</font>```for```

<font _mstmutation="1" _msthash="104078" _msttexthash="134884607">为了防止迭代永远继续下去，我们可以使用 语句。</font>```StopIteration```

<font _mstmutation="1" _msthash="104273" _msttexthash="279980571">在 方法中，如果迭代执行指定次数，我们可以添加终止条件以引发错误：</font>```__next__()```

### 例子

20 次迭代后停止：
```
 class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    if self.a <= 20:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration

myclass = MyNumbers()
myiter = iter(myclass)

for x in myiter:
  print(x) 

```


