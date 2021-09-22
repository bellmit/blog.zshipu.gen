
---
title: Python基础：Python sets
author: 知识铺
date: 2020-10-25 17:10:41+08:00
tags: [python]
---
# Python sets


* * *

## 设置

 sets是无序和未编制索引的 sets合。在 Python 中， sets用大括号编写。

### 例子

创建 sets：
```
 thisset = {"apple", "banana", "cherry"}
print(thisset)

```

**注：** sets是无序的，因此您无法确定项目按什么顺序显示。

* * *

## 访问项目

不能通过引用索引或键来访问 sets合中的项。

<font _mstmutation="1" _msthash="104312" _msttexthash="284631412">但是，您可以使用 循环遍历 sets项，或使用 关键字询问 sets合中是否存在指定值。</font>```for in```

### 例子

循环浏览 sets，并打印值：
```
 thisset = {"apple", "banana", "cherry"}

for x in thisset:
  print(x)

```

### 例子

检查套装中是否存在"香蕉"：
```
 thisset = {"apple", "banana", "cherry"}

print("banana" in thisset)

```

* * *

## 更改项目

创建 sets后，不能更改其项，但可以添加新项。

* * *

## 添加项目

<font _mstmutation="1" _msthash="104494" _msttexthash="94360604">要将一个项添加到 sets合，请使用 方法。</font>```add()```

<font _mstmutation="1" _msthash="104689" _msttexthash="94145714">要向 sets合中添加多个项，请使用 方法。</font>```update()```

### 例子

<font _mstmutation="1" _msthash="221351" _msttexthash="56269447">使用 方法将项添加到 sets：</font>```add()```
```
 thisset = {"apple", "banana", "cherry"}

thisset.add("orange")

print(thisset)

```

### 例子

<font _mstmutation="1" _msthash="221572" _msttexthash="68754881">使用 方法将多个项添加到 sets：</font>```update()```
```
 thisset = {"apple", "banana", "cherry"}

thisset.update(["orange", "mango", "grapes"])

print(thisset)

```

* * *

* * *

## 获取 sets的长度

<font _mstmutation="1" _msthash="104676" _msttexthash="90317240">若要确定 sets有多少项，请使用 方法。</font>```len()```

### 例子

获取 sets合中的项目数：
```
 thisset = {"apple", "banana", "cherry"}

print(len(thisset))

```

* * *

## 删除项目

<font _mstmutation="1" _msthash="105651" _msttexthash="98516223">若要删除 sets合中的项，请使用 或 方法。</font>```remove() discard()```

### 例子

<font _mstmutation="1" _msthash="220441" _msttexthash="44295758">使用以下方法删除"香蕉"</font>```remove()```

```
 thisset = {"apple", "banana", "cherry"}

thisset.remove("banana")

print(thisset)

```

<font _mstmutation="1" _msthash="220389" _msttexthash="119573740">**注：**如果要删除的项不存在，将引发错误。</font>```remove()```

### 例子

<font _mstmutation="1" _msthash="220883" _msttexthash="44295758">使用以下方法删除"香蕉"</font>```discard()```
```
 thisset = {"apple", "banana", "cherry"}

thisset.discard("banana")

print(thisset)

```

<font _mstmutation="1" _msthash="220831" _msttexthash="133593473">**注：**如果要删除的项不存在，则**不会**引发错误。</font>```discard()```

<font _mstmutation="1" _msthash="104858" _msttexthash="547805661">还可以使用 的方法删除项，但此方法将删除最后一_个_项。请记住， sets是无序的，因此您将不知道删除的项。</font>```pop()```

<font _mstmutation="1" _msthash="105053" _msttexthash="59768072">方法的返回值是已删除的项。</font>```pop()```

### 例子

<font _mstmutation="1" _msthash="221767" _msttexthash="67856399">使用 以下方法删除最后一项：</font>```pop()```
```
 thisset = {"apple", "banana", "cherry"}

x =  thisset.pop()

print(x)

print(thisset)

```

<font _mstmutation="1" _msthash="221715" _msttexthash="234059176">**注：** sets_是无序的_，所以当使用 方法时，您将不知道哪个项被删除。</font>```pop()```

### 例子

<font _mstmutation="1" _msthash="222209" _msttexthash="34430058">该方法清空 sets：</font>```clear()```

```
 thisset = {"apple", "banana", "cherry"}

thisset.clear()

print(thisset)

```

### 例子

<font _mstmutation="1" _msthash="222430" _msttexthash="1271530">The keyword will delete the set completely:</font>```del```
```
 thisset = {"apple", "banana", "cherry"}

del  thisset

print(thisset)

```

* * *

## 加入两组

有几种方法可以在 Python 中加入两个或多个 sets。

<font _mstmutation="1" _msthash="105040" _msttexthash="489446334">可以使用返回包含两个 sets中所有项的新 sets的方法，也可以使用将一个 sets的所有项插入另一个 sets的方法：</font>```union()``````update()```

### 例子

<font _mstmutation="1" _msthash="221754" _msttexthash="114337977">该方法返回包含两个 sets中所有项的新 sets：</font>```union()```
```
 set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

set3 = set1.union(set2)
print(set3)

```

### 例子

<font _mstmutation="1" _msthash="221975" _msttexthash="62797124">该方法将 set2 中的项插入 set1：</font>```update()```
```
 set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

set1.update(set2)
print(set1)

```

<font _mstmutation="1" _msthash="221923" _msttexthash="55210415">**注：**和 将排除任何重复项。</font>```union()  update()```

还有其他方法连接两个 sets，只保留重复项，或从不复制，检查本页底部的 sets方法的完整列表。

* * *

##  sets（） 构造函数

也可以使用set（） 构造函数进行设置。

### 例子

使用 set（） 构造函数进行设置：
```
 thisset = set(("apple", "banana", "cherry")) # note the double round-brackets print(thisset)

```



* * *


