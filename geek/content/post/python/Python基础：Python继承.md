
---
title: Python基础：Python继承
author: 知识铺
date: 2020-10-25 19:26:56+08:00
tags: [python]
---
# Python继承


## Python 继承

继承允许我们定义一个类，该类从另一个类继承所有方法和属性。

**父类**是从继承的类，也称为基类。

**子类**是从另一个类继承的类，也称为派生类。

* * *

## 创建父类

任何类都可以是父类，因此语法与创建任何其他类相同：

### 例子

<font _mstmutation="1" _msthash="220701" _msttexthash="109319821">创建名为 的 类，带 和 属性，以及方法：</font>```Person``````firstname``````lastname``````printname```
```
 class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname

  def printname(self):
    print(self.firstname, self.lastname)

#Use the Person class to create an object, and then execute the printname method: 
x = Person("John", "Doe")
x.printname()

```

* * *

## 创建子类

若要创建从另一个类继承功能的类，请将父类作为参数发送，以便创建子类：

### 例子

<font _mstmutation="1" _msthash="221806" _msttexthash="120594240">创建名为 的 类，它将从 类继承属性和方法：</font>```Student``````Person```
```
 class Student(Person):
  pass

<font _mstmutation="1" _msthash="219752" _msttexthash="203163363">**注：**当您不想向类添加任何其他属性或方法时，请使用 关键字。</font>```pass```

现在，学生类具有与 Person 类相同的属性和方法。

### 例子

<font _mstmutation="1" _msthash="220467" _msttexthash="91902135">使用 类创建对象，然后执行方法：</font>```Student``````printname```
```
 x = Student("Mike", "Olsen")
x.printname()

```

* * *

 <script>googletag.cmd.push(function() { googletag.display('div-gpt-ad-1493883843099-0'); });</script>

* * *

## 添加__init__（） 函数

到目前为止，我们已经创建了一个子类，该子类从其父级继承属性和方法。

<font _mstmutation="1" _msthash="103896" _msttexthash="128995893">我们要将函数添加到子类（而不是关键字）。</font>```__init__()``````pass```

<font _mstmutation="1" _msthash="220181" _msttexthash="169165035">**注：**每次使用类创建新对象时，都会自动调用该函数。</font>```__init__()```

### 例子

<font _mstmutation="1" _msthash="220675" _msttexthash="39094575">将 函数添加到类中：</font>```__init__()``````Student```
```
 class Student(Person):
  def __init__(self, fname, lname):
    #add properties etc.

<font _mstmutation="1" _msthash="104481" _msttexthash="104806468">添加函数时，子类将不再继承父类的函数。</font>```__init__()``````__init__()```

<font _mstmutation="1" _msthash="220844" _msttexthash="74508525">**注：**子函数**将覆盖**父函数的继承。</font>```__init__()``` ```__init__()```

<font _mstmutation="1" _msthash="104871" _msttexthash="150567937">若要保留父函数的继承，请向父函数添加调用：</font>```__init__()``````__init__()```

### 例子
```
 class Student(Person):
  def __init__(self, fname, lname):
    Person.__init__(self, fname, lname)

```

<font _mstmutation="1" _msthash="105261" _msttexthash="525465967">现在，我们已经成功地添加了 __init__（） 函数，并保留了父类的继承，并且我们准备在函数中添加功能。</font>```__init__()```

* * *

## 使用超级（） 函数

<font _mstmutation="1" _msthash="104273" _msttexthash="277803474">Python 还有一个函数，该函数将使子类从其父类继承所有方法和属性：</font>```super()```

### 例子
```
 class Student(Person):
  def __init__(self, fname, lname):
    super().__init__(fname, lname)

```

<font _mstmutation="1" _msthash="104663" _msttexthash="293601009">通过使用 函数，不必使用父元素的名称，它将自动从其父元素继承方法和属性。</font>```super()```

* * *

## 添加属性

### 例子

<font _mstmutation="1" _msthash="221988" _msttexthash="48649081">添加调用到类的属性：</font>```graduationyear``````Student```
```
 class Student(Person):
  def __init__(self, fname, lname):
    super().__init__(fname, lname)
    self.graduationyear = 2019

```

<font _mstmutation="1" _msthash="105638" _msttexthash="630142214">在下面的示例中，年应是一个变量，并在创建学生对象时传递到类中。为此，请添加另一个参数在 __init__（） 函数中：</font>```2019``````Student```

### 例子

<font _mstmutation="1" _msthash="222430" _msttexthash="131188915">添加参数，并在创建对象时传递正确的一年：</font>```year```
```
 class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

x = Student("Mike", "Olsen", 2019)

```

* * *

## 添加方法

### 例子

<font _mstmutation="1" _msthash="221312" _msttexthash="49717941">添加调用到 类的方法：</font>```welcome``````Student```
```
 class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

  def welcome(self):
    print("Welcome", self.firstname, self.lastname, "to the class of", self.graduationyear)

```

如果在子类中添加与父类中的函数同名的方法，则父方法的继承将被覆盖。

