
---
title: Python基础：Python 作用域
author: 知识铺
date: 2020-10-25 19:36:45+08:00
tags: [python]
---
# Python 作用域


变量仅从创建它的地区内部可用。这称为** 作用域**。

* * *

## 本地 作用域

在函数内创建的变量属于_该函数的_本地 作用域，只能在该函数内使用。

### 例子

在函数内创建的变量在函数内可用：
```
 def myfunc():
  x = 300
  print(x)

myfunc()

```

### 函数内函数

<font _mstmutation="1" _msthash="104117" _msttexthash="263337074">如上例所述，该变量在函数之外不可用，但它可用于函数内的任何函数：</font>```x```

### 例子

可以从函数中的函数访问本地变量：
```
 def myfunc():
  x = 300
  def myinnerfunc():
    print(x)
  myinnerfunc()

myfunc()

```

* * *

* * *

## 全局 作用域

在 Python 代码的主体中创建的变量是全局变量，属于全局 作用域。

全局变量可从任何 作用域内、全局变量和本地变量获得。

### 例子

在函数外部创建的变量是全局变量，任何人都可以使用：
```
 x = 300

def myfunc():
  print(x)

myfunc()

print(x)

```

### 命名变量

如果使用函数内外的相同变量名进行操作，Python 会将它们视为两个单独的变量，一个在全局作用域中可用（在函数外部），另一个在本地作用域（函数内部）中可用：

### 例子

<font _mstmutation="1" _msthash="221351" _msttexthash="106839668">函数将打印本地 ，然后代码将打印全局：</font>```x``````x```
```
 x = 300

def myfunc():
  x = 200
  print(x)

myfunc()

print(x)

```

* * *

## 全局关键字

<font _mstmutation="1" _msthash="103896" _msttexthash="213225194">如果需要创建全局变量，但卡在本地作用域中，可以使用 关键字。</font>```global```

<font _mstmutation="1" _msthash="104091" _msttexthash="53519934">关键字使变量成为全局变量。</font>```global```

### 例子

<font _mstmutation="1" _msthash="220675" _msttexthash="111699263">如果使用 关键字，则变量属于全局 作用域：</font>```global```
```
 def myfunc():
  global x
  x = 300

myfunc()

print(x)

```

<font _mstmutation="1" _msthash="104481" _msttexthash="165256143">此外，如果要更改函数内的全局变量，请使用 关键字。</font>```global```

### 例子

<font _mstmutation="1" _msthash="221117" _msttexthash="193821628">若要更改函数内全局变量的值，请使用 关键字引用变量：</font>```global```
```
 x = 300

def myfunc():
  global x
  x = 200

myfunc()

print(x)

```


