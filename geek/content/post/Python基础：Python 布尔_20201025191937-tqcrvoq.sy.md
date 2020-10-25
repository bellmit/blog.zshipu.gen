---
title: Python基础：Python 布尔
author: 知识铺
date: 2020-10-25 14:44:34+08:00
tags: [python]
---

# Python 布尔

<font _mstmutation="1" _msthash="95082" _msttexthash="51765441">布尔表示两个值之一： 或 。</font>``True``````False``

---

## 布尔值

<font _mstmutation="1" _msthash="103532" _msttexthash="108692454">在编程中，您经常需要知道表达式是 或 。</font>``True``````False``

<font _mstmutation="1" _msthash="103727" _msttexthash="220713454">您可以计算 Python 中的任何表达式，并获取两个答案之一，或 。</font>``True``````False``

比较两个值时，将计算表达式，Python 返回布尔答案：

### 例子

```
 print(10 > 9)
print(10 == 9)
print(10 < 9)

```

<font _mstmutation="1" _msthash="104312" _msttexthash="108135599">在 if 语句中运行条件时，Python 返回 或 ：</font>``True``````False``

### 例子

<font _mstmutation="1" _msthash="220922" _msttexthash="64810096">根据条件是 或 ： 打印消息：</font>``True``````False``

```
 a = 200
b = 33

if b > a:
  print("b is greater than a")
else:
  print("b is not greater than a")

```

---

## 评估值和变量

<font _mstmutation="1" _msthash="105287" _msttexthash="127500932">函数允许您计算任何值，并给出或作为回报，</font>``bool()``````True``````False``

### 例子

评估字符串和数字：

```
 print(bool("Hello"))
print(bool(15)) 

```

### 例子

评估两个变量：

```
 x = "Hello"
y = 15

print(bool(x))
print(bool(y)) 

```

---

---

## 大多数值都为 True

<font _mstmutation="1" _msthash="105274" _msttexthash="104658684">几乎任何值都计算为，如果它有某种内容。</font>``True``

<font _mstmutation="1" _msthash="105469" _msttexthash="77166479">任何字符串都是 ，空字符串除外。</font>``True``

<font _mstmutation="1" _msthash="103896" _msttexthash="43936204">任何数字都是 ，除了 。</font>``True``````0``

<font _mstmutation="1" _msthash="104091" _msttexthash="129295036">任何列表、元组、集和字典都是 ，除了空列表。</font>``True``

### 例子

以下将返回 True：

```
 bool("abc")
bool(123)
bool(["apple", "cherry", "banana"]) 

```

---

## 某些值为 false

<font _mstmutation="1" _msthash="105066" _msttexthash="353589782">实际上，除空值（如 、、、数字和 值）外，计算 到 的值没有很多。当然，值会评估到 。</font>``False``````()``````[]``````{}``````""``````0``````None``````False``````False``

### 例子

以下内容将返回 False：

```
 bool(False)
bool(None)
bool(0)
bool("")
bool(())
bool([])
bool({})

```

<font _mstmutation="1" _msthash="105456" _msttexthash="10508667">One more value, or object in this case, evaluates to , and that is if you have an object that is made from a class with a function that returns or :</font> ``False``````__len__``````0``````False``

### Example

```
 class myclass():
  def __len__(self):
    return 0

myobj = myclass()
print(bool(myobj))

```

---

## 函数可以返回布尔

您可以创建返回布尔值的函数：

### 例子

打印函数的答案：

```
 def myFunction() :
  return True

print(myFunction())

```

您可以根据函数的布尔答案执行代码：

### 例子

如果函数返回 True，则打印"是！"

```
 def myFunction() :
  return True

if myFunction():
  print("YES!")
else:
  print("NO!")

```

<font _mstmutation="1" _msthash="105443" _msttexthash="543756681">Python 还具有许多内置函数，这些函数返回布尔值，如函数，可用于确定对象是否具有特定数据类型：</font>``isinstance()``

### 例子

检查对象是否为整数：

```
 x = 200
print(isinstance(x, int))

```

---
