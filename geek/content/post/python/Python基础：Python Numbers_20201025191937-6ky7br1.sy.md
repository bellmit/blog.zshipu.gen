---
title: Python基础：Python Numbers
author: 知识铺
date: 2020-10-25 14:36:11+08:00
tags: [python]
---

# Python Numbers

---

## Python  Numbers

Python 中有三种数字类型：

* ``int``
* ``float``
* ``complex``

向数值分配值时，将创建数值类型的变量：

### 例子

```

 x = 1    # int y = 2.8  # float z = 1j   # complex 
```

<font _mstmutation="1" _msthash="103727" _msttexthash="185478917">若要验证 Python 中任何对象的类型，请使用 以下函数：</font>``type()``

### 例子

```

 print(type(x))
print(type(y))
print(type(z)) 

```

---

## Int

int 或整数是长度无限的整数，正数或负数。没有小数。

### 例子

整数：

```
 x = 1
y = 35656222554887711
z = -3255522

print(type(x))
print(type(y))
print(type(z))

```

---

## Float

浮动或"浮点数"是一个数字，正或负，包含一个或多个小数。

### 例子

浮：

```
 x = 1.10
y = 1.0
z = -35.59

print(type(x))
print(type(y))
print(type(z))

```

浮动也可以是科学数字与"e"，以指示10的功率。

### 例子

浮：

```
 x = 35e3
y = 12E4
z = -87.7e100

print(type(x))
print(type(y))
print(type(z))

```

---

---

## 复杂

复数以"j"作为虚部：

### 例子

```

复杂：

 x = 3+5j
y = 5j
z = -5j

print(type(x))
print(type(y))
print(type(z))

```

---

## 类型转换

<font _mstmutation="1" _msthash="105066" _msttexthash="132386267">可以使用 和 方法从一种类型转换为另一种类型：</font>``int()``````float()``````complex()``

### 例子

从一种类型转换为另一种类型：

```
 x = 1    # int y = 2.8  # float z = 1j   # complex 
#convert from int to float: a = float(x)

#convert from float to int: b = int(y)

#convert from int to complex: c = complex(x)

print(a)
print(b)
print(c)

print(type(a))
print(type(b))
print(type(c))

```

**注：**不能将复数转换为其他数字类型。

---

## 随机 Numbers

<font _mstmutation="1" _msthash="104468" _msttexthash="499767723">Python 没有用于生成随机数的函数，但 Python 具有一个称为内置模块的模块，可用于生成随机数：</font>``random()``````random``

### 例子

导入随机模块，并显示介于 1 和 9 之间的随机数：

```
 import random

print(random.randrange(1, 10))

```
