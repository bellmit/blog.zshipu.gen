
---
title: Python基础：Python 阵列
author: 知识铺
date: 2020-10-25 19:08:45+08:00
tags: [python]
---
# Python 阵列


**注：**Python 没有对数组的内置支持，但可以使用 Python列表。

* * *

## 阵 列

**注：**本页演示如何使用列表作为 ARRAYS，但是，要使用 Python 中的数组，您必须导入库，如NumPy 库。

数组用于在单个变量中存储多个值：

### 例子

创建包含车名的数组：
```
 cars = ["Ford", "Volvo", "BMW"]

```

* * *

## 什么是阵列？

数组是一个特殊的变量，一次可以容纳多个值。

如果您有项目列表（例如汽车名称列表），则将汽车存储在单个变量中可能看起来像这样：

  car1 = "Ford"
car2 = "Volvo"
car3 = "BMW" 

但是，如果你想通过汽车循环，并找到一个特定的呢？如果你没有3辆车，但是300辆车呢？

解决方案是一个数组！

数组可以在单个名称下保存多个值，并且可以通过引用索引号来访问这些值。

* * *

## 访问数组的元素

通过引用索引号 来引用数组_元素_。

### 例子

获取第一个数组项的值：
```
 x = cars[0]

```

### 例子

修改第一个数组项的值：
```
 cars[0] = "Toyota"

```

* * *

## 数组的长度

<font _mstmutation="1" _msthash="104091" _msttexthash="145205528">使用 方法返回数组的长度（数组中的元素数）。</font>```len()```

### 例子

<font _mstmutation="1" _msthash="220675" _msttexthash="48508226">返回数组中的元素数：</font>```cars```
```
 x = len(cars)

```

**注：**数组的长度始终比最高数组索引多一个。

* * *

* * *

## 循环数组元素

<font _mstmutation="1" _msthash="104078" _msttexthash="77180454">可以使用 循环遍历数组的所有元素。</font>```for in```

### 例子

<font _mstmutation="1" _msthash="220662" _msttexthash="48857406">打印数组中的每一项：</font>```cars```
```
 for x in cars:
  print(x)

```

* * *

## 添加数组元素

<font _mstmutation="1" _msthash="105053" _msttexthash="71703996">可以使用 方法将元素添加到数组中。</font>```append()```

### 例子

<font _mstmutation="1" _msthash="221767" _msttexthash="50664133">向数组再添加一个元素：</font>```cars```
```
 cars.append("Honda")

```

* * *

## 删除数组元素

<font _mstmutation="1" _msthash="104260" _msttexthash="67509572">可以使用 方法从数组中删除元素。</font>```pop()```

### 例子

<font _mstmutation="1" _msthash="220870" _msttexthash="54623751">删除数组的第二个元素：</font>```cars```
```
 cars.pop(1)

```

<font _mstmutation="1" _msthash="104650" _msttexthash="75659961">还可以使用 方法从数组中删除元素。</font>```remove()```

### 例子

删除值为"沃尔沃"的元素：
```
 cars.remove("Volvo")

```

<font _mstmutation="1" _msthash="221260" _msttexthash="112112156">**注：**列表的方法仅删除指定值的第一次出现。</font>```remove()```

* * *


