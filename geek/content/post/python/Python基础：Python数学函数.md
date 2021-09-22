
---
title: Python基础：Python数学函数
author: 知识铺
date: 2020-10-25 19:41:55+08:00
tags: [python]
---
# Python数学函数



Python 有一组内置的数学函数，包括一个广泛的数学模块，允许您对数字执行数学任务。

* * *

## 内置数学函数

<font _mstmutation="1" _msthash="103532" _msttexthash="141053016">和 函数可用于查找可重复值中的最低值或最高值：</font>```min()``````max()```

### 例子
```
 x = min(5, 10, 25)
y = max(5, 10, 25)

print(x)
print(y)

```

<font _mstmutation="1" _msthash="103922" _msttexthash="108939948">函数返回指定数字的绝对（正）值：</font>```abs()```

### 例子
```

 x = abs(-7.25)
print(x)

```

<font _mstmutation="1" _msthash="104312" _msttexthash="82027465">函数将 x 的值返回到 y （x） 的功率</font>```pow(_x_, _y_)```<sup _msthash="229879" _msttexthash="8099">Y</sup><font _mstmutation="1" _msthash="104313" _msttexthash="8515">).</font>

### 例子

将值 4 返回到 3 的功率（与 4 * 4 * 4 相同）：
```
 x = pow(4, 3)

print(x)

```

* * *

## 数学模块

<font _mstmutation="1" _msthash="105287" _msttexthash="208283712">Python 还有一个内置模块，叫做 ，它扩展了数学函数的列表。</font>```math```

<font _mstmutation="1" _msthash="103714" _msttexthash="65855738">要使用它，必须导入模块：</font>```math```

 import math

<font _mstmutation="1" _msthash="104104" _msttexthash="120111849">导入模块后，可以开始使用模块的方法和常量。</font>```math```

<font _mstmutation="1" _msthash="104299" _msttexthash="79350349">例如，方法返回数字的平方根：</font>```math.sqrt()```

### 例子
```

 import math
x = math.sqrt(64)

print(x)

```

<font _mstmutation="1" _msthash="104689" _msttexthash="360487777">该方法向上舍入到最接近的整数，该方法向下舍入到其最近的整数，并返回结果：</font>```math.ceil()``````math.floor()```

### 例子
```

 import math
x = math.ceil(1.4)
y = math.floor(1.4)

print(x) # returns 2 print(y) # returns 1

```

<font _mstmutation="1" _msthash="105079" _msttexthash="86496371">常量，返回 PI 的值 （3.14...）：</font>```math.pi```

### 例子
```
 import math

x = math.pi

print(x)

```

* * *

## 完整的数学模块参考

在我们的数学模块参考中，您将找到属于数学模块的所有方法和常量的完整引用。


