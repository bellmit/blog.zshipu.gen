---
title: Golang实践：Golang的 3 个陷阱
author: 知识铺
date: 2020-10-13 22:20:16+08:00
tags: [golang]
---

<font _mstmutation="1" _msthash="44967" _msttexthash="998946091">在过去的一年里，我们一直在开发一个复杂的半实时生产系统。我们决定和Golang一起写。我们在 Go 中几乎没有经验，所以正如你想象的那样，这不是一件小事。</font>

<font _mstmutation="1" _msthash="28210" _msttexthash="232982165">快进一年：该系统在生产中运行，并成为CllimaCell产品的主要支柱之一。</font>

<font _mstmutation="1" _msthash="26923" _msttexthash="323578528">精通意味着你有足够的经验来知道你正在使用的平台的陷阱是什么以及如何避免它们。</font>

<font _mstmutation="1" _msthash="33748" _msttexthash="377549159">我想描述一下我们在与Golang的探索中遇到的三个陷阱，希望这能帮助你避免它们离开大门。</font>

# <font _mstmutation="1" _msthash="27378" _msttexthash="11073088">可伸缩性</font>

<font _mstmutation="1" _msthash="26924" _msttexthash="36342800">请考虑以下示例：</font>

package main

import (
"fmt"
"sync"
)

type A struct {
id int
}

func main() {
channel := make(chan A, 5)

```
var wg sync.WaitGroup

wg.Add(1)
go func() {
	defer wg.Done()
	for a := range channel {
		wg.Add(1)
		go func() {
			defer wg.Done()
			fmt.Println(a.id)
		}()
	}

}()

for i := 0; i < 10; i++ {
	channel <- A{id:i}
}
close(channel)

wg.Wait()
```

}

<font _mstmutation="1" _msthash="28587" _msttexthash="417832831">我们有一个通道，用于构造实例。我们与操作员一起遍网络。你认为这一段代码的输出是什么？</font>``range``

6
6
6
6
6
9
9
9
9
9

<font _mstmutation="1" _msthash="33995" _msttexthash="226712382">很奇怪， 不是吗？我们预计会看到数字1~9（当然没有订购）。</font>

<font _mstmutation="1" _msthash="28548" _msttexthash="139234576">我们实际看到的是循环变量的可变异性的结果：</font>

<font _mstmutation="1" _msthash="23101" _msttexthash="2357056585">在每次迭代中，我们都会使用一个结构实例。结构是值类型 - 它们在每个迭代中复制到 for 迭代变量。这里的关键词是**复制**。为了避免大量内存打印，而不是在每次迭代**中**创建变量的新实例，而是在循环的开头创建一个实例，并在每次迭代中复制**数据**。</font>

<font _mstmutation="1" _msthash="44317" _msttexthash="1622940176">闭包是等式的另一部分：Go 中的闭包（与大多数语言一样），保留闭包中对象的引用（不复制数据），因此内部 go 例程需要引用该引用的对象，这意味着所有 go 例程都得到对同一实例的相同引用。</font>

**解决方案**

<font _mstmutation="1" _msthash="33215" _msttexthash="667127292">首先要知道，这会发生。它并非微不足道，因为它与其他语言完全不同（在 C# 中，在 JS 中为 for - 在那些循环变量是不可变的）</font>

<font _mstmutation="1" _msthash="28457" _msttexthash="423010341">为了避免此陷阱，请捕获循环范围内的变量，从而自己创建新实例，然后根据您想使用它：</font>

go func() {
defer wg.Done()
for a := range channel {
wg.Add(1)
go func(item A) {
defer wg.Done()
fmt.Println(item.id)
}(a) // Capture happens here
}
}()

<font _mstmutation="1" _msthash="33878" _msttexthash="316652154">在这里，我们使用内部 go 例程的函数调用来捕获 - 有效地复制它。也可以显式复制：</font>``a``

for a := range channel {
wg.Add(1)
item := a // Capture happens here
go func() {
defer wg.Done()
fmt.Println(item.id)
}()
}

**笔记**

* <font _mstmutation="1" _msthash="32747" _msttexthash="1223122082">对于大型数据集，请注意，捕获循环变量将创建大量对象，每个对象都保存到执行基础 go 例程之前，因此如果对象包含多个字段，请考虑仅捕获执行内部例程所需的字段</font>
* ``for-range``<font _mstmutation="1" _msthash="33254" _msttexthash="910275314">作为数组的附加表示。它还创建一个索引循环变量。请注意，索引循环变量也是**可变的。**即，要在 go 例程中使用它，请像使用值循环变量一样捕获它</font>
* <font _mstmutation="1" _msthash="28171" _msttexthash="742134627">在当前 Go 版本 （1.15） 上，我们看到的初始代码实际上将引发错误！帮助我们避免此问题，并强制我们捕获我们需要的数据</font>

# <font _mstmutation="1" _msthash="39364" _msttexthash="12351079">小心 ： |</font>

<font _mstmutation="1" _msthash="34411" _msttexthash="99853793">GoLang 有两个赋值运算符，并且：</font>``=``````:=``

var num int
num = 3

name := "yossi"

``:=``<font _mstmutation="1" _msthash="40053" _msttexthash="1013312300">非常有用，允许在赋值之前避免变量声明。它实际上是当今许多类型语言的常见做法（如 C# 中）。它非常有用， 并保持代码更干净 （我卑微的意见） 。</font>``var``

<font _mstmutation="1" _msthash="27222" _msttexthash="793817414">但是，尽管这很可爱，但当与 GoLang 中的一些其他行为、范围和多个返回值相结合时，我们可能会遇到意外的行为。请考虑以下示例：</font>

package main

import (
"fmt"
)

func main() {
var data []string

```
data, err := getData()
if err != nil {
	panic("ERROR!")
}

for _, item := range data {
	fmt.Println(item)
}
```

}

func getData() ([]string, error) {
// Simulating getting the data from a datasource - lets say a DB.
return []string{"there","are","no","strings","on","me"}, nil
}

<font _mstmutation="1" _msthash="27755" _msttexthash="155632282">在此示例中，我们从某处读取字符串数组并打印它：</font>

there
are
no
strings
on
me

<font _mstmutation="1" _msthash="23673" _msttexthash="17557020">请注意：</font>``:=``

data, err := getData()

<font _mstmutation="1" _msthash="23582" _msttexthash="394969783">请注意，即使已声明，我们仍然可以使用，因为不是。不错的速记， 创建一个更干净的代码。</font>``data``````:=``````err``

<font _mstmutation="1" _msthash="33722" _msttexthash="56724382">现在让我们修改一下代码：</font>

func main() {
var data []string

```
killswitch := os.Getenv("KILLSWITCH")

if killswitch == "" {
	fmt.Println("kill switch is off")
	data, err := getData()

	if err != nil {
		panic("ERROR!")
	}

	fmt.Printf("Data was fetched! %d\n", len(data))
} 	

for _, item := range data {
	fmt.Println(item)
}
```

}

<font _mstmutation="1" _msthash="39039" _msttexthash="81530462">你认为这一段代码的结果是什么？</font>

kill switch is off
Data was fetched! 6

<font _mstmutation="1" _msthash="23114" _msttexthash="733203900">很奇怪，不是吗？由于 kill 开关已关闭，因此我们确实加载数据 - 我们甚至打印数据的长度。那么为什么代码不像以前那样打印呢？</font>

<font _mstmutation="1" _msthash="33228" _msttexthash="38353549">你猜对了，因为！</font>``:=``

<font _mstmutation="1" _msthash="23504" _msttexthash="432494569">GoLang 中的范围（与大多数现代拉瓜奇一样）用 定义。在这里，这将创建一个新的范围：</font>``{}``````if``

if killswitch == "" {
...		
}

<font _mstmutation="1" _msthash="32500" _msttexthash="597966070">因为我们使用 ，Go 将同时视为新的变量！即。 if 子句中实际上是一个新变量，当作用域关闭时，该变量将被丢弃。</font>``:=``````data``````err``````data``

<font _mstmutation="1" _msthash="31902" _msttexthash="1345242509">我们在初始化流中多次遇到此类行为，这些操作通常公开某种包变量，完全按照此处所述进行初始化，使用 kill 开关，以便我们禁用生产上的某些行为。上述实现将导致系统无效状态。</font>

**解决方案**

<font _mstmutation="1" _msthash="29276" _msttexthash="58783335">意识 — — 我已经说过了吗？:)</font>

<font _mstmutation="1" _msthash="32630" _msttexthash="351624676">在某些情况下，如果未使用子句中的内部变量，则 Go 编译器将发出警告甚至错误：</font>``if``

if killswitch == "" {
fmt.Println("kill switch is off")
data, err := getData()

```
if err != nil {
	panic("ERROR!")
}
```

}

// Will issue an error :
data declared but not used

<font _mstmutation="1" _msthash="28821" _msttexthash="63167546">因此，在编译时请注意警告。</font>

<font _mstmutation="1" _msthash="28132" _msttexthash="203010041">但是，有时我们确实在作用域内使用变量，因此不会发出错误。</font>

<font _mstmutation="1" _msthash="33709" _msttexthash="674509355">无论如何，最好的行动方针是尽量避免速记 - 特别是当它涉及多个返回值和错误处理，并在决定使用它时保持额外的注意：</font>``:=``

func main() {
var data []string
var err error // Declaring err to make sure we can use = instead of :=

```
killswitch := os.Getenv("KILLSWITCH")

if killswitch == "" {
	fmt.Println("kill switch is off")
	data, err = getData()

	if err != nil {
		panic("ERROR!")
	}

	fmt.Printf("Data was fetched! %d\n", len(data))
} 

for _, item := range data {
	fmt.Println(item)
}
```

}

<font _mstmutation="1" _msthash="39351" _msttexthash="16974906">将导致：</font>

kill switch is off
Data was fetched! 6
there
are
no
strings
on
me

<font _mstmutation="1" _msthash="35516" _msttexthash="909712817">请记住，随着代码的发展，不同的人将修改它。以前不在不同范围内的代码可能是将来。修改现有代码时，尤其是将代码移动到其他范围时，请留意。</font>

# <font _mstmutation="1" _msthash="29588" _msttexthash="33733401">工人池。队长工人池</font>

<font _mstmutation="1" _msthash="23387" _msttexthash="36342800">请考虑以下示例：</font>

package main

import (
"fmt"
"sync"
"time"
)

type A struct {
id int
}

func main() {
start := time.Now()

```
channel := make(chan A, 100)

var wg sync.WaitGroup

wg.Add(1)
go func() {
	defer wg.Done()
	for a := range channel {
		process(a)
	}

}()

for i := 0; i < 100; i++ {
	channel <- A{id:i}
}
close(channel)

wg.Wait()

elapsed := time.Since(start)
fmt.Printf("Took %s\n", elapsed)
```

}

func process(a A) {
fmt.Printf("Start processing %v\n", a)
time.Sleep(100 * time.Millisecond)
fmt.Printf("Finish processing %v\n", a)
}

<font _mstmutation="1" _msthash="23569" _msttexthash="2086523946">和以前一样，我们在通道上有一个 for 范围环路。比们说，函数包含我们需要运行的算法，而且速度不是很快。如果我们处理，让我们说，上面的代码将运行近3小时（进程运行100ms在示例中）。因此，让我们这样做：</font>``process``

package main

import (
"fmt"
"sync"
"time"
)

type A struct {
id int
}

func main() {
start := time.Now()

```
channel := make(chan A, 100)

var wg sync.WaitGroup

wg.Add(1)
go func() {
	defer wg.Done()
	for a := range channel {
		wg.Add(1)
		go func(a A) {
			defer wg.Done()
			process(a)
		}(a)
	}

}()

for i := 0; i < 100; i++ {
	channel <- A{id:i}
}
close(channel)

wg.Wait()

elapsed := time.Since(start)
fmt.Printf("Took %s\n", elapsed)
```

}

func process(a A) {
fmt.Printf("Start processing %v\n", a)
time.Sleep(100 * time.Millisecond)
fmt.Printf("Finish processing %v\n", a)
}

<font _mstmutation="1" _msthash="37947" _msttexthash="689875563">我们不要串行处理项目，而是为通道中的每个项目调度一个 Go 例程。我们希望利用 Go 惊人的并发处理来帮助我们更快地处理数据：</font>

<font _mstmutation="1" _msthash="29367" _msttexthash="136279455">从理论上讲，这也对10万件商品有效，对吗？</font>

<font _mstmutation="1" _msthash="33956" _msttexthash="70248490">不幸的是，答案是"视情况而定"。</font>

<font _mstmutation="1" _msthash="28613" _msttexthash="3215794621">要了解原因，我们需要了解当我们调度一个去例程时会发生什么。我不会深入讨论它，因为它超出了本文的范围。简而言之，运行时将创建一个对象，其中包含与 go 例程相关的所有数据并存储它。执行 go 例程后，将逐出该例程。go 例程对象的最小大小为 2K，但它可以达到 1GB（在 64 位计算机上）。</font>

<font _mstmutation="1" _msthash="27274" _msttexthash="2076964006">现在，您可能知道我们要去哪里 - 我们创建操作的去越多，我们创建的对象也越来越多，因此内存消耗正在增加。此外，go 例程需要 CPU 的执行时间才能执行实际执行，因此，内核越少，这些对象中将保留在内存中等待执行。</font>

<font _mstmutation="1" _msthash="31005" _msttexthash="2679557686">在资源环境低（Lambda 函数、具有重新占用限制的 K8s 窗格）上，CPU 和内存都受到限制，代码示例即使在 100K go 例程时也会对内存造成压力（同样，取决于实例的可用内存量）。在我们的案例中，在具有 128MB 内存的云函数上，我们能够在崩溃之前处理 10 万个项。</font>

<font _mstmutation="1" _msthash="32461" _msttexthash="677967563">请注意，从应用程序的角度来看，我们需要的实际数据非常小 — 在这种情况下，是一个简单的 int。大多数内存消耗是 go 例程本身。</font>

**解决方案**

<font _mstmutation="1" _msthash="35425" _msttexthash="16015961">工人池！</font>

<font _mstmutation="1" _msthash="23400" _msttexthash="510974737">辅助角色池允许我们管理我们的访问例程数，保持内存打印量低。让我们看到与辅助角色池相同的示例：</font>

package main

import (
"fmt"
"sync"
"time"
)

type A struct {
id int
}

func main() {
start := time.Now()

```
workerPoolSize := 100

channel := make(chan A, 100)

var wg sync.WaitGroup

wg.Add(1)
go func() {
	defer wg.Done()
	for i := 0;i < workerPoolSize;i++ {
		wg.Add(1)
		go func() {
			defer wg.Done()

			for a := range channel {
				process(a)
			}
		}()
	}

}()

// Feeding the channel
for i := 0; i < 100000; i++ {
	channel <- A{id:i}
}
close(channel)

wg.Wait()

elapsed := time.Since(start)
fmt.Printf("Took %s\n", elapsed)
```

}

func process(a A) {
fmt.Printf("Start processing %v\n", a)
time.Sleep(100 * time.Millisecond)
fmt.Printf("Finish processing %v\n", a)
}

<font _mstmutation="1" _msthash="34749" _msttexthash="246024233">我们将工作人员池的数量限制为 100，并且每个池都创建了一个 go 例程：</font>

go func() {
defer wg.Done()
for i := 0;i < workerPoolSize;i++ {
wg.Add(1)
go func() { // Go routine per worker
defer wg.Done()

```
		for a := range channel {
			process(a)
		}
	}()
}
```

}()

<font _mstmutation="1" _msthash="34489" _msttexthash="864045403">将通道视为队列，每个工作人员转到的例程都是队列的使用者。Go 的通道允许多个转到例程侦听同一通道，其中通道中的每个项目将处理一次。</font>

<font _mstmutation="1" _msthash="21801" _msttexthash="351601432">**好处：**我们现在可以规划我们的环境，因为现在存储器打印是预期的，可以测量：</font>

the size of the worker pool * expected size of a single go routine (min 2K)

<font _mstmutation="1" _msthash="22022" _msttexthash="5964247770">**缺点：执行**时间将增加。当我们限制内存使用时，我们会用增加的执行时间来支付内存使用量。为什么？以前，我们每个项目都调度一个 go 例程来处理 — — 实际上每个项目都创建使用者。实际上，我们提供了无限的规模和高并发性。实际上，它不正确，因为执行 go 例程取决于运行应用程序的核心的可用性。这意味着我们必须根据我们运行的平台优化员工数量，但在高容量系统中这样做是有意义的。</font>

<font _mstmutation="1" _msthash="23205" _msttexthash="937616394">**总结：**工作池让我们更好地控制代码的执行。它们允许我们实现可预测性，因此我们可以规划和优化我们的代码和平台，以扩展到高吞吐量和高数据量。</font>

<font _mstmutation="1" _msthash="23764" _msttexthash="1999371387">我建议在**应用程序需要**迭代数据集（即使是小数据集）的情况下始终使用辅助角色池。使用辅助角色池，我们现在能够处理 Cloud 函数上的数百万个项目，甚至无需接近平台启用的限制，从而为我们提供了足够的扩展空间。</font>

**笔记**

* <font _mstmutation="1" _msthash="34191" _msttexthash="469796600">应配置工作人员数量（例如 env 变量），以便您玩该数，并在运行的每个平台上达到您想要的结果</font>
* <font _mstmutation="1" _msthash="33865" _msttexthash="642918380">将通道大小设置为至少池中工作点数 - 这将允许数据生产者填充队列，并防止工作人员在生成数据时等待空闲。使其可配置。</font>

# <font _mstmutation="1" _msthash="39104" _msttexthash="6674577">结论</font>

<font _mstmutation="1" _msthash="26793" _msttexthash="294375263">使我们成为更好的专业人员的是能够从错误中吸取教训。但是向别人学习同样重要。</font>

<font _mstmutation="1" _msthash="33124" _msttexthash="61742850">如果你到达这么远 ~ 谢谢！</font>

<font _mstmutation="1" _msthash="38662" _msttexthash="398272706">我希望我们在这里看到的将帮助你， 亲爱的读者， 以避免我们在与 GoLang 的旅程中所犯的错误。</font>
