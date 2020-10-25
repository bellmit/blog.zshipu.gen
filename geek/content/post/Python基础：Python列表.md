
---
title: Python基础：Python列表
author: 知识铺
date: 2020-10-25 16:28:55+08:00
tags: [python]
---
# Python列表


* * *

## Python 集合（数组）

Python 编程语言有四种集合数据类型：

*   **列表**是一个有序且可更改的集合。允许重复的成员。
*   **元组**是一个有序且不可更改的集合。允许重复的成员。
*   **Set**是无序和未编制索引的集合。没有重复的成员。
*   **字典**是无序、可更改和索引的集合。没有重复的成员。

选择集合类型时，了解该类型的属性非常有用。为特定数据集选择正确的类型可能意味着保留意义，并且可能意味着效率或安全性的提高。

## 列表

列表是有序且可更改的集合。在 Python 列表中用方括号编写。

### 例子

创建列表：
```

 thislist = ["apple", "banana", "cherry"]
print(thislist)

```

* * *

## 访问项目

通过引用索引号来访问列表项：

### 例子

打印列表的第二个项目：
```

 thislist = ["apple", "banana", "cherry"]
print(thislist[1])

```

### 负索引

<font _mstmutation="1" _msthash="105287" _msttexthash="170143324">负索引表示从末尾开始，指最后一项，指最后一项等。</font>```-1 -2```

### 例子

打印列表的最后一项：
```

 thislist = ["apple", "banana", "cherry"]
print(thislist[-1])

```

### 索引范围

可以通过指定开始地点和结束范围来指定索引范围。

指定范围时，返回值将是具有指定项的新列表。

### 例子

返回第三、第四和第五项：
```

 thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(thislist[2:5])

```

**注：**搜索将从索引 2（包括）开始，到索引 5（不包括）结束。

请记住，第一个项目具有索引 0。

通过删除开始值，范围将从第一项开始：

### 例子

此示例返回从开头到"橙色"的项：
```

 thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(thislist[:4])

```

通过删除结束值，范围将转到列表的末尾：

### 例子

此示例返回从"樱桃"和末尾的项目：
```

 thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(thislist[2:])

```

### 负索引范围

如果要从列表末尾开始搜索，请指定负索引：

### 例子

本示例将项从索引 -4（包括）返回到索引 -1（排除）
```

 thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(thislist[-4:-1])

```

* * *

## 更改项目值

<font _mstmutation="1" _msthash="46592" _msttexthash="103790973">要更改特定项的值，请参阅索引号：</font>

### 例子

更改第二个项目：
```

 thislist = ["apple", "banana", "cherry"]
thislist[1] = "blackcurrant"
print(thislist)

```

* * *

* * *

## 循环浏览列表

<font _mstmutation="1" _msthash="104858" _msttexthash="63861577">可以使用循环遍历列表项：</font>```for```

### 例子

打印列表中的所有项目，一个：
```

 thislist = ["apple", "banana", "cherry"]
for x in thislist:
  print(x)

```

<font _mstmutation="1" _msthash="105248" _msttexthash="197941380">您将在我们的 Python For 循环章节中了解有关循环的详细了解。</font>```for```

* * *

## 检查项目是否存在

<font _mstmutation="1" _msthash="104260" _msttexthash="161008458">若要确定列表中是否存在指定项，请使用 关键字：</font>```in```

### 例子

检查列表中是否存在"苹果"：
```

 thislist = ["apple", "banana", "cherry"]
if "apple" in thislist:
  print("Yes, 'apple' is in the fruits list")

```

* * *

## 列表长度

<font _mstmutation="1" _msthash="105235" _msttexthash="135525221">若要确定列表包含的项数，请使用 以下函数：</font> ```len()```

### 例子

打印列表中的项目数：
```

 thislist = ["apple", "banana", "cherry"]
print(len(thislist))

```

* * *

## 添加项目

若要将项添加到列表的末尾，请使用追加（）方法：

### 例子

<font _mstmutation="1" _msthash="221079" _msttexthash="38692940">使用 方法追加项：</font>```append()```
```

 thislist = ["apple", "banana", "cherry"]
thislist.append("orange")
print(thislist)

```

若要在指定的索引下添加项，请使用insert（）方法：

### 例子

将项目作为第二个位置插入：
```

 thislist = ["apple", "banana", "cherry"]
thislist.insert(1, "orange")
print(thislist)

```

* * *

## 删除项目

有几种方法可以从列表中删除项目：

### 例子

<font _mstmutation="1" _msthash="222625" _msttexthash="52100373">该方法删除指定的项：</font>```remove()```
```

 thislist = ["apple", "banana", "cherry"]
thislist.remove("banana")
print(thislist)

```

### 例子

<font _mstmutation="1" _msthash="222846" _msttexthash="255432372">该方法删除指定的索引（如果未指定索引，则删除最后一项）：</font>```pop()```
```

 thislist = ["apple", "banana", "cherry"]
thislist.pop()
print(thislist)

```

### 例子

<font _mstmutation="1" _msthash="221065" _msttexthash="56025502">关键字删除指定的索引：</font>```del```
```

 thislist = ["apple", "banana", "cherry"]
del thislist[0]
print(thislist)

```

### 例子

<font _mstmutation="1" _msthash="221286" _msttexthash="68422926">关键字还可以完全删除列表：</font>```del```
```

 thislist = ["apple", "banana", "cherry"]
del thislist

```

### 例子

<font _mstmutation="1" _msthash="221507" _msttexthash="38437568">该方法清空列表：</font>```clear()```
```

 thislist = ["apple", "banana", "cherry"]
thislist.clear()
print(thislist)

```

* * *

## 复制列表

<font _mstmutation="1" _msthash="105794" _msttexthash="399017047">您不能简单地通过键入 来复制列表，因为 ： 将_仅引用_，并且 中所做的更改也会自动在 中进行。</font>```list2 = list1``````list2``````list1``````list1``````list2```

<font _mstmutation="1" _msthash="105989" _msttexthash="146287102">有一种方法可以复制，一种方法是使用内置的 List 方法。</font> ```copy()```

### 例子

<font _mstmutation="1" _msthash="222833" _msttexthash="51478583">使用 以下方法复制列表：</font>```copy()```
```

 thislist = ["apple", "banana", "cherry"]
mylist = thislist.copy()
print(mylist)

```

<font _mstmutation="1" _msthash="106379" _msttexthash="89438154">制作副本的另一种方法是使用内置方法。</font>```list()```

### 例子

<font _mstmutation="1" _msthash="221273" _msttexthash="51478583">使用 以下方法复制列表：</font>```list()```
```

 thislist = ["apple", "banana", "cherry"]
mylist = list(thislist)
print(mylist)

```

* * *

## 加入两个列表

有几种方法可以在 Python 中加入或串联两个或多个列表。

<font _mstmutation="1" _msthash="105781" _msttexthash="71163287">最简单的方法之一是使用运算符。</font>```+```

### 例子

加入两个列表：
```

 list1 = ["a", "b" , "c"]
list2 = [1, 2, 3]

list3 = list1 + list2
print(list3)

```

加入两个列表的另一种方式是将列表 2 中的所有项目附加到列表 1 中，一个附加：

### 例子

将列表2追加到列表1：
```

 list1 = ["a", "b" , "c"]
list2 = [1, 2, 3]

for x in list2:
  list1.append(x)

print(list1)

```

<font _mstmutation="1" _msthash="106561" _msttexthash="275704923">或者可以使用 方法，该方法的目的是将元素从一个列表添加到另一个列表：</font>```extend()```

### 例子

<font _mstmutation="1" _msthash="221481" _msttexthash="73824855">使用 方法在列表 1 的末尾添加 list2：</font>```extend()```
```

 list1 = ["a", "b" , "c"]
list2 = [1, 2, 3]

list1.extend(list2)
print(list1)

```

* * *

## 列表（） 构造函数

还可以使用list（） 构造函数来制作新列表。

### 例子

<font _mstmutation="1" _msthash="222586" _msttexthash="53691794">使用构造函数创建列表：</font>```list()```
```

 thislist = list(("apple", "banana", "cherry")) # note the double round-brackets print(thislist)

```

* * *



