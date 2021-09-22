
---
title: Python基础：Python Regx 正则表达式 
author: 知识铺
date: 2020-10-25 19:47:09+08:00
tags: [python]
---
# Python RegEx


RegEx 或正则表达式是组成搜索模式的字符序列。

RegEx 可用于检查字符串是否包含指定的搜索模式。

* * *

## 正则表达式模块

<font _mstmutation="1" _msthash="103727" _msttexthash="167684608">Python 有一个名为 的内置包，可用于使用正则表达式。</font>```re```

<font _mstmutation="1" _msthash="103922" _msttexthash="19734117">导入模块：</font>```re```

 import re

* * *

## Python 中的 RegEx

<font _mstmutation="1" _msthash="104897" _msttexthash="111968259">导入模块后，可以开始使用正则表达式：</font>```re```

### 例子

搜索字符串以查看其是否以"The"开头，以"西班牙"结尾：
```
 import re

txt = "The rain in Spain"
x = re.search("^The.*Spain$", txt)

```

* * *

## 正则表达式功能

<font _mstmutation="1" _msthash="104104" _msttexthash="210956720">该模块提供了一组函数，允许我们搜索字符串以寻找匹配项：</font>```re```

| Function | Description |
| [findall](#findall) | Returns a list containing all matches |
| [search](#search) | Returns a [Match object](#matchobject) if there is a match anywhere in the string |
| [split](#split) | Returns a list where the string has been split at each match |
| [sub](#sub) | Replaces one or many matches with a string |

* * *

* * *

## 元字符

元字符是具有特殊含义的字符：

| Character | Description | Example |
| [] | A set of characters | "[a-m]" | 
| \ | Signals a special sequence (can also be used to escape special characters) | "\d" | 
| . | Any character (except newline character) | "he..o" | 
| ^ | Starts with | "^hello" | 
| $ | Ends with | "world$" | 
| * | Zero or more occurrences | "aix*" | 
| + | One or more occurrences | "aix+" | 
| {} | Exactly the specified number of occurrences | "al{2}" | 
| | | Either or | "falls|stays" | 
| () | Capture and group |   |   |

* * *

## 特殊序列

<font _mstmutation="1" _msthash="104871" _msttexthash="170342380">特殊序列后跟以下列表中的一个字符，具有特殊含义：</font>```\```

| Character | Description | Example |
| \A | Returns a match if the specified characters are at the beginning of the string | "\AThe" | 
| \b | Returns a match where the specified characters are at the beginning or at the end of a word
(the "r" in the beginning is making sure that the string is being treated as a "raw string") | r"\bain"
r"ain\b" | 

| \B | Returns a match where the specified characters are present, but NOT at the beginning (or at the end) of a word
(the "r" in the beginning is making sure that the string is being treated as a "raw string") | r"\Bain"
r"ain\B" | 

| \d | Returns a match where the string contains digits (numbers from 0-9) | "\d" | 
| \D | Returns a match where the string DOES NOT contain digits | "\D" | 
| \s | Returns a match where the string contains a white space character | "\s" | 
| \S | Returns a match where the string DOES NOT contain a white space character | "\S" | 
| \w | Returns a match where the string contains any word characters (characters from a to Z, digits from 0-9, and the underscore _ character) | "\w" | 
| \W | Returns a match where the string DOES NOT contain any word characters | "\W" | 
| \Z | Returns a match if the specified characters are at the end of the string | "Spain\Z" | 

* * *

## 集

<font _mstmutation="1" _msthash="104078" _msttexthash="162328530">一组是一对方括号内的一组字符，具有特殊的含义：</font> ```[]```

| Set | Description |
| [arn] | Returns a match where one of the specified characters (```a```, ```r```, or ```n```) are present | 
| [a-n] | Returns a match for any lower case character, alphabetically between ```a``` and ```n``` | 
| [^arn] | Returns a match for any character EXCEPT ```a```, ```r```, and ```n``` | 
| [0123] | Returns a match where any of the specified digits (```0```, ```1```, ```2```, or ```3```) are present | 
| [0-9] | Returns a match for any digit between ```0``` and ```9``` | 
| [0-5][0-9] | Returns a match for any two-digit numbers from ```00``` and ```59``` | 
| [a-zA-Z] | Returns a match for any character alphabetically between ```a``` and ```z```, lower case OR upper case | 
| [+] | In sets, ```+```, ```*```, ```.```, ```|```, ```()```, ```$```,```{}``` has no special meaning, so ```[+]``` means: return a match for any ```+``` character in the string | 

* * *

 <a name="findall"> </a>

## findall （） 函数

<font _mstmutation="1" _msthash="105248" _msttexthash="72503743">函数返回包含所有匹配项的列表。</font>```findall()```

### 例子

打印所有匹配项的列表：
```
 import re

txt = "The rain in Spain"
x = re.findall("ai", txt)
print(x)

```

该列表包含按其找到顺序显示的匹配项。

如果未找到匹配项，则返回空列表：

### 例子

如果未找到匹配项，请返回空列表：
```
 import re

txt = "The rain in Spain"
x = re.findall("Portugal", txt)
print(x)

```

* * *

 <a name="search"> </a>

## 搜索（） 函数

<font _mstmutation="1" _msthash="105235" _msttexthash="194355824">函数搜索字符串以寻找匹配项，并在有[匹配项时](#matchobject)返回 Match 对象。</font>```search()```

如果有多个匹配项，则只返回匹配项的第一个匹配项：

### 例子

搜索字符串中的第一个空白字符：
```
 import re

txt = "The rain in Spain"
x = re.search("\s", txt)

print("The first white-space character is located in position:", x.start())

```

<font _mstmutation="1" _msthash="105820" _msttexthash="93393196">如果未找到匹配项，则返回该值：</font>```None```

### 例子

进行不匹配的搜索：
```
 import re

txt = "The rain in Spain"
x = re.search("Portugal", txt)
print(x)

```

* * *

 <a name="split"> </a>

## 拆分（） 函数

<font _mstmutation="1" _msthash="105222" _msttexthash="179600928">函数返回一个列表，其中字符串已在每个匹配项上拆分：</font>```split()```

### 例子

在每个空白字符上拆分：
```
 import re

txt = "The rain in Spain"
x = re.split("\s", txt)
print(x)

```

<font _mstmutation="1" _msthash="105612" _msttexthash="97396585">您可以通过指定参数来控制发生次数：</font>```maxsplit```

### 例子

仅在第一次出现时拆分字符串：
```
 import re

txt = "The rain in Spain"
x = re.split("\s", txt, 1)
print(x)

```

* * *

 <a name="sub"> </a>

## 子（） 函数

<font _mstmutation="1" _msthash="105014" _msttexthash="93896894">函数将匹配项替换为您选择的文本：</font>```sub()```

### 例子

将每个空格字符替换为数字 9：
```
 import re

txt = "The rain in Spain"
x = re.sub("\s", "9", txt)
print(x)

```

<font _mstmutation="1" _msthash="105404" _msttexthash="88755108">您可以通过指定参数来控制替换数：</font>```count```

### 例子

替换前 2 个匹配项：
```
 import re

txt = "The rain in Spain"
x = re.sub("\s", "9", txt, 2)
print(x)

```

* * *

 <a name="matchobject"> </a>

## 匹配对象

匹配对象是包含有关搜索和结果的信息的对象。

<font _mstmutation="1" _msthash="221221" _msttexthash="179725260">**注：**如果没有匹配项，将返回该值，而不是匹配对象。</font>```None```

### 例子

进行将返回匹配对象的搜索：
```
 import re

txt = "The rain in Spain"
x = re.search("ai", txt)
print(x) #this will print an object

```

Match 对象具有用于检索有关搜索的信息以及结果的属性和方法：

```.span()```<font _mstmutation="1" _msthash="105586" _msttexthash="440211993">返回包含匹配的开始位置和结束位置的元组。
返回传递到函数中的
字符串返回有匹配项的字符串部分</font>```.string``````.group()```

### 例子

打印第一次匹配发生的位置（开始位置和结束位置）。

正则表达式寻找以大写"S"开头的任何单词：
```
 import re

txt = "The rain in Spain"
x = re.search(r"\bS\w+", txt)
print(**x.span()**)

```

### 例子

打印传递到函数中的字符串：
```
 import re

txt = "The rain in Spain"
x = re.search(r"\bS\w+", txt)
print(**x.string**)

```

### 例子

打印有匹配项的字符串部分。

正则表达式寻找以大写"S"开头的任何单词：
```
 import re

txt = "The rain in Spain"
x = re.search(r"\bS\w+", txt)
print(**x.group()**)

```


