
---
title: Python基础：Python字符串
author: 知识铺
date: 2020-10-25 14:42:57+08:00
tags: [python]
---
# Python字符串


* * *

## 字符串

python 中的字符串文本由单个引号或双引号包围。

"你好"和'你好'是一样的。

<font _mstmutation="1" _msthash="95628" _msttexthash="94136627">您可以使用 以下函数显示字符串文本：</font>```print()```

### 例子
```
 print("Hello")
print('Hello')

```

* * *

## 将字符串分配给变量

将字符串分配给变量使用变量名称后跟一个等号和字符串完成：

### 例子
```
 a = "Hello"
print(a)

```

* * *

## 多行字符串

可以使用三个引号将多行字符串分配给变量：

### 例子

您可以使用三个双引号：
```
 a = """Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua."""
print(a)

```

或三个单引号：

### 例子
```
 a = '''Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua.'''
print(a)

```

**注意：**在结果中，换行符插入的位置与代码中的位置相同。

* * *

* * *

## 字符串是数组

与许多其他流行的编程语言一样，Python 中的字符串是表示单码字符的字节数组。

但是，Python 没有字符数据类型，单个字符只是长度为 1 的字符串。

方括号可用于访问字符串的元素。

### 例子

获取位置 1 的字符（请记住，第一个字符具有位置 0）：
```
 a = "Hello, World!"
print(a[1])

```

## 切片

可以使用切片语法返回字符范围。

指定开始索引和结束索引（由冒号分隔）以返回字符串的一部分。

### 例子

获取字符从位置 2 到位置 5（不包括）：
```
 b = "Hello, World!"
print(b[2:5])

```

## 负索引

<font _mstmutation="1" _msthash="46592" _msttexthash="87787986">使用负索引从字符串末尾开始切片：</font>

### 例子

获取从位置 5 到位置 1（不包括）的字符，从字符串末尾开始计数：
```
 b = "Hello, World!"
print(b[-5:-2])

```

## 字符串长度

<font _mstmutation="1" _msthash="104273" _msttexthash="95584996">若要获取字符串的长度，请使用 函数。</font>```len()```

### 例子

<font _mstmutation="1" _msthash="220883" _msttexthash="55911609">函数返回字符串的长度：</font>```len()```
```
 a = "Hello, World!"
print(len(a))

```

* * *

## 字符串方法

Python 有一组内置方法，可用于字符串。

### 例子

<font _mstmutation="1" _msthash="221988" _msttexthash="90284428">该方法从开头或末尾删除任何空白：</font>```strip()```
```
 a = " Hello, World! "
print(a.strip()) # returns "Hello, World!"

```

### 例子

<font _mstmutation="1" _msthash="222209" _msttexthash="59573930">该方法以小写返回字符串：</font>```lower()```
```
 a = "Hello, World!"
print(a.lower())

```

### 例子

<font _mstmutation="1" _msthash="222430" _msttexthash="53283893">该方法返回大写字符串：</font>```upper()```
```
 a = "Hello, World!"
print(a.upper())

```

### 例子

<font _mstmutation="1" _msthash="220649" _msttexthash="83363397">方法将字符串替换为另一个字符串：</font>```replace()```
```
 a = "Hello, World!"
print(a.replace("H", "J"))

```

### 例子

<font _mstmutation="1" _msthash="220870" _msttexthash="201983249">如果该方法找到分隔符的实例，则将字符串拆分为子字符串：</font>```split()```
```
 a = "Hello, World!"
print(a.split(",")) # returns ['Hello', ' World!']

```

使用字符串方法参考了解有关[字符串方法的详细了解](python_ref_string.asp)

* * *

## 检查字符串

<font _mstmutation="1" _msthash="105430" _msttexthash="198585764">要检查字符串中是否存在某个短语或字符，可以使用关键字或 。</font>```in``````not in```

### 例子

检查以下文本中是否存在短语"ain"：
```
 txt = "The rain in Spain stays mainly in the plain"
x = "ain" in txt
print(x)

```

### 例子

检查以下文本中是否不存在短语"ain"：
```
 txt = "The rain in Spain stays mainly in the plain"
x = "ain" not in txt
print(x) 

```

* * *

## 字符串串联

若要连接或组合两个字符串，可以使用 + 运算符。

### 例子

<font _mstmutation="1" _msthash="221520" _msttexthash="60170422">将变量与变量合并为变量 ：</font>```a``````b``````c```
```
 a = "Hello"
b = "World"
c = a + b
print(c)

```

### 例子

<font _mstmutation="1" _msthash="221741" _msttexthash="102438232">若要在它们之间添加空格，请添加 ：</font>```" "```
```
 a = "Hello"
b = "World"
c = a + " " + b
print(c)

```

* * *

## 字符串格式

正如我们在 Python 变量章节中学到的，我们不能像这样组合字符串和数字：

### 例子
```
 age = 36
txt = "My name is John, I am " + age
print(txt)

```

<font _mstmutation="1" _msthash="104624" _msttexthash="147303312">但是，我们可以通过使用 方法组合字符串和数字！</font>```format()```

<font _mstmutation="1" _msthash="104819" _msttexthash="292480695">该方法采用传递的参数，设置它们格式，并将它们放在占位符的字符串中：</font>```format()``````{}```

### 例子

<font _mstmutation="1" _msthash="221507" _msttexthash="70163301">使用 方法将数字插入字符串中：</font>```format()```
```
 age = 36
txt = "My name is John, and I am {}"
print(txt.format(age))

```

format（） 方法采用无限数量的参数，并放置在相应的占位符中：

### 例子
```
 quantity = 3
itemno = 567
price = 49.95
myorder = "I want {} pieces of item {} for {} dollars."
print(myorder.format(quantity, itemno, price))

```

<font _mstmutation="1" _msthash="105599" _msttexthash="152177090">您可以使用索引号确保参数放置在正确的占位符中：</font>```{0}```

### 例子
```
 quantity = 3
itemno = 567
price = 49.95
myorder = "I want to pay {2} dollars for {0} pieces of item {1}."
print(myorder.format(quantity, itemno, price))

```

* * *

## 转义字符

若要在字符串中插入非法字符，请使用转义字符。

<font _mstmutation="1" _msthash="105001" _msttexthash="101991279">转义字符是反斜杠，后跟要插入的字符。</font>```\```

非法字符的示例是字符串内的双引号，该字符串由双引号包围：

### 例子

如果在字符串内使用双引号，则出现错误：使用双引号：
```
 txt = "We are the so-called "Vikings" from the north."

```

<font _mstmutation="1" _msthash="105586" _msttexthash="1350661">To fix this problem, use the escape character :</font>```\"```

### Example
```
The escape character allows you to use double quotes when you normally would not be allowed:

 txt = "We are the so-called \"Vikings\" from the north."

```

Python 中使用的其他转义字符：

| Code | Result |
| \' | Single Quote | 
| \\ | Backslash | 
| \n | New Line | 
| \r | Carriage Return | 
| \t | Tab | 
| \b | Backspace | 
| \f | Form Feed |  |
| \ooo | Octal value | 
| \xhh | Hex value | 

* * *

## 字符串方法

Python 有一组内置方法，可用于字符串。

**注：**所有字符串方法都返回新值。它们不会更改原始字符串。

| Method | Description |
| [capitalize()](ref_string_capitalize.asp) | Converts the first character to upper case |
| [casefold()](ref_string_casefold.asp) | Converts string into lower case |
| [center()](ref_string_center.asp) | Returns a centered string |
| [count()](ref_string_count.asp) | Returns the number of times a specified value occurs in a string |
| [encode()](ref_string_encode.asp) | Returns an encoded version of the string |
| [endswith()](ref_string_endswith.asp) | Returns true if the string ends with the specified value |
| [expandtabs()](ref_string_expandtabs.asp) | Sets the tab size of the string |
| [find()](ref_string_find.asp) | Searches the string for a specified value and returns the position of where it was found |
| [format()](ref_string_format.asp) | Formats specified values in a string |
| format_map() | Formats specified values in a string |
| [index()](ref_string_index.asp) | Searches the string for a specified value and returns the position of where it was found |
| [isalnum()](ref_string_isalnum.asp) | Returns True if all characters in the string are alphanumeric |
| [isalpha()](ref_string_isalpha.asp) | Returns True if all characters in the string are in the alphabet |
| [isdecimal()](ref_string_isdecimal.asp) | Returns True if all characters in the string are decimals |
| [isdigit()](ref_string_isdigit.asp) | Returns True if all characters in the string are digits |
| [isidentifier()](ref_string_isidentifier.asp) | Returns True if the string is an identifier |
| [islower()](ref_string_islower.asp) | Returns True if all characters in the string are lower case |
| [isnumeric()](ref_string_isnumeric.asp) | Returns True if all characters in the string are numeric |
| [isprintable()](ref_string_isprintable.asp) | Returns True if all characters in the string are printable |
| [isspace()](ref_string_isspace.asp) | Returns True if all characters in the string are whitespaces |
| [istitle()](ref_string_istitle.asp) | Returns True if the string follows the rules of a title |
| [isupper()](ref_string_isupper.asp) | Returns True if all characters in the string are upper case |
| [join()](ref_string_join.asp) | Joins the elements of an iterable to the end of the string |
| [ljust()](ref_string_ljust.asp) | Returns a left justified version of the string |
| [lower()](ref_string_lower.asp) | Converts a string into lower case |
| [lstrip()](ref_string_lstrip.asp) | Returns a left trim version of the string |
| [maketrans()](ref_string_maketrans.asp) | Returns a translation table to be used in translations |
| [partition()](ref_string_partition.asp) | Returns a tuple where the string is parted into three parts |
| [replace()](ref_string_replace.asp) | Returns a string where a specified value is replaced with a specified value |
| [rfind()](ref_string_rfind.asp) | Searches the string for a specified value and returns the last position of where it was found |
| [rindex()](ref_string_rindex.asp) | Searches the string for a specified value and returns the last position of where it was found |
| [rjust()](ref_string_rjust.asp) | Returns a right justified version of the string |
| [rpartition()](ref_string_rpartition.asp) | Returns a tuple where the string is parted into three parts |
| [rsplit()](ref_string_rsplit.asp) | Splits the string at the specified separator, and returns a list |
| [rstrip()](ref_string_rstrip.asp) | Returns a right trim version of the string |
| [split()](ref_string_split.asp) | Splits the string at the specified separator, and returns a list |
| [splitlines()](ref_string_splitlines.asp) | Splits the string at line breaks and returns a list |
| [startswith()](ref_string_startswith.asp) | Returns true if the string starts with the specified value |
| [strip()](ref_string_strip.asp) | Returns a trimmed version of the string |
| [swapcase()](ref_string_swapcase.asp) | Swaps cases, lower case becomes upper case and vice versa |
| [title()](ref_string_title.asp) | Converts the first character of each word to upper case |
| [translate()](ref_string_translate.asp) | Returns a translated string |
| [upper()](ref_string_upper.asp) | Converts a string into upper case |
| [zfill()](ref_string_zfill.asp) | Fills the string with a specified number of 0 values at the beginning |

* * *


