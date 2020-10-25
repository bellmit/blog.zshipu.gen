---
title: Python基础：Python变量
author: 知识铺
date: 2020-10-25 14:32:32+08:00
tags: [python]
---

# Python变量

---

## 创建变量

变量是用于存储数据值的容器。

与其他编程语言不同，Python 没有声明变量的命令。

变量在您首次为其分配值时创建。

### 例子

```
 x = 5
y = "John"
print(x)
print(y)

```

变量不需要用任何特定类型声明_，_甚至可以在设置后更改类型。

### 例子

```
 x = 4 # x is of type int x = "Sally" # x is now of type str print(x)

```

可以使用单引号或双引号声明字符串变量：

### 例子

```
 x = "John"
# is the same as x = 'John'

```

<font _mstmutation="1" _msthash="145678" _msttexthash="308127170">下一章将介绍有关数据类型（如（字符串）和（整数））的详细了解。</font>``str int``

---

## 变量名称

<font _mstmutation="1" _msthash="46592" _msttexthash="468090376">变量可以具有短名称（如 x 和 y）或更具描述性的名称（年龄、车名、total_volume）。Python 变量的规则：</font>

* 变量名称必须以字母或下划线字符开头
* 变量名称不能以数字为起点
* 变量名称只能包含字母数字字符和下划线（A-z、0-9 和 _ ）。
* 变量名称与大小写敏感（年龄、年龄和年龄是三个不同的变量）

### 例子

```
 #Legal variable names: myvar = "John"
my_var = "John"
_my_var = "John"
myVar = "John"
MYVAR = "John"
myvar2 = "John"

#Illegal variable names: 2myvar = "John"
my-var = "John"
my var = "John"

```

请记住，变量名称是大小写相关的

---

---

## 将值分配给多个变量

Python 允许您在一行中为多个变量分配值：

### 例子

```
 x, y, z = "Orange", "Banana", "Cherry"
print(x)
print(y)
print(z)

```

您可以在一行_中为_多个变量分配相同的值：

### 例子

```
 x = y = z = "Orange"
print(x)
print(y)
print(z)

```

---

## 输出变量

<font _mstmutation="1" _msthash="104871" _msttexthash="68331783">Python 语句通常用于输出变量。</font>``print``

<font _mstmutation="1" _msthash="105066" _msttexthash="121857645">若要合并文本和变量，Python 使用以下字符：</font>``+``

### 例子

```
 x = "awesome"
print("Python is " + x)

```

<font _mstmutation="1" _msthash="105456" _msttexthash="123209060">还可以使用该字符将变量添加到另一个变量：</font>``+``

### 例子

```
 x = "Python is "
y = "awesome"
z =  x + y
print(z)
```

<font _mstmutation="1" _msthash="104078" _msttexthash="91072020">对于数字，字符用作数学运算符：</font>

### 例子

```
 x = 5
y = 10
print(x + y)

```

如果尝试合并字符串和数字，Python 将为您提供错误：

### 例子

```
 x = 5
y = "John"
print(x + y)

```

---

## 全局变量

在函数外部创建的变量（如上述所有示例所示）称为全局变量。

全局变量可以由每个人使用，包括函数内部和外部。

### 例子

在函数外部创建变量，并在函数内使用它

```
 x = "awesome"

def myfunc():
  print("Python is " + x)

myfunc()

```

如果在函数内创建具有相同名称的变量，则此变量将是局部的，并且只能在函数内使用。同名的全局变量将保持原样、全局变量和原始值。

### 例子

在函数内创建变量，其名称与全局变量相同

```
 x = "awesome"

def myfunc():
  x = "fantastic"
  print("Python is " + x)

myfunc()

print("Python is " + x)

```

---

## 全局关键字

通常，在函数内创建变量时，该变量是局部的，只能在该函数内使用。

<font _mstmutation="1" _msthash="105430" _msttexthash="122599659">若要在函数内创建全局变量，可以使用 关键字。</font>``global``

### 例子

<font _mstmutation="1" _msthash="222196" _msttexthash="111699263">如果使用 关键字，则变量属于全局范围：</font>``global``

```
 def myfunc():
  global x
  x = "fantastic"

myfunc()

print("Python is " + x)

```

<font _mstmutation="1" _msthash="105820" _msttexthash="165256143">此外，如果要更改函数内的全局变量，请使用 关键字。</font>``global``

### 例子

<font _mstmutation="1" _msthash="222638" _msttexthash="193821628">若要更改函数内全局变量的值，请使用 关键字引用变量：</font>``global``

```
 x = "awesome"

def myfunc():
  global x
  x = "fantastic"

myfunc()

print("Python is " + x)

```
