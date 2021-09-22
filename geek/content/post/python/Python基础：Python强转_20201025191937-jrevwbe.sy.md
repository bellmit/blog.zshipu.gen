---
title: Python基础：Python强转
author: 知识铺
date: 2020-10-25 14:39:17+08:00
tags: [python]
---

# Python强转

---

## 指定变量类型

有时可能需要为变量指定类型。这可以通过强转完成。Python 是一种面向对象的语言，因此它使用类来定义数据类型，包括其基元类型。

因此，使用构造函数在 python 中强制转换：

* int（） - 从整数文本、浮数字（通过向下舍入到上一个整数）或字符串文本（提供字符串表示整数）构造整数数字）
* float（） - 从整数文本、浮点文本或字符串文本构造浮点数（提供字符串表示浮点或整数）
* str（） - 从各种数据类型构造字符串，包括字符串、整数文本和浮法文本

### 例子

整数：

```
 x = int(1)   # x will be 1 y = int(2.8) # y will be 2 z = int("3") # z will be 3 

```

### 例子

浮：

```
 x = float(1)     # x will be 1.0 y = float(2.8)   # y will be 2.8 z = float("3")   # z will be 3.0 w = float("4.2") # w will be 4.2 

```

### 例子

字符串：

```
 x = str("s1") # x will be 's1' y = str(2)    # y will be '2' z = str(3.0)  # z will be '3.0'

```
