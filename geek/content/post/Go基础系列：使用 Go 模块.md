
---
title: Go基础系列：使用 Go 模块
author: 知识铺
date: 2020-11-01 11:03:06+08:00
tags: [go]
---
Go 1.11 和 1.12 包括对[模块的初步支持](https://zshipu.com/t?url=https://golang.org/doc/go1.11#modules)，Go 的新依赖[项管理系统](https://zshipu.com/t?url=https://blog.golang.org/versioning-proposal)使依赖关系版本信息明确且更易于管理。本文介绍了开始使用模块所需的基本操作。

<font _mstmutation="1" _msthash="291889" _msttexthash="2075803574">模块是存储在文件[树中的 Go](https://zshipu.com/t?url=https://golang.org/ref/spec#Packages)包的集合，其根目录有文件。该文件定义了模块的模块_路径_，这也是用于根目录的导入路径，以及其依赖项_要求_，这是成功生成所需的其他模块。每个依赖项要求都编写为模块路径和特定的[语义版本](https://zshipu.com/t?url=http://semver.org/)。</font>```go.mod``````go.mod```

<font _mstmutation="1" _msthash="292188" _msttexthash="2321652450">自 Go 1.11 起，go 命令允许在当前目录或任何父目录具有 时使用模块，前提是目录_位于 外部_。（为了兼容，go 命令仍然在旧的 GOPATH 模式下运行，即使找到 。有关详细信息[，请参阅 go](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Preliminary_module_support)命令文档。从 Go 1.13 开始，模块模式将是所有发展的默认模式。</font>```go.mod``````$GOPATH/src``````$GOPATH/src``````go.mod```

本文将学习使用模块开发 Go 代码时出现的一系列常见操作：

*   创建新模块。
*   添加依赖项。
*   升级依赖项。
*   添加对新主要版本的依赖项。
*   将依赖项升级到新的主要版本。
*   删除未使用的依赖项。

#### 创建新模块

让我们创建一个新模块。

<font _mstmutation="1" _msthash="306007" _msttexthash="317295095">在 ， 在 目录外的某个地方创建一个新的空目录，然后创建一个新的源文件， ：</font>```$GOPATH/src``````cd``````hello.go```

<code>package hello

func Hello() string {
    return "Hello, world."
}</code> 

<font _mstmutation="1" _msthash="306631" _msttexthash="80238951">让我们也编写一个测试，在 中：</font>```hello_test.go```

<code>package hello

import "testing"

func TestHello(t *testing.T) {
    want := "Hello, world."
    if got := Hello(); got != want {
        t.Errorf("Hello() = %q, want %q", got, want)
    }
}</code> 

<font _mstmutation="1" _msthash="307255" _msttexthash="421944120">此时，目录包含包，但不包含模块，因为没有文件。如果我们现在工作并运行，我们将看到：</font>```go.mod``````/home/gopher/hello``````go test```

<code>$ go test
PASS
ok  	_/home/gopher/hello	0.020s
$</code> 

<font _mstmutation="1" _msthash="307879" _msttexthash="936642356">最后一行总结了整个包测试。由于我们在外部和任何模块之外工作，因此该命令不知道当前目录的导入路径，并且根据目录名称组成一个假的路径： 。</font>```$GOPATH``````go``````_/home/gopher/hello```

<font _mstmutation="1" _msthash="305370" _msttexthash="192692578">让我们使用 ，然后重试，使当前目录成为模块的根目录：</font>```go mod init``````go test```

<code>$ go mod init example.com/hello
go: creating new go.mod: module example.com/hello
$ go test
PASS
ok  	example.com/hello	0.020s
$</code> 

祝贺！您已经编写并测试了第一个模块。

<font _mstmutation="1" _msthash="306306" _msttexthash="42213925">该命令写了一个文件：</font>```go mod init``````go.mod```

<code>$ cat go.mod
module example.com/hello

go 1.12
$</code> 

<font _mstmutation="1" _msthash="306930" _msttexthash="1899839916">该文件仅显示在模块的根目录中。子目录中的包具有导入路径，包括模块路径和子目录路径。例如，如果我们创建了一个子目录 ，我们不需要（也不需要）在那里运行。通过导入路径，将自动识别为模块的一部分。</font>```go.mod``````world``````go mod init``````example.com/hello``````example.com/hello/world```

#### 添加依赖项

Go 模块的主要动机是改进使用其他开发人员编写的代码（即添加依赖性）的体验。

<font _mstmutation="1" _msthash="307866" _msttexthash="113907560">让我们更新我们的导入，并用它来实现：</font>```hello.go``````rsc.io/quote``````Hello```

<code>package hello

import "rsc.io/quote"

func Hello() string {
    return quote.Hello()
}</code> 

现在让我们再次运行测试：

<code>$ go test
go: finding rsc.io/quote v1.5.2
go: downloading rsc.io/quote v1.5.2
go: extracting rsc.io/quote v1.5.2
go: finding rsc.io/sampler v1.3.0
go: finding golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
go: downloading rsc.io/sampler v1.3.0
go: extracting rsc.io/sampler v1.3.0
go: downloading golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
go: extracting golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
PASS
ok  	example.com/hello	0.023s
$</code> 

<font _mstmutation="1" _msthash="306293" _msttexthash="5542927845">该命令使用 中列出的特定依赖项模块版本解析导入。当它遇到 一个未由 中的任何模块提供的包时，该命令会自动备份包含该包的模块，并使用最新版本将它添加到 。（"最新"定义为最新的标记稳定（非[预发行](https://zshipu.com/t?url=https://semver.org/#spec-item-9)）版本，或者最新的标记预发行版本，或者最新的未标记版本。在我们的示例中，解决了模块的新导入。它还下载 了 使用的两个依赖项，即 。文件中仅记录直接依赖项：</font>```go``````go.mod``````import``````go.mod``````go``````go.mod``````go test``````rsc.io/quote``````rsc.io/quote v1.5.2``````rsc.io/quote``````rsc.io/sampler``````golang.org/x/text``````go.mod```

<code>$ cat go.mod
module example.com/hello

go 1.12

require rsc.io/quote v1.5.2
$</code> 

<font _mstmutation="1" _msthash="306917" _msttexthash="391055210">第二个命令不会重复此工作，因为 现在是最新的，下载的模块在本地缓存（在 中）：</font>```go test``````go.mod``````$GOPATH/pkg/mod```

<code>$ go test
PASS
ok  	example.com/hello	0.020s
$</code> 

<font _mstmutation="1" _msthash="307541" _msttexthash="2429521510">请注意，虽然该命令使添加新的依赖项变得快速而简单，但它并非没有成本。您的模块现在_实际上_依赖于关键领域（如正确性、安全性和正确许可）中的新依赖关系，只需举几例。有关更多注意事项，请参阅 Russ Cox 的博客文章"我们的[软件依赖性问题"。](https://zshipu.com/t?url=https://research.swtch.com/deps)</font>```go```

<font _mstmutation="1" _msthash="307853" _msttexthash="614346694">正如我们上面看到的，添加一个直接依赖关系通常也会带来其他间接依赖关系。该命令列出了当前模块及其所有依赖项：</font>```go list -m all```

<code>$ go list -m all
example.com/hello
golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
rsc.io/quote v1.5.2
rsc.io/sampler v1.3.0
$</code> 

<font _mstmutation="1" _msthash="308477" _msttexthash="374954892">在输出中，当前模块（也称为主_模块）_始终是第一行，后跟按模块路径排序的依赖项。</font>```go list```

<font _mstmutation="1" _msthash="305968" _msttexthash="245618815">该版本是伪版本[的示例，](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Pseudo_versions)它是命令针对特定未标记的提交的版本语法。</font>```golang.org/x/text``````v0.0.0-20170915032832-14c0d48ead0c``````go```

<font _mstmutation="1" _msthash="306280" _msttexthash="340501044">除了 ，该命令还维护一个名为的文件，[其中包含特定模块](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Module_downloading_and_verification)版本内容的预期加密哈希：</font>```go.mod``````go``````go.sum```

<code>$ cat go.sum
golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c h1:qgOY6WgZO...
golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c/go.mod h1:Nq...
rsc.io/quote v1.5.2 h1:w5fcysjrx7yqtD/aO+QwRjYZOKnaM9Uh2b40tElTs3...
rsc.io/quote v1.5.2/go.mod h1:LzX7hefJvL54yjefDEDHNONDjII0t9xZLPX...
rsc.io/sampler v1.3.0 h1:7uVkIFmeBqHfdjD+gZwtXXI+RODJ2Wc4O7MPEh/Q...
rsc.io/sampler v1.3.0/go.mod h1:T1hPZKmBbMNahiBKFy5HrXp6adAjACjK9...
$</code> 

<font _mstmutation="1" _msthash="306904" _msttexthash="1162419947">该命令使用该文件来确保这些模块的未来下载检索与第一次下载相同的位，以确保项目所依赖的模块不会意外更改，无论是出于恶意、意外还是其他原因。和 应签入版本控制。</font>```go``````go.sum``````go.mod``````go.sum```

#### 升级依赖项

<font _mstmutation="1" _msthash="307528" _msttexthash="2444931333">使用 Go 模块，版本使用语义版本标记进行引用。语义版本由三个部分组成：主要版本、次要版本和修补程序版本。例如，对于 ，主要版本为 0，次要版本为 1，修补程序版本为 2。让我们演练几个次要版本升级。下一节中，我们将考虑主要版本升级。</font>```v0.1.2```

<font _mstmutation="1" _msthash="307840" _msttexthash="533778518">从 的输出中，我们可以看到我们使用的未标记版本。让我们升级到最新的标记版本，并测试一切仍然有效：</font>```go list -m all``````golang.org/x/text```

<code>$ go get golang.org/x/text
go: finding golang.org/x/text v0.3.0
go: downloading golang.org/x/text v0.3.0
go: extracting golang.org/x/text v0.3.0
$ go test
PASS
ok  	example.com/hello	0.013s
$</code> 

<font _mstmutation="1" _msthash="308464" _msttexthash="146652662">呜呼！一切都过去了让我们再看看一下，文件：</font>```go list -m all``````go.mod```

<code>$ go list -m all
example.com/hello
golang.org/x/text v0.3.0
rsc.io/quote v1.5.2
rsc.io/sampler v1.3.0
$ cat go.mod
module example.com/hello

go 1.12

require (
    golang.org/x/text v0.3.0 // indirect
    rsc.io/quote v1.5.2
)
$</code> 

<font _mstmutation="1" _msthash="306267" _msttexthash="971052888">包已升级到最新标记版本 （）。该文件已更新以指定。注释指示依赖项不直接由此模块使用，仅由其他模块依赖项间接使用。有关详细信息，请参阅。</font>```golang.org/x/text``````v0.3.0``````go.mod``````v0.3.0``````indirect``````go help modules```

<font _mstmutation="1" _msthash="306579" _msttexthash="330084066">现在，让我们尝试升级次要版本。通过运行和运行测试，以同样的方式开始：</font>```rsc.io/sampler``````go get```

<code>$ go get rsc.io/sampler
go: finding rsc.io/sampler v1.99.99
go: downloading rsc.io/sampler v1.99.99
go: extracting rsc.io/sampler v1.99.99
$ go test
--- FAIL: TestHello (0.00s)
    hello_test.go:8: Hello() = "99 bottles of beer on the wall, 99 bottles of beer, ...", want "Hello, world."
FAIL
exit status 1
FAIL	example.com/hello	0.014s
$</code> 

<font _mstmutation="1" _msthash="307203" _msttexthash="391173185">哦 哦！测试失败表明 的最新版本与我们的用法不兼容。让我们列出该模块的可用标记版本：</font>```rsc.io/sampler```

<code>$ go list -m -versions rsc.io/sampler
rsc.io/sampler v1.0.0 v1.2.0 v1.2.1 v1.3.0 v1.3.1 v1.99.99
$</code> 

我们一直在使用v1.3.0;v1.99.99 明显不好。也许我们可以尝试使用 v1.3.1 代替：

<code>$ go get rsc.io/sampler@v1.3.1
go: finding rsc.io/sampler v1.3.1
go: downloading rsc.io/sampler v1.3.1
go: extracting rsc.io/sampler v1.3.1
$ go test
PASS
ok  	example.com/hello	0.022s
$</code> 

<font _mstmutation="1" _msthash="308451" _msttexthash="554082672">请注意参数中的显式。通常，传递给的每个参数都可以使用显式版本;默认值为 ，它解析为前面定义的最新版本。</font>```@v1.3.1``````go get``````go get``````@latest```

#### 添加对新主要版本的依赖项

<font _mstmutation="1" _msthash="309075" _msttexthash="545729314">让我们向包中添加一个新函数：通过调用 返回 Go 并发谚语，该函数由 模块提供。首先我们更新以添加新函数：</font>```func Proverb``````quote.Concurrency``````rsc.io/quote/v3``````hello.go```

<code>package hello

import (
    "rsc.io/quote"
    quoteV3 "rsc.io/quote/v3"
)

func Hello() string {
    return quote.Hello()
}

func Proverb() string {
    return quoteV3.Concurrency()
}</code> 

<font _mstmutation="1" _msthash="306878" _msttexthash="75608624">然后，我们将一个测试添加到 ：</font>```hello_test.go```

<code>func TestProverb(t *testing.T) {
    want := "Concurrency is not parallelism."
    if got := Proverb(); got != want {
        t.Errorf("Proverb() = %q, want %q", got, want)
    }
}</code> 

然后，我们可以测试我们的代码：

<code>$ go test
go: finding rsc.io/quote/v3 v3.1.0
go: downloading rsc.io/quote/v3 v3.1.0
go: extracting rsc.io/quote/v3 v3.1.0
PASS
ok  	example.com/hello	0.024s
$</code> 

<font _mstmutation="1" _msthash="308126" _msttexthash="93341378">请注意，我们的模块现在依赖于 和 ：</font>```rsc.io/quote``````rsc.io/quote/v3```

<code>$ go list -m rsc.io/q...
rsc.io/quote v1.5.2
rsc.io/quote/v3 v3.1.0
$</code> 

<font _mstmutation="1" _msthash="308750" _msttexthash="5324716982">Go 模块的每个不同主要版本（、等）使用不同的模块路径：从 开始，路径必须以主要版本结束。在示例中，不再 ：而是由模块路径标识。此约定称为[语义导入版本控制](https://zshipu.com/t?url=https://research.swtch.com/vgo-import)，它给不兼容的包（具有不同主要版本的包）不同的名称。相反，应该向后兼容 ，因此它重用名称。（在上一节_中_，应该与 向后兼容，但错误或有关模块行为的错误或不正确的客户端假设都可能发生。</font>```v1``````v2``````v2``````v3``````rsc.io/quote``````rsc.io/quote``````rsc.io/quote/v3``````v1.6.0``````rsc.io/quote``````v1.5.2``````rsc.io/quote``````rsc.io/sampler``````v1.99.99``````rsc.io/sampler``````v1.3.0```

<font _mstmutation="1" _msthash="309062" _msttexthash="6630706238">该命令允许生成最多包含任何特定模块路径的一个版本，即最多包含一个主要版本：一个、一个、一个，等等。这为模块作者提供了关于单个模块路径可能重复的清晰规则：程序不可能同时使用 和 生成。同时，允许模块的不同主要版本（因为它们具有不同的路径）使模块使用者能够逐步升级到新的主要版本。在此示例中，我们希望使用 ，但尚未准备好迁移我们的使用 。在大型程序或代码库中，增量迁移的能力尤为重要。</font>```go``````rsc.io/quote``````rsc.io/quote/v2``````rsc.io/quote/v3``````rsc.io/quote v1.5.2``````rsc.io/quote v1.6.0``````quote.Concurrency``````rsc/quote/v3 v3.1.0``````rsc.io/quote v1.5.2```

#### 将依赖项升级到新的主要版本

<font _mstmutation="1" _msthash="306865" _msttexthash="1195358463">让我们完成从使用到仅使用的转换。由于主要版本更改，我们预期某些 API 可能已被删除、重命名或以其他方式以不兼容的方式更改。阅读文档，我们可以看到，已成为：</font>```rsc.io/quote``````rsc.io/quote/v3``````Hello``````HelloV3```

<code>$ go doc rsc.io/quote/v3
package quote // import "rsc.io/quote"

Package quote collects pithy sayings.

func Concurrency() string
func GlassV3() string
func GoV3() string
func HelloV3() string
func OptV3() string
$</code> 

<font _mstmutation="1" _msthash="307489" _msttexthash="177531289">（输出中[还有一](https://zshipu.com/t?url=https://golang.org/issue/30778)个已知错误;显示的导入路径错误地丢弃了 .</font>```/v3```

<font _mstmutation="1" _msthash="307801" _msttexthash="94476252">我们可以更新我们的使用， 以使用：</font>```quote.Hello()``````hello.go``````quoteV3.HelloV3()```

<code>package hello

import quoteV3 "rsc.io/quote/v3"

func Hello() string {
    return quoteV3.HelloV3()
}

func Proverb() string {
    return quoteV3.Concurrency()
}</code> 

然后在这一点上，不再需要重命名导入，因此我们可以撤消：

<code>package hello

import "rsc.io/quote/v3"

func Hello() string {
    return quote.HelloV3()
}

func Proverb() string {
    return quote.Concurrency()
}</code> 

让我们重新运行测试，以确保一切正常：

<code>$ go test
PASS
ok      example.com/hello       0.014s</code>
#### 删除未使用的依赖项

<font _mstmutation="1" _msthash="307164" _msttexthash="203178729">我们已经删除了 的所有用途，但它仍然出现在我们的文件中：</font>```rsc.io/quote``````go list -m all``````go.mod```

<code>$ go list -m all
example.com/hello
golang.org/x/text v0.3.0
rsc.io/quote v1.5.2
rsc.io/quote/v3 v3.1.0
rsc.io/sampler v1.3.1
$ cat go.mod
module example.com/hello

go 1.12

require (
    golang.org/x/text v0.3.0 // indirect
    rsc.io/quote v1.5.2
    rsc.io/quote/v3 v3.0.0
    rsc.io/sampler v1.3.1 // indirect
)
$</code> 

<font _mstmutation="1" _msthash="307788" _msttexthash="2745688387">为什么？因为构建单个包（如 或 ）可以轻松判断何时缺少内容并需要添加，但无法判断何时可以安全地删除某样东西。只有在检查了模块中的所有包以及这些包的所有可能的生成标记组合后，才能删除依赖项。普通生成命令不加载此信息，因此无法安全地删除依赖项。</font>```go build``````go test```

<font _mstmutation="1" _msthash="308100" _msttexthash="88327421">该命令清理这些未使用的依赖项：</font>```go mod tidy```

<code>$ go mod tidy
$ go list -m all
example.com/hello
golang.org/x/text v0.3.0
rsc.io/quote/v3 v3.1.0
rsc.io/sampler v1.3.1
$ cat go.mod
module example.com/hello

go 1.12

require (
    golang.org/x/text v0.3.0 // indirect
    rsc.io/quote/v3 v3.1.0
    rsc.io/sampler v1.3.1 // indirect
)

$ go test
PASS
ok  	example.com/hello	0.020s
$</code>
#### 结论

Go 模块是 Go 中依赖项管理的未来。模块功能现在在所有受支持的 Go 版本中可用（即 Go 1.11 和 Go 1.12 中）。

本文使用 Go 模块介绍了这些工作流：

*   ```go mod init```<font _mstmutation="1" _msthash="488267" _msttexthash="93348879">创建一个新模块，初始化描述它的文件。</font>```go.mod```
*   ```go build```<font _mstmutation="1" _msthash="488657" _msttexthash="143853333">，和其他包生成命令根据需要向 中添加新的依赖项。</font>```go test``````go.mod```
*   ```go list -m all```<font _mstmutation="1" _msthash="489047" _msttexthash="44206539">打印当前模块的依赖项。</font>
*   ```go get```<font _mstmutation="1" _msthash="489437" _msttexthash="149973109">更改依赖项的所需版本（或添加新的依赖项）。</font>
*   ```go mod tidy```<font _mstmutation="1" _msthash="489827" _msttexthash="40871948">删除未使用的依赖项。</font>


