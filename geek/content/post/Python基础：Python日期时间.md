
---
title: Python基础：Python日期时间
author: 知识铺
date: 2020-10-25 19:39:52+08:00
tags: [python]
---
# Python日期时间



## Python 日期

<font _mstmutation="1" _msthash="95264" _msttexthash="431819869">Python 中的日期不是它自己的数据类型，但我们可以导入名为的模块，以将日期用作日期对象。</font>```datetime```

### 例子

导入日期时间模块并显示当前日期：
```
 import datetime

x = datetime.datetime.now()
print(x)

```

* * *

## 日期输出

当我们从上面的示例执行代码时，结果将是：

```<script>cc = "2018/05/06 09:30:20" var d = new Date(); var m = d.getMonth() + 1; if (m < 10) m = "0" + m var day = d.getDate(); if (day < 10) day = "0" + day; var h = d.getHours(); if (h < 10) h = "0" + h; var n = d.getMinutes(); if (n < 10) n = "0" + n; var s = d.getSeconds(); if (s < 10) s = "0" + s; var ms = d.getMilliseconds(); while (ms.toString().length < 3) { ms = "0" + ms; } var ex = Math.floor(Math.random() * 999); while (ex.toString().length < 3) { ex = "0" + ex; } var x = d.getFullYear() + "-" + m + "-" + day + " " + h + ":" + n + ":" + s + "." + ms + ex document.write(x);</script> 2020-10-25 19:38:28.884625```

日期包含年、月、日、小时、分钟、秒和微秒。

<font _mstmutation="1" _msthash="104507" _msttexthash="126777196">该模块有许多方法可以返回有关日期对象的信息。</font>```datetime```

下面是一些示例，您将在本章的稍后部分了解有关它们的详细了解：

### 例子

返回工作日的年数和名称：
```
 import datetime

x = datetime.datetime.now()

print(x.year)
print(x.strftime("%A"))

```

* * *

## 创建日期对象

<font _mstmutation="1" _msthash="103909" _msttexthash="159487640">若要创建日期，可以使用模块的类（构造函数）。</font>```datetime()``````datetime```

<font _mstmutation="1" _msthash="104104" _msttexthash="119189317">该类需要三个参数才能创建日期：年、月、日。</font>```datetime()```

### 例子

创建日期对象：
```
 import datetime

x = datetime.datetime(2020, 5, 17)

print(x)

```

<font _mstmutation="1" _msthash="104494" _msttexthash="645725925">该类还采用时间和时区的参数（小时、分钟、秒、微秒、tzone），但它们是可选的，默认值为 ， （对于时区）。</font>```datetime()``````0``````None```

* * *

* * *

## strftime（） 方法

<font _mstmutation="1" _msthash="104091" _msttexthash="137019844">该对象具有将日期对象格式化为可读字符串的方法。</font>```datetime```

<font _mstmutation="1" _msthash="104286" _msttexthash="218458240">该方法称为 ，并采用一个参数 ，来指定返回的字符串的格式：</font>```strftime()``````format```

### 例子

显示月份名称：
```
 import datetime

x = datetime.datetime(2018, 6, 1)

print(x.strftime("%B"))

```

所有法律格式代码的引用：

| Directive | Description | Example |
| %a | Weekday, short version | Wed | 
| %A | Weekday, full version | Wednesday | 
| %w | Weekday as a number 0-6, 0 is Sunday | 3 | 
| %d | Day of month 01-31 | 31 | 
| %b | Month name, short version | Dec | 
| %B | Month name, full version | December | 
| %m | Month as a number 01-12 | 12 | 
| %y | Year, short version, without century | 18 | 
| %Y | Year, full version | 2018 | 
| %H | Hour 00-23 | 17 | 
| %I | Hour 00-12 | 05 | 
| %p | AM/PM | PM | 
| %M | Minute 00-59 | 41 | 
| %S | Second 00-59 | 08 | 
| %f | Microsecond 000000-999999 | 548513 | 
| %z | UTC offset | +0100 |  |
| %Z | Timezone | CST |  |
| %j | Day number of year 001-366 | 365 | 
| %U | Week number of year, Sunday as the first day of week, 00-53 | 52 | 
| %W | Week number of year, Monday as the first day of week, 00-53 | 52 | 
| %c | Local version of date and time | Mon Dec 31 17:41:00 2018 | 
| %x | Local version of date | 12/31/18 | 
| %X | Local version of time | 17:41:00 | 
| %% | A % character | % | 


