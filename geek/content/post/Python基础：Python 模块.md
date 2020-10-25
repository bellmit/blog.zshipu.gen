
---
title: Python基础：Python 模块
author: 知识铺
date: 2020-10-25 19:38:23+08:00
tags: [python]
---
# Python 模块



## 什么是模块？

将模块视为与代码库相同。

包含要在应用程序中包含的一组函数的文件。

* * *

## 创建模块

<font _mstmutation="1" _msthash="103922" _msttexthash="220897157">若要创建模块，只需将要保存的代码保存在文件扩展名的文件中：</font>```.py```

### 例子

<font _mstmutation="1" _msthash="220480" _msttexthash="29522922">将此代码保存在名为</font>```mymodule.py```
```
 def greeting(name):
  print("Hello, " + name)

## 使用模块

<font _mstmutation="1" _msthash="104507" _msttexthash="172829462">现在，我们可以使用刚刚创建的模块，使用以下语句：</font>```import```

### 例子

导入名为 my 模块的模块，然后调用问候语函数：
```
 import mymodule

mymodule.greeting("Jonathan")

```

**注：**使用模块中的函数时，请使用语法_：module_name.函数名称_。

* * *

## 模块中的变量

该模块可以包含已描述的函数，但也包含所有类型的变量（数组、字典、对象等）：

### 例子

<font _mstmutation="1" _msthash="220467" _msttexthash="34536554">将此代码保存在文件中</font>```mymodule.py```
```
 person1 = {
  "name": "John",
  "age": 36,
  "country": "Norway"
}

### 例子

导入名为 my 模块的模块，然后访问人员词典：
```
 import mymodule

a = mymodule.person1["age"]
print(a)

```

* * *

* * *

## 命名模块

<font _mstmutation="1" _msthash="103896" _msttexthash="111787182">您可以命名模块文件，但必须具有文件扩展名</font>```.py```

## 重新命名模块

<font _mstmutation="1" _msthash="104286" _msttexthash="114656295">可以使用 以下关键字在导入模块时创建别名：</font>```as```

### 例子

<font _mstmutation="1" _msthash="220896" _msttexthash="34071999">为 调用 创建别名：</font>```mymodule``````mx```
```
 import mymodule as mx

a = mx.person1["age"]
print(a)

```

* * *

## 内置模块

Python 中有几个内置模块，您可以随时导入这些模块。

### 例子

<font _mstmutation="1" _msthash="222001" _msttexthash="33679477">导入和使用模块：</font>```platform```
```
 import platform

x = platform.system()
print(x)

[自己试试 |](trypython.asp?filename=demo_module4)

* * *

## 使用 dir（） 函数

<font _mstmutation="1" _msthash="104468" _msttexthash="271833029">有一个内置函数来列出模块中的所有函数名称（或变量名称）。功能：</font>```dir()```

### 例子

列出属于平台模块的所有定义名称：
```
 import platform

x = dir(platform)
print(x)

[自己试试 |](trypython.asp?filename=demo_module5)

**注：**dir（） 函数可用于所有_模块，_也可以用于您自己创建模块。

* * *

## 从模块导入

<font _mstmutation="1" _msthash="105638" _msttexthash="96148884">您可以使用 关键字选择仅从模块导入零件。</font>```from```

### 例子

<font _mstmutation="1" _msthash="222430" _msttexthash="79794351">名为的模块有一个函数和一个字典：</font>```mymodule```
```
 def greeting(name):
  print("Hello, " + name)

person1 = {
  "name": "John",
  "age": 36,
  "country": "Norway"
} 

### 例子

仅从模块导入人员 1 字典：
```
 from mymodule import person1

print (person1["age"]) 

```

<font _mstmutation="1" _msthash="220597" _msttexthash="297814543">**注：**使用 关键字导入时，在引用模块中的元素时不要使用模块名称。示例： 、**不**</font>```from``````person1["age"]``` ```~~mymodule.person1["age"]~~```


