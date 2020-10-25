---
title: Python基础：Python词典
author: 知识铺
date: 2020-10-25 17:12:47+08:00
tags: [python]
---

# Python词典

## 字典

字典是无序、可更改和索引的集合。在 Python 字典中，用大括号编写，它们具有键和值。

### 例子

创建和打印字典：

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
print(thisdict) 

```

---

## 访问项目

您可以通过引用字典的键名称（方括号内）来访问字典的项：

### 例子

获取"模型"键的值：

```
 x = thisdict["model"] 

```

<font _mstmutation="1" _msthash="104312" _msttexthash="165601930">还有一种称为方法，该方法将为您提供相同的结果：</font>``get()``

### 例子

获取"模型"键的值：

```
 x = thisdict.get("model") 

```

---

---

## 更改值

可以通过引用特定项的键名称来更改其值：

### 例子

将"年"更改为 2018 年：

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict["year"] = 2018 

```

---

## 循环浏览字典

<font _mstmutation="1" _msthash="105079" _msttexthash="40206218">可以使用循环遍历字典。</font>``for``

在循环字典时，返回值_是字典_的键，但也有方法_可以返回_这些值。

### 例子

打印字典中的所有键名称，一个打印：

```
 for x in thisdict:
  print(x)

```

### 例子

打印字典_中_的所有值，一个个：

```
 for x in thisdict:
  print(thisdict[x])

```

### 例子

<font _mstmutation="1" _msthash="220454" _msttexthash="73317062">还可以使用 方法返回字典的值：</font>``values()``

```
 for x in thisdict.values():
  print(x)

```

### 例子

<font _mstmutation="1" _msthash="220675" _msttexthash="48237345">使用 方法_遍__历键_和值 ，</font>``items()``

```
 for x, y in thisdict.items():
  print(x, y)

```

---

## 检查密钥是否存在

<font _mstmutation="1" _msthash="105066" _msttexthash="159531476">要确定字典中是否存在指定的键，请使用 关键字：</font>``in``

### 例子

检查字典中是否存在"模型"：

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
if "model" in thisdict:
  print("Yes, 'model' is one of the keys in the thisdict dictionary")

```

---

## 字典长度

<font _mstmutation="1" _msthash="104273" _msttexthash="171307474">若要确定字典包含的项数（键值对），请使用 函数。</font>``len()``

### 例子

打印字典中的项目数：

```
 print(len(thisdict))

```

---

## 添加项目

通过使用新的索引键为其分配值，可以将项添加到字典中：

### 例子

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict["color"] = "red"
print(thisdict) 

```

---

## 删除项目

有几种方法可以从字典中删除项目：

### 例子

<font _mstmutation="1" _msthash="221091" _msttexthash="89837748">该方法删除具有指定键名称的项：</font>``pop()``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.pop("model")
print(thisdict)

```

### 例子

<font _mstmutation="1" _msthash="221312" _msttexthash="327359773">该方法删除最后一个插入的项目（在 3.7 之前的版本中，将删除随机项）：</font>``popitem()``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.popitem()
print(thisdict)

```

### 例子

<font _mstmutation="1" _msthash="221533" _msttexthash="89215776">关键字删除具有指定键名称的项：</font>``del``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
del thisdict["model"]
print(thisdict)

```

### 例子

<font _mstmutation="1" _msthash="221754" _msttexthash="65655278">关键字还可以完全删除字典：</font>``del``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
del thisdict
print(thisdict) #this will cause an error because "thisdict" no longer exists.

```

### 例子

<font _mstmutation="1" _msthash="221975" _msttexthash="36430160">该方法清空字典：</font>``clear()``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.clear()
print(thisdict)

```

---

## 复制字典

<font _mstmutation="1" _msthash="104442" _msttexthash="377693823">您不能仅仅通过键入来复制字典，因为 ：_将仅引用_，并且 中所做的更改也会自动在 中进行。</font>``dict2 = dict1    dict2    dict1    dict1    dict2``

<font _mstmutation="1" _msthash="104637" _msttexthash="139486464">有办法制作副本，一种方法是使用内置的字典方法。</font> ``copy()``

### 例子

<font _mstmutation="1" _msthash="221299" _msttexthash="49015031">使用以下方法复制字典：</font>``copy()``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
mydict = thisdict.copy()
print(mydict)

```

<font _mstmutation="1" _msthash="105027" _msttexthash="86693867">制作副本的另一种方式是使用内置函数。</font>``dict()``

### 例子

<font _mstmutation="1" _msthash="221741" _msttexthash="49120721">使用以下功能复制字典：</font>``dict()``

```
 thisdict =  {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
mydict = dict(thisdict)
print(mydict)

```

---

## 嵌套词典

字典也可以包含许多字典，这称为嵌套词典。

### 例子

创建包含三个字典的字典：

```
 myfamily = {
  "child1" : {
    "name" : "Emil",
    "year" : 2004
  },
  "child2" : {
    "name" : "Tobias",
    "year" : 2007
  },
  "child3" : {
    "name" : "Linus",
    "year" : 2011
  }
}

```

或者，如果要嵌套三个已作为字典存在的字典：

### 例子

创建三个字典，然后创建一个包含其他三个字典的字典：

```
 child1 = {
  "name" : "Emil",
  "year" : 2004
}
child2 = {
  "name" : "Tobias",
  "year" : 2007
}
child3 = {
  "name" : "Linus",
  "year" : 2011
}

myfamily = {
  "child1" : child1,
  "child2" : child2,
  "child3" : child3
}

```

---

## 命令（） 构造函数

也可以使用dict（）构造函数来制作新字典：

### 例子

```
 thisdict = dict(brand="Ford", model="Mustang", year=1964)
# note that keywords are not string literals # note the use of equals rather than colon for the assignment print(thisdict) 

```
