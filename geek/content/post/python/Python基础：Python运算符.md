
---
title: Python基础：Python运算符
author: 知识铺
date: 2020-10-25 15:53:03+08:00
tags: [python]
---
# Python运算符



## Python 运算符

运算符用于对变量和值执行操作。

Python 将运算符分为以下组：

*   算术运算符
*   分配运算符
*   比较运算符
*   逻辑运算符
*   标识运算符
*   会员运算符
*   位运算符

* * *

## Python 算术运算符

算术运算符与数值一起使用，以执行常见的数学运算：

| Operator | Name | Example |
| + | Addition | x + y | 
| - | Subtraction | x - y | 
| * | Multiplication | x * y | 
| / | Division | x / y | 
| % | Modulus | x % y | 
| ** | Exponentiation | x ** y | 
| // | Floor division | x // y | 

* * *

## Python 分配运算符

赋值运算符用于将值分配给变量：

| Operator | Example | Same As |
| = | x = 5 | x = 5 | 
| += | x += 3 | x = x + 3 | 
| -= | x -= 3 | x = x - 3 | 
| *= | x *= 3 | x = x * 3 | 
| /= | x /= 3 | x = x / 3 | 
| %= | x %= 3 | x = x % 3 | 
| //= | x //= 3 | x = x // 3 | 
| **= | x **= 3 | x = x ** 3 | 
| &= | x &= 3 | x = x & 3 | 
| |= | x |= 3 | x = x | 3 | 
| ^= | x ^= 3 | x = x ^ 3 | 
| >>= | x >>= 3 | x = x >> 3 | 
| <<= | x <<= 3 | x = x << 3 | 

* * *

* * *

## Python 比较运算符

比较运算符用于比较两个值：

| Operator | Name | Example |
| == | Equal | x == y | 
| != | Not equal | x != y | 
| > | Greater than | x > y | 
| < | Less than | x < y | 
| >= | Greater than or equal to | x >= y | 
| <= | Less than or equal to | x <= y | 

* * *

## Python 逻辑运算符

逻辑运算符用于组合条件语句：

| Operator | Description | Example |
| and  | Returns True if both statements are true | x < 5 and  x < 10 | 
| or | Returns True if one of the statements is true | x < 5 or x < 4 | 
| not | Reverse the result, returns False if the result is true | not(x < 5 and x < 10) | 

* * *

## Python 标识运算符

标识运算符用于比较对象，而不是它们相等，但如果它们实际上是同一个对象，则具有相同的内存位置：

| Operator | Description | Example |
| is  | Returns True if both variables are the same object | x is y | 
| is not | Returns True if both variables are not the same object | x is not y | 

* * *

## Python 成员资格运算符

成员资格运算符用于测试对象中是否显示序列：

| Operator | Description | Example |
| in  | Returns True if a sequence with the specified value is present in the object | x in y | 
| not in | Returns True if a sequence with the specified value is not present in the object | x not in y | 

* * *

## Python 位运算符

位运算符用于比较（二进制）数字：

| Operator | Name | Description |
| &  | AND | Sets each bit to 1 if both bits are 1 |
| | | OR | Sets each bit to 1 if one of two bits is 1 |
|  ^ | XOR | Sets each bit to 1 if only one of two bits is 1 |
| ~  | NOT | Inverts all the bits |
| << | Zero fill left shift | Shift left by pushing zeros in from the right and let the leftmost bits fall off |
| >> | Signed right shift | Shift right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off |

* * *


