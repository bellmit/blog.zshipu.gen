
---
title: Python基础：Python tuples
author: 知识铺
date: 2020-10-25 16:31:24+08:00
tags: [python]
---
# Python tuples


* * *

## tuples

tuples组是有序且不可**更改的集合**。在 Python tuples对中，用圆形括号书写。

### 例子

创建tuples组：
```

 thistuple = ("apple", "banana", "cherry")
print(thistuple)

```

* * *

## 访问tuples组项目

您可以通过引用方括号内的索引号来访问tuples组项：

### 例子

打印tuples组中的第二个项目：
```

 thistuple = ("apple", "banana", "cherry")
print(thistuple[1])

```

### 负索引

<font _mstmutation="1" _msthash="104507" _msttexthash="170143324">负索引表示从末尾开始，指最后一项，指最后一项等。</font>```-1 -2```

### 例子

打印tuples组的最后一项：
```

 thistuple = ("apple", "banana", "cherry")
print(thistuple[-1])

```

### 索引范围

可以通过指定开始地点和结束范围来指定索引范围。

指定范围时，返回值将是包含指定项的新tuples组。

### 例子

返回第三、第四和第五项：
```

 thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[2:5])

```

**注：**搜索将从索引 2（包括）开始，到索引 5（不包括）结束。

请记住，第一个项目具有索引 0。

### 负索引范围

如果要从tuples组末尾开始搜索，请指定负索引：

### 例子

本示例将项从索引 -4（包括）返回到索引 -1（排除）
```

 thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[-4:-1])

```

* * *

* * *

## 更改tuples组值

创建tuples组后，不能更改其值。tuples对tuples**是不变的，**或**不可变的**，因为它也被称为。

但有一个解决方法。您可以将tuples组转换为列表，更改列表，并将列表转换回tuples组。

### 例子

将tuples组转换为列表以便能够更改它：
```

 x = ("apple", "banana", "cherry")
y = list(x)
y[1] = "kiwi"
x = tuple(y)

print(x)

```

* * *

## 循环通过tuples组

<font _mstmutation="1" _msthash="105651" _msttexthash="50901149">可以使用循环遍历tuples组项。</font>```for```

### 例子

通过项目迭代并打印值：
```

 thistuple = ("apple", "banana", "cherry")
for x in thistuple:
  print(x)

```

<font _mstmutation="1" _msthash="104273" _msttexthash="197941380">您将在我们的 Python For 循环章节[中了解有关循环](python_for_loops.asp)的详细了解。</font>```for```

* * *

## 检查项目是否存在

<font _mstmutation="1" _msthash="105053" _msttexthash="160593134">若要确定tuples组中是否存在指定项，请使用 关键字：</font>```in```

### 例子

检查tuples组中是否存在"苹果"：
```

 thistuple = ("apple", "banana", "cherry")
if "apple" in thistuple:
  print("Yes, 'apple' is in the fruits tuple")

```

* * *

## tuples组长度

<font _mstmutation="1" _msthash="104260" _msttexthash="122451875">若要确定tuples组包含的项数，请使用 方法：</font>```len()```

### 例子

打印tuples组中的项目数：
```

 thistuple = ("apple", "banana", "cherry")
print(len(thistuple))

```

* * *

## 添加项目

创建tuples组后，不能向tuples组添加项目。tuples是**不变的**。

### 例子

不能将项添加到tuples组：
```

 thistuple = ("apple", "banana", "cherry")
thistuple[3] = "orange" # This will raise an error print(thistuple)

```

* * *

## 使用一个项目创建tuples组

若要创建只有一个项的tuples组，您必须在项后添加逗号，否则 Python 不会将其识别为tuples组。

### 例子

一个项目tuples组，记住组合：
```

 thistuple = ("apple",)
print(type(thistuple))

#NOT a tuple thistuple = ("apple")
print(type(thistuple))

```

* * *

## 删除项目

**注：**不能删除tuples组中的项目。

tuples组是**不可更改的**，因此您不能从tuples组中删除项目，但可以完全删除tuples组：

### 例子

<font _mstmutation="1" _msthash="222404" _msttexthash="59578857">关键字可以完全删除tuples组：</font>```del```
```

 thistuple = ("apple", "banana", "cherry")
del thistuple
print(thistuple)  #this will raise an error because the tuple no longer exists

```

* * *

## 加入两个tuples

<font _mstmutation="1" _msthash="104819" _msttexthash="122368285">要加入两个或多个tuples，您可以使用运算符：</font>```+```

### 例子

加入两个tuples：
```

 tuple1 = ("a", "b" , "c")
tuple2 = (1, 2, 3)

tuple3 = tuple1 + tuple2
print(tuple3)

```

* * *

## tuples组（） 构造函数

也可以使用tuples组（） 构造函数来制作tuples组。

### 例子

使用tuples组（） 方法创建tuples组：
```

 thistuple = tuple(("apple", "banana", "cherry")) # note the double round-brackets print(thistuple)

```

* * *


