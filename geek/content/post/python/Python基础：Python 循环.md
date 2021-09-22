
---
title: Python基础：Python 循环
author: 知识铺
date: 2020-10-25 18:50:04+08:00
tags: [python]
---
# Python 循环



## Python 循环

Python 有两个基元循环命令：

*   while loops
*   for loops

* * *

## while 循环

使用while 循环，我们可以执行一组语句，只要条件为 true。

### 例子

打印 i 只要 i 小于 6：
```
 i = 1
while i < 6:
  print(i)
  i += 1 

```

**注意：**请记住增加 i，否则循环将永远继续。

while 循环需要相关变量准备就绪，在此示例中，我们需要定义一个索引变量i，我们将其设置为 1。

* * *

## 中断语句

使用break 语句，我们可以停止循环，即使 while 条件为 true：

### 例子

当 i 为 3 时退出循环：
```
 i = 1
while i < 6:
  print(i)
  if i == 3:
    break
  i += 1

```

* * *

* * *

## 继续声明

使用continue 语句，我们可以停止当前迭代，并继续下一个：

### 例子

如果 i 为 3，请继续下一次迭代：
```
 i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i) 

```

* * *

## 其他语句

使用else 语句，当条件不再为 true 时，我们可以运行一次代码块：

### 例子

条件为 false 后打印消息：
```
 i = 1
while i < 6:
  print(i)
  i += 1
else:
  print("i is no longer less than 6") 

```



