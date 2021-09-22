
---
title: Python基础：Python文件打开
author: 知识铺
date: 2020-10-25 20:23:38+08:00
tags: [python]
---
# Python文件打开

## 打开服务器上的文件

假设我们有以下文件，位于与 Python 相同的文件夹中：

test. txt
```
 Hello! Welcome to demofile.txt
This file is for testing purposes.
Good Luck!
```
<font _mstmutation="1" _msthash="95628" _msttexthash="74986028">若要打开文件，请使用内置函数。</font>```open()```

<font _mstmutation="1" _msthash="103532" _msttexthash="197682147">函数返回一个文件对象，该对象具有读取文件内容的方法：</font>```open()``````read()```

### 例子
```
 f = open("demofile.txt", "r")
print(f.read())

```

如果文件位于其他位置，则必须指定文件路径，具体内容为：

### 例子

打开其他位置的文件：
```
 f = open("D:\\myfiles\welcome.txt", "r")
print(f.read())

```

* * *

## 只读取文件的某些部分

<font _mstmutation="1" _msthash="104897" _msttexthash="270345114">默认情况下，该方法返回整个文本，但您也可以指定要返回的字符数：</font>```read()```

### 例子

返回文件的 5 个前字符：
```
 f = open("demofile.txt", "r")
print(f.read(**5**))

```

* * *

* * *

## 读取行

<font _mstmutation="1" _msthash="104689" _msttexthash="66326000">可以使用 以下方法返回一行：</font>```readline()```

### 例子

读取文件的一行：
```
 f = open("demofile.txt", "r")
print(f.readline())

```

<font _mstmutation="1" _msthash="105079" _msttexthash="97894836">通过调用两次，您可以读取前两行：</font>```readline()```

### 例子

读取文件的两行：
```
 f = open("demofile.txt", "r")
print(f.readline())
print(f.readline())

```

通过循环浏览文件的行，您可以一行一读整个文件：

### 例子

按行循环文件：
```
 f = open("demofile.txt", "r")
for x in f:
  print(x)

```

* * *

## 关闭文件

处理完文件后，始终关闭该文件是一种好的做法。

### 例子

完成文件后关闭该文件：
```
 f = open("demofile.txt", "r")
print(f.readline())
f.close()

```

**注：**在某些情况下，由于缓冲，应始终关闭文件，在关闭文件之前，可能不会显示对文件所做的更改。


