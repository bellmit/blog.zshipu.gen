
---
title: Python基础：Python user input 接收
author: 知识铺
date: 2020-10-25 20:04:39+08:00
tags: [python]
---
# Python user input 接收

## user_input

Python 允许用户输入。

这意味着我们可以向用户请求输入。

在 Python 3.6 中，该方法与 Python 2.7 方法略有不同。

<font _mstmutation="1" _msthash="103532" _msttexthash="36380149">Python 3.6 使用该方法。</font>```input()```

<font _mstmutation="1" _msthash="103727" _msttexthash="36380175">Python 2.7 使用该方法。</font>```raw_input()```

下面的示例要求使用用户名，当您输入用户名时，它会在屏幕上打印出来：

### Python 3.6
```
 username = input("Enter username:")
print("Username is: " + username) 

```

### Python 2.7
```
 username = raw_input("Enter username:")
print("Username is: " + username) 

```

<font _mstmutation="1" _msthash="220649" _msttexthash="222019408">Python 在函数时停止执行，并在用户提供某些输入时继续执行。</font>```input()```

