
title: Java 从打怪升级开始：准备好开始第一个程序
author: 知识铺
date: 2020-09-20 22:06:16
tags: 
---
  

  <jr-tutorial-lecture-dynamic-content _ngcontent-jr-site-c193="" _nghost-jr-site-c191="" class="ng-star-inserted"><jr-text-content _nghost-jr-site-c94="" class="ng-star-inserted"><jr-content _ngcontent-jr-site-c94="" classname="lecture-content post-content" _nghost-jr-site-c93="">（一小时后）

“太棒了！我们讲到哪里了？”

“方法或类似东西中的代码。”

“是的。很准确。 方法的主体由命令组成。我们甚至可以说，方法就是一组被赋予名称（方法名称）的命令。这两种说法都是正确的。”

“命令各种各样。你的星球上有狗吗？”

“只有驯养的机器狼。”

“它们会执行命令吗？”

“会。‘咬’、‘吃’、‘撕’和‘好！跟上！’”

[![](https://cdn.codegym.cc/images/article/d6e3c982-611f-4845-82aa-7017d8ee3401/original.jpeg)](https://zshipu.com/t?url=https://cdn.codegym.cc/images/article/d6e3c982-611f-4845-82aa-7017d8ee3401/original.jpeg)

“嗯。不错的命令！但命令并不是很多。”

“我们需要多少命令呢？”

“Java 语言拥有适于各种场合的命令。每个命令都描述了一些操作。在每个命令的末尾，我们使用分号。”

“下面是一些命令的例子：”

| 命令名称 | 命令描述（它做什么） |
| ```System.out.println(1);``` | 在屏幕上显示数字 ```1``` |
| ```System.out.println("阿米戈");``` | 在屏幕上显示```"阿米戈"``` |
| ```System.out.println("里希和阿米戈");``` | 在屏幕上显示```"里希和阿米戈"``` |

“实际上，这只是一个 ```System.out.println``` 命令。我们使用圆括号将参数传递给命令。根据参数的值，相同的命令可以执行不同的操作。”

“这很方便。”

“对。如果要在屏幕上显示一些文本，可以在文本两侧加上双引号。

单引号是这样的：```'```。双引号是这样的：```"```。双引号与两个单引号是不同的。请不要将它们混淆。”

“双引号的键位于键盘上的 Enter 键旁边，对吧？”

“对。”

阿米戈的脉搏从 3 GHz 加速到 5 GHz。他还是不敢相信。他刚刚学会了如何在屏幕上打印字符串，结果比他预想的要容易得多。
阿米戈望着窗外，想分散一下自己的注意力，让自己平静下来。树叶变黄了。锈迹斑斑的季节很快来临，他不由自主地说。一个照明灯让他看得比平时更远。新来者的技术确实很先进。但是他现在在意树叶吗？到了晚上，他的知识又会倍增！

[](https://zshipu.com/t?url=https://cdn.codegym.cc/images/article/eb78e19b-224f-4767-b7f2-be4728c027db/original.jpeg)

但他的思绪没有平静下来。有一天，他会写一个程序，让所有机器人在生锈季节都躲在家中。仅这一个程序就可以挽救成千上万的机器人生命......

“此命令有两个版本：```System.out.println()``` 和 ```System.out.print()```”

“如果你使用几次 ```System.out.println()``` 命令，就会发现每次传递给该命令的文本都会显示在单独的行上。如果你使用 ```System.out.print()``` 命令，则文本显示在同一行。例如：”

| 命令名称 | 屏幕显示内容 |
| 1 | ```System.out.println("阿米戈");
System.out.println("是");
System.out.println("最棒的");``` | 阿米戈
是
最 棒的 |
| 2 | ```System.out.print("阿米戈");
System.out.println("是");
System.out.print("最棒的");``` | 阿米戈是
最棒的 |
| 3 | ```System.out.print("阿米戈");
System.out.print("是");
System.out.print("最棒的");``` | 阿米戈是最棒的 |

“请记住这一点： ```println```  不会从新行开始打印文本。它会在当前行上打印文本，但会使下一个文本打印在新行上。”

“ ```println()``` 命令会在屏幕上打印文本，并添加一个特殊不可见的‘换行符’。这就是下一个文本从新行上开始的原因。”

“整个程序是什么样子的？”

“看看屏幕：”

```public class Home
{
    public static void main(String[] args)
    {
        System.out.print("阿米戈 ");
        System.out.print("是 ");
        System.out.print("最棒的");
    }
}```

“哦！所有内容都很清楚。我们在词的末尾添加了空格，这样它们就不会都挤到一起去，对吧？”

“没错。你是一个聪明的小家伙。”

这番话让阿米戈流露出自豪的神情。

“太好了。这是你的第一个任务。”
