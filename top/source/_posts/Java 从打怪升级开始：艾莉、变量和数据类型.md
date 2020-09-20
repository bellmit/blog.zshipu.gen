
title: Java 从打怪升级开始：艾莉、变量和数据类型
author: 知识铺
date: 2020-09-20 22:13:19
tags: 
---
  

  <jr-tutorial-lecture-dynamic-content _ngcontent-jr-site-c193="" _nghost-jr-site-c191="" class="ng-star-inserted"><jr-text-content _nghost-jr-site-c94="" class="ng-star-inserted"><jr-content _ngcontent-jr-site-c94="" classname="lecture-content post-content" _nghost-jr-site-c93="">![image-zho-CN-00-14](https://cdn.codegym.cc/images/article/b7adf6cb-9b01-40bc-b249-638acc575918/800.webp)

一个粉红色头发的女人进入了船舱。“我想知道是否所有人类女性都有这样的头发，”阿米戈在想。

“嗨！我叫埃莉诺•凯瑞 (Eleanor Carrey)。你可以叫我艾莉。我是银河系狂奔号的导航员。”

“嗨，艾莉，”阿米戈逼着自己说道。

“我将讲解整个 Java 语言中最有趣的部分：变量。”

“我准备好听讲了。你说的这些变量是什么？”

“变量是用来存储数据的特殊实体。任何数据。在 Java 语言中，所有数据都存储在变量中。最接近的比喻就好比是一个盒子。”

“一个盒子？什么样的盒子？”

“任何一个旧盒子。假设你在一张纸上写下数字 13，并把它放进一个盒子里。现在我们可以说，这个盒子里面存的是数值 13。”

“在 Java 语言中，每个变量都有三个重要的属性：类型、名称和值。”

“你能解释一下这是什么意思吗？”

“当然。我们使用名称，这样我们可以将一个变量与另一个变量区分开来。这就像一个盒子上的标签。”

“一个变量的类型决定了可以存储在其中的值/数据的类型。我们把帽子放进帽盒，把鞋子放进鞋盒，等等。”

“值是存储在变量中的特定对象、数据或信息。”

“你能告诉我关于类型的更多内容吗？”

“当然。Java 语言中的每个对象都有一个特定的类型。例如整数、小数、文本、猫 (Cat)、房屋 (House) 等。”

“变量也有类型。它只能存储类型与其自身相同的值。”

“你可以在现实生活中看到这一点。不同种类的盒子用来储存不同的东西：”

[![](https://cdn.codegym.cc/images/article/4195b19c-af84-4642-abb9-ee6bbe83e5b4/original.jpeg)](https://zshipu.com/t?url=https://cdn.codegym.cc/images/article/4195b19c-af84-4642-abb9-ee6bbe83e5b4/original.jpeg)

“要创建（或声明）一个变量，我们要使用类型的名称：```TypeName variableName```。”

“下面是一些例子：”

|  | 声明一个变量：
首先是类型，然后是名称。 | 说明 |
| 1 | ```<mark class="red">int a</mark>;``` | 创建一个 <mark class="red">int</mark> 变量，其名称为 <mark class="red">a</mark>。 |
| 2 | ```<mark class="green">String s</mark>;``` | 创建一个 <mark class="green">String</mark> 变量，其名称为 <mark class="green">s</mark>。 |
| 3 | ```<mark class="viola">double c</mark>;``` | 创建一个 <mark class="viola">double</mark> 变量，其名称为 <mark class="viola">c</mark>。 |

“两种最常见的类型是整数（使用 <mark class="red">int</mark> 来声明）和文本（使用 <mark class="green">String</mark> 来声明）。”

“什么是 double？”

“**Double** 是分数，或实数。”

“你说变量有三个属性：类型、名称和值。但我只能看到两个属性。所以，我的问题是，如何给变量赋值？”

“让我们回到那个盒子的类比。想象一下，你拿一张纸，写下数字 42，然后把它放进盒子里。现在盒子里存的值是 42。”

“我明白了。”

“我们用一个特殊操作（**赋值**）为变量分配数值。赋值操作会将值从一个变量复制到另一个变量。它不会去移动数值。而是复制数值。就像磁盘上的文件。它的代码是这样的：“

|  | 代码 | 说明 |
| 1 | ```<mark class="green">i</mark> = 3;``` | 将数值 3 赋值给变量 <mark class="green">i</mark>。 |
| 2 | ```<mark class="green">a</mark> = 1;
<mark class="viola">b</mark> = <mark class="green">a</mark>+1;``` | 将数值 1 赋值给变量 <mark class="green">a</mark>。
将数值 2 赋值给变量 <mark class="viola">b</mark>。 |
| 3 | ```<mark>x</mark> = 3;
<mark>x</mark> = <mark>x</mark> + 1;``` | 将数值 3 赋值给变量 <mark>x</mark>。
在下一行中，<mark>x</mark> 的数值增加 1，使 x 等于4 |

“为了执行赋值操作，我们使用**等号** (```=```)。”

“我再说一遍：**这不是进行比较**。我们正在将等号右边的值复制给左边的变量。要进行比较，Java 语言会使用双等号 (```==```)。”

“我知道如何将猫放入变量中了。就像一个程序。”

“如何捉猫：

1.拿一个空盒子。

2.等等。”

[![](https://cdn.codegym.cc/images/article/a9a5ffcb-edb4-4a08-b4a4-c2b84cf197c2/original.jpeg)](https://zshipu.com/t?url=https://cdn.codegym.cc/images/article/a9a5ffcb-edb4-4a08-b4a4-c2b84cf197c2/original.jpeg)

“不，阿米戈。你只能把一只猫塞进一个盒子里。呃，我的意思是你只能给一个变量赋一个值。”

“我明白了。你能给我讲讲更多创建变量的例子吗？”

“可以啊。让我再说一遍：要创建（或声明）变量，你需要使用‘```TypeName variableName```’名称。”

|  | 代码 | 说明 |
| 1 | ```String <mark class="red">s</mark>;``` | 创建了一个 ```String``` 变量，其名称为 <mark class="red">s</mark>。
此变量可以存储文本。 |
| 2 | ```int <mark>x</mark>;``` | 创建了一个 ```int``` 变量，其名称为 <mark>x</mark>。
此变量可以存储整数。 |
| 3 | ```int <mark class="viola">a</mark>, <mark class="user">b</mark>, <mark class="green">c</mark>;
int <mark>d</mark>;``` | 创建了四个 ```int``` 变量，其名称为 <mark class="viola">a</mark>、<mark class="user">b</mark>、<mark class="green">c</mark>和 <mark>d</mark>。
这些变量可以存储整数。 |

“哦，现在我明白了！”

“请记住，你不能在同一方法中创建两个名称相同的变量。”

“在不同的方法中可以这样做吗？”

“是的，你可以这样做。这就像在不同的房子里都有盒子一样。”

“我能给一个变量取一个我喜欢的名字吗？”

“基本上可以。变量名不能包含空格、加号、减号等。最好在一个变量名中只使用字母和数字。”

“请记住，**Java 语言区分大小写。** ```int a``` 和 ```Int a``` 不同。”

“顺便说一下，在 Java 语言中，你可以创建一个变量并同时为它赋值。这样可以节省时间和空间。”

|  | 紧凑代码 | 等效代码（代码较长） |
| 1 | ```int a = 5;
int b = 6;``` | ```int a;
a = 5;
int b;
b = 6;``` |
| 2 | ```int c = 7;
int d = c+1;``` | ```int c;
c = 7;
int d;
d = c+1;``` |
| 3 | ```String s = "我是阿米戈";``` | ```String s;
s = "我是阿米戈";``` |

“这种方式代码更紧凑，更清晰。”

“我们就是这么做的。”

“每个 Java 新手都需要熟悉的两种类型：int（整数）和String（文本/字符串）。”

“**int** 类型可以让你在变量中存储数字，并对其执行运算：加法、减法、乘法、除法等。”

|  | 代码 | 说明 |
| 1 | ```int <mark>x</mark> = 1;
int <mark class="user">y</mark> = <mark>x</mark>*2;
int <mark class="green">z</mark> = 5*<mark class="user">y</mark>*<mark class="user">y</mark> + 2*<mark class="user">y</mark> + 3;``` | <mark>x</mark> 等于 1
<mark class="user">y</mark> 等于 2
<mark class="green">z</mark> 等于 20+4+3，其结果等于 27 |
| 2 | ```int <mark class="user">a</mark> = 5;
int <mark class="green">b</mark> = 1;
int <mark class="viola">c</mark> = (<mark class="user">a</mark>-<mark class="green">b</mark>) * (<mark class="user">a</mark>+<mark class="green">b</mark>);``` | <mark class="user">a</mark> 等于 5
<mark class="green">b</mark> 等于 1
<mark class="viola">c</mark> 等于 4x6，其结果为 24 |
| 3 | ```int <mark class="user">a</mark> = 64;
int <mark class="red">b</mark> = <mark class="user">a</mark>/8;
int <mark class="viola">c</mark> = <mark class="red">b</mark>/4;
int <mark>d</mark> = <mark class="viola">c</mark>*3;``` | <mark class="user">a</mark> 等于 64
<mark class="red">b</mark> 等于 8
<mark class="viola">c</mark> 等于 2
<mark>d</mark> 等于 6 |

“明白了。编程总是这么简单吗？”

“事实上，是的。”

“太好了！那么，接下来是什么？”

“**String** 类型允许你存储多行的文本，也称为‘字符串’。”

“要在 Java 中分配一个字符串，你需要将文本放在引号内。下面是一些示例：”

|  | 代码 | 说明 |
| 1 | ```String s = "阿米戈";``` | ```s``` 包含```“阿米戈”```。 |
| 2 | ```String s = "123";``` | ```s``` 包含```“123”```。 |
| 3 | ```String s = "123 + 456";``` | ```s``` 包含```“123 + 456”```。 |

“明白了。看起来并不是很难。”

“还有一个有趣的事情告诉你。”

“你可以用加号 (```+```) 将字符串连接起来。看看这些例子。”

|  | 代码 | 说明 |
| 1 | ```String s = "阿米戈" + "是最棒的";``` | ```s``` 包含```"阿米戈是最棒的"```。 |
| 2 | ```String s = "";``` | ```s``` 包含一个空字符串——一个完全没有符号的字符串。 |
| 3 | ```int x = 333;
String s = "阿米戈" + x;``` | ```s``` 包含```"阿米戈333"```。 |

“那么，你可以为数字添加字符串吗？”

“可以，但请记住，当你添加字符串和数字时，结果始终是一个字符串。”

“我通过你的例子理解了。”

“如果你很聪明的话，想想如何在屏幕上显示一个变量。”

“嗯。一个变量？在屏幕上？没有任何思路。”

“实际上，这很简单。要在屏幕上显示某些内容，我们使用 ```System.out.println()``` 命令，然后我们将想要打印的内容作为参数来传递。”

|  | 代码 | 屏幕输出信息 |
| 1 | ```System.out.**println**("阿米戈");``` | 阿米戈 |
| 2 | ```System.out.**println**("阿米"+"戈");``` | 阿米戈 |
| 3 | ```String s = "阿米戈";
System.out.**println**(s);``` | 阿米戈 |
| 4 | ```String s = "阿米";
System.out.**println**(s+"戈");``` | 阿米戈 |

“啊哈！这让一切都清晰多了。”

