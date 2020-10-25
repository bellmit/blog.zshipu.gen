
---
title: Python基础：Python Json
author: 知识铺
date: 2020-10-25 19:44:06+08:00
tags: [python]
---
# Python Json

JSON 是一种用于存储和交换数据的语法。

JSON 是文本，使用 JavaScript 对象表示法编写。

* * *

## Python 中的 Json

<font _mstmutation="1" _msthash="103727" _msttexthash="133907332">Python 有一个名为 的内置包，可用于处理 JSON 数据。</font>```json```

### 例子

导入 json 模块：
```
 import json
```
* * *

## 解析 Json - 从 Json 转换为 Python

<font _mstmutation="1" _msthash="104702" _msttexthash="111690982">如果您有 JSON 字符串，可以使用 方法分析它。</font>```json.loads()```

结果将是[Python字典](python_dictionaries.asp)。

### 例子

从 JSON 转换为 Python：
```
 import json

# some JSON: x =  '{ "name":"John", "age":30, "city":"New York"}'

# parse x: y = json.loads(x)

# the result is a Python dictionary: print(y["age"])

```

* * *

## 从 Python 转换为 JSON

<font _mstmutation="1" _msthash="104104" _msttexthash="171363764">如果您有 Python 对象，可以使用 方法将其转换为 JSON 字符串。</font>```json.dumps()```

### 例子

从 Python 转换为 JSON：
```
 import json

# a Python object (dict): x = {
  "name": "John",
  "age": 30,
  "city": "New York"
}

# convert into JSON: y = json.dumps(x)

# the result is a JSON string: print(y)

```

* * *

* * *

您可以将以下类型的 Python 对象转换为 JSON 字符串：

*   命令
*   列表
*   元
*   字符串
*   Int
*   浮动
*   真
*   假
*   没有

### 例子

将 Python 对象转换为 JSON 字符串，并打印值：
```
 import json

print(json.dumps({"name": "John", "age": 30}))
print(json.dumps(["apple", "bananas"]))
print(json.dumps(("apple", "bananas")))
print(json.dumps("hello"))
print(json.dumps(42))
print(json.dumps(31.76))
print(json.dumps(True))
print(json.dumps(False))
print(json.dumps(None))

```

* * *

当您从 Python 转换为 JSON 时，Python 对象将转换为 JSON （JavaScript） 等效项：

| Python | JSON |
| dict | Object |
| list | Array |
| tuple | Array |
| str | String |
| int | Number |
| float | Number |
| True | true |
| False | false |
| None | null |

* * *

### 例子

转换包含所有合法数据类型的 Python 对象：
```
 import json

x = {
  "name": "John",
  "age": 30,
  "married": True,
  "divorced": False,
  "children": ("Ann","Billy"),
  "pets": None,
  "cars": [
    {"model": "BMW 230", "mpg": 27.5},
    {"model": "Ford Edge", "mpg": 24.1}
  ]
}

print(json.dumps(x)) 

```

* * *

## 设置结果的格式

上面的示例打印一个 JSON 字符串，但它不是很容易读懂，没有缩进和换行符。

<font _mstmutation="1" _msthash="104663" _msttexthash="114052991">该方法具有参数，以便更容易读取结果：</font>```json.dumps()```

### 例子

<font _mstmutation="1" _msthash="221325" _msttexthash="48186788">使用 参数定义缩进数：</font>```indent```
```
 json.dumps(x, indent=4) 

```

您还可以定义分隔符，默认值是 （"，""，"："），这意味着使用逗号和空格分隔每个对象，以及冒号和空格来分隔键和值：

### 例子

<font _mstmutation="1" _msthash="221767" _msttexthash="66406795">使用 参数更改默认分隔符：</font>```separators```
```
 json.dumps(x, indent=4, separators=(". ", " = ")) 

```

* * *

## 订购结果

<font _mstmutation="1" _msthash="104260" _msttexthash="173101149">该方法具有参数，用于对结果中的键进行顺序排列：</font>```json.dumps()```

### 例子

<font _mstmutation="1" _msthash="220870" _msttexthash="101057749">使用 参数指定是否应对结果进行排序：</font>```sort_keys```
```
 json.dumps(x, indent=4, sort_keys=True) 

```


