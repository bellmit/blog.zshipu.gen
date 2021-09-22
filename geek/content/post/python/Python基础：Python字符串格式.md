
---
title: Python基础：Python字符串格式
author: 知识铺
date: 2020-10-25 20:05:49+08:00
tags: [python]
---
# Python字符串格式


<font _mstmutation="1" _msthash="95082" _msttexthash="309512073">若要确保字符串将像预期的那样显示，我们可以使用 方法对结果进行格式设置。</font>```format()```

* * *

## 字符串格式（）

<font _mstmutation="1" _msthash="103532" _msttexthash="94712488">该方法允许您格式化字符串的选定部分。</font>```format()```

有时，有些文本部分您无法控制，可能它们来自数据库，或者用户输入？

<font _mstmutation="1" _msthash="103922" _msttexthash="386324718">若要控制这些值，请添加文本中的占位符（卷曲括号），并通过 方法运行这些值：</font>```{}``````format()```

### 例子

在要显示价格的处位符：
```
 price = 49
txt = "The price is {} dollars"
print(txt.format(price))

```

您可以在大括号内添加参数，以指定如何转换值：

### 例子

将要显示为具有两个小数的数字格式化：
```
 txt = "The price is {:.2f} dollars" 

```

查看我们的字符串格式（）[引用的所有格式类型](ref_string_format.asp)。

* * *

## 多个值

如果要使用更多值，只需向 format（） 方法添加更多值：

 print(txt.format(price, itemno, count))

并添加更多占位符：

### 例子
```
 quantity = 3
itemno = 567
price = 49
myorder = "I want {} pieces of item number {} for {:.2f} dollars."
print(myorder.format(quantity, itemno, price))

```

* * *

## 索引号

<font _mstmutation="1" _msthash="105079" _msttexthash="289117816">您可以使用索引号（大括号内的数字）来确保将值放置在正确的占位符中：</font>```{0}```

### 例子
```
 quantity = 3
itemno = 567
price = 49
myorder = "I want {0} pieces of item number {1} for {2:.2f} dollars."
print(myorder.format(quantity, itemno, price))

```

此外，如果要多引用同一值，请使用索引号：

### 例子
```
 age = 36
name = "John"
txt = "His name is {1}. {1} is {0} years old."
print(txt.format(age, name))

```

* * *

## 命名索引

<font _mstmutation="1" _msthash="104676" _msttexthash="347735908">还可以通过在大括号中输入名称来使用命名索引，但在传递参数值时必须使用名称：</font>```{carname}``````txt.format(carname = "Ford")```

### 例子
```
 myorder = "I have a {carname}, it is a {model}."
print(myorder.format(carname = "Ford", model = "Mustang"))

```


