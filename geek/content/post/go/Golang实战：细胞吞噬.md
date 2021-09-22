---
title: Golang实战：细胞吞噬
author: 知识铺
date: 2020-10-11 21:50:17+08:00
tags:
---

细胞吞噬游戏是一_个细胞自动_机， 但这并没有意味着很多， 大多数人。想象一下，一个存在于两种状态的细胞网格：活着或死亡。您看到的"动画"实际上是连续几代呈现在屏幕上。有四个规则可以帮助决定下一代的状态。维基百科这样描述它们。

1.  任何只有不到两个活邻居的活细胞死亡，好像因为人口不足。
2.  任何有两个或三个活邻居的活细胞都住着下一代。
3.  任何有三个超过三个活邻居的活细胞死亡，好像因为人口过剩。
4.  任何有三个活邻居的死细胞都变成了活细胞，就像通过繁殖一样。

需要有初始状态。正如我们从规则中看到的，空板不会产生细胞

<font _mstmutation="1" _msthash="290615" _msttexthash="893507992">每次运行_程序时，Go 中的包都会生成一个确定值序列_。我不想在我的主板的默认状态是相同的每个负载，所以我种子与不断变化的变量：时间。</font>```rand```

<font _mstmutation="1" _msthash="290914" _msttexthash="685440106">以下函数使用指向我的结构的指针，该结构具有一个称为板的属性。我们编辑存储在内存中的板，因此我们不需要返回任何内容。</font>```Game```

 <code>// Given an empty board, give it a random state
func giveState(g *Game) {
    rand.Seed(time.Now().UnixNano()) // <-- Different every time
    for x := 0; x < RES; x++ {
        for y := 0; y < RES; y++ {
            if rand.Intn(15) == 1 {
                g.board[x][y] = 1
            }
        }
    }
}</code> 

每个细胞在第一代都有1/15的机会活着。Ebiten 的更新功能以 60fps/秒的速度运行，我为每个报价创建新一代。我在左上角打印出当前代号。

[![Generation number](https://res.cloudinary.com/practicaldev/image/fetch/s--0qX4ZI_f--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/wu7h9427oyfo18dlziah.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--0qX4ZI_f--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/wu7h9427oyfo18dlziah.png)

细胞吞噬游戏似乎是计算机科学学生的仪式。至少，这就是我从网上学到的。它并没有出现在我的任何类， 所以它的乐趣， 玩它周围， 并阅读人们用它创造的惊人的东西。例如，[具有均匀时间](https://zshipu.com/t?url=https://codegolf.stackexchange.com/a/111932)步数的数字时钟的副本。

### [](#interaction)<font _mstmutation="1" _msthash="306202" _msttexthash="4031014">互动</font>

[![Interaction GIF](https://res.cloudinary.com/practicaldev/image/fetch/s--3N1C5VYi--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/4h0vgbxkspmszb7jlvb7.gif)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--3N1C5VYi--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/4h0vgbxkspmszb7jlvb7.gif)

<font _mstmutation="1" _msthash="290303" _msttexthash="2319385263">如果单击板，附近的单元格会翻转其状态。您可以在屏幕上拖动以使单元格级联。动画模式有一个简单的乐趣。Ebiten 有一个函数用于单击，我在每个更新刻度上调用它。在这里，我们使用多个内联赋值来设置 和 的值。这些变量的类型在编译时推断。</font>```x``````y```

 <code>if ebiten.IsMouseButtonPressed(ebiten.MouseButtonLeft) {
    x, y := ebiten.CursorPosition()
    interaction(x, y, g)
}</code> 

和 Golang 一样低级， 默认情况下， 它似乎不走你的路。

### [](#go-modules)<font _mstmutation="1" _msthash="304941" _msttexthash="11614759">转到模块</font>

<font _mstmutation="1" _msthash="291499" _msttexthash="1220215984">我知道 Go 的模块系统是最近增加的。我通过运行创建了一个 mod 文件，然后每当我构建或运行代码时，依赖项都会自动更新。更改开发设置就像克隆存储库和运行一样简单。</font>```go mod init github.com/my/repo``````go install```

我还发现VS代码的 Go 插件是令人难以置信的有用， 它执行更有用的行动比我可能知道！这有助于我专注于学习语言。任何人寻找一种方法进入去，我[推荐一个去之旅](https://zshipu.com/t?url=https://tour.golang.org/welcome/1)。除此之外， 谁知道 — — 我自己正在测试一些， 欢迎推荐！

查看我的[GitHub](https://zshipu.com/t?url=https://github.com/healeycodes/conways-game-of-life)上的代码。




