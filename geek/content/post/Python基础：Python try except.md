
---
title: Python基础：Python try except
author: 知识铺
date: 2020-10-25 20:03:01+08:00
tags: [python]
---
# Python try except


<font _mstmutation="1" _msthash="95082" _msttexthash="68617809">该块允许您测试代码块的错误。</font>```try```

<font _mstmutation="1" _msthash="95264" _msttexthash="41269397">该块允许您处理错误。</font>```except```

<font _mstmutation="1" _msthash="95446" _msttexthash="150649486">该块允许您执行代码，而不管 try- 和除块的结果如何。</font>```finally```

* * *

## 异常处理

当发生错误或我们称之为异常时，Python 通常会停止并生成错误消息。

<font _mstmutation="1" _msthash="104117" _msttexthash="66581866">可以使用 语句处理这些异常：</font>```try```

### 例子

<font _mstmutation="1" _msthash="220701" _msttexthash="68980002">块将生成异常，因为未定义：</font>```try``````x```
```
 try:
  print(x)
except:
  print("An exception occurred")

```

由于 try 块引发错误，因此将执行除块。

如果没有 try 块，程序将崩溃并引发错误：

### 例子

<font _mstmutation="1" _msthash="221364" _msttexthash="88395801">此语句将引发错误，因为未定义：</font>```x```
```
 print(x)

```

* * *

## 许多例外

您可以定义尽可能多的异常块，例如，如果要为特殊错误执行特殊代码块：

### 例子

<font _mstmutation="1" _msthash="220467" _msttexthash="134509440">如果 try 块引发其他错误，请打印一条消息：</font>```NameError```
```
 try:
  print(x)
except NameError:
  print("Variable x is not defined")
except:
  print("Something else went wrong")

```

* * *

* * *

## 还

<font _mstmutation="1" _msthash="105469" _msttexthash="187710419">如果未引发错误，可以使用 关键字定义要执行的代码块：</font>```else```

### 例子

<font _mstmutation="1" _msthash="220233" _msttexthash="88489635">在此示例中，块不生成任何错误：</font>```try```
```
 try:
  print("Hello")
except:
  print("Something went wrong")
else:
  print("Nothing went wrong")

```

* * *

## 最后

<font _mstmutation="1" _msthash="104676" _msttexthash="215018271">如果指定了该块，则无论 try 块是否引发错误，都将执行该块。</font>```finally```

### 例子

 try:
```  print(x)
except:
  print("Something went wrong")
finally:
  print("The 'try except' is finished")

```

这对于关闭对象和清理资源非常有用：

### 例子

尝试打开并写入不可写入的文件：
```
 try:
  f = open("demofile.txt")
  f.write("Lorum Ipsum")
except:
  print("Something went wrong when writing to the file")
finally:
  f.close()

```

程序可以继续，而不会使文件对象保持打开状态。

* * *

## 引发异常

作为 Python 开发人员，您可以选择在出现异常时引发异常。

<font _mstmutation="1" _msthash="104663" _msttexthash="123020131">若要引发（或引发）异常，请使用 关键字。</font>```raise```

### 例子

如果 x 低于 0，则引发错误并停止程序：
```
 x = -1

if x < 0:
  raise Exception("Sorry, no numbers below zero")

```

<font _mstmutation="1" _msthash="105053" _msttexthash="34489455">关键字用于引发异常。</font>```raise```

您可以定义要引发的错误，以及要打印给用户的文本。

### 例子

如果 x 不是整数，请引发类型Error：
```
 x = "hello"

if not type(x) is int:
  raise TypeError("Only integers are allowed")

```


