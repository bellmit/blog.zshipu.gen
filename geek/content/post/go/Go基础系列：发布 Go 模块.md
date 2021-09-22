
---
title: Go基础系列：发布 Go 模块
author: 知识铺
date: 2020-11-01 11:08:22+08:00
tags: [go]
---
<font _mstmutation="1" _msthash="291889" _msttexthash="338286585">请注意：这篇文章涵盖了开发，包括。如果你有兴趣，请参阅去[模块：v2和Beyond](/v2-go-modules)。</font>```v1``````v2```

这篇文章在示例中[使用了 Git](https://zshipu.com/t?url=https://git-scm.com/)[mercurial](https://zshipu.com/t?url=https://www.mercurial-scm.org/)[bazaar](https://zshipu.com/t?url=http://wiki.bazaar.canonical.com/)，和其他人也得到支持。

#### 项目设置

对于此帖子，您需要一个现有项目作为示例。因此，从"使用转到模块"文章[末尾的文件](https://zshipu.com/t?url=https://blog.golang.org/using-go-modules)开始：

<code>$ cat go.mod
module example.com/hello

go 1.12

require rsc.io/quote/v3 v3.1.0

$ cat go.sum
golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c h1:qgOY6WgZOaTkIIMiVjBQcw93ERBE4m30iBm00nkL0i8=
golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c/go.mod h1:NqM8EUOU14njkJ3fqMW+pc6Ldnwhi/IjpwHt7yyuwOQ=
rsc.io/quote/v3 v3.1.0 h1:9JKUTTIUgS6kzR9mK1YuGKv6Nl+DijDNIc0ghT58FaY=
rsc.io/quote/v3 v3.1.0/go.mod h1:yEA65RcK8LyAZtP9Kv3t0HmxON59tX3rD+tICJqUlj0=
rsc.io/sampler v1.3.0 h1:7uVkIFmeBqHfdjD+gZwtXXI+RODJ2Wc4O7MPEh/QiW4=
rsc.io/sampler v1.3.0/go.mod h1:T1hPZKmBbMNahiBKFy5HrXp6adAjACjK9JXDnKaTXpA=

$ cat hello.go
package hello

import "rsc.io/quote/v3"

func Hello() string {
    return quote.HelloV3()
}

func Proverb() string {
    return quote.Concurrency()
}

$ cat hello_test.go
package hello

import (
    "testing"
)

func TestHello(t *testing.T) {
    want := "Hello, world."
    if got := Hello(); got != want {
        t.Errorf("Hello() = %q, want %q", got, want)
    }
}

func TestProverb(t *testing.T) {
    want := "Concurrency is not parallelism."
    if got := Proverb(); got != want {
        t.Errorf("Proverb() = %q, want %q", got, want)
    }
}

$</code> 

<font _mstmutation="1" _msthash="305695" _msttexthash="739088701">接下来，创建一个新存储库并添加初始提交。如果要发布自己的项目，请确保包含一个文件。更改为包含 的目录，然后创建存储库：</font>```git``````LICENSE``````go.mod```

<code>$ git init
$ git add LICENSE go.mod go.sum hello.go hello_test.go
$ git commit -m "hello: initial commit"
$</code>
#### 语义版本和模块

<font _mstmutation="1" _msthash="306631" _msttexthash="7363187">[](https://zshipu.com/t?url=https://semver.org)</font>```go.mod```

<font _mstmutation="1" _msthash="306943" _msttexthash="30249726">语义版本具有形式。</font>```vMAJOR.MINOR.PATCH```

*   <font _mstmutation="1" _msthash="485758" _msttexthash="427245793">当您对模块的公共 API 进行[向后不](https://zshipu.com/t?url=https://golang.org/doc/go1compat)兼容的更改时，请增加版本。这只有在绝对必要的时候才应完成。</font>```MAJOR```
*   <font _mstmutation="1" _msthash="486148" _msttexthash="524935723">当您对 API 进行向后兼容更改（如更改依赖关系或添加新函数、方法、结构字段或类型）时，请增加版本。</font>```MINOR```
*   <font _mstmutation="1" _msthash="486538" _msttexthash="299933400">在进行不影响模块的公共 API 或依赖项（如修复 Bug）的小更改后，增加版本。</font>```PATCH```

<font _mstmutation="1" _msthash="307567" _msttexthash="1709242652">您可以通过追加连字符和点分隔标识符（例如 或 ）来指定预发行版本。与预发行版本不同，命令首选普通版本，因此，如果您的模块具有任何正常版本，则用户必须显式请求预发行版本（例如 ）。</font>```v1.0.1-alpha``````v2.2.2-beta.2``````go``````go get example.com/hello@v1.0.1-alpha```

```v0```<font _mstmutation="1" _msthash="307879" _msttexthash="950042106">主要版本和预发行版本不能保证向后兼容性。它们允许您在向用户做出稳定性承诺之前优化 API。但是，主要版本和其他版本需要该主要版本中的向后兼容性。</font>```v1```

<font _mstmutation="1" _msthash="305370" _msttexthash="5948452237">在 中引用的版本可能是存储库中标记的显式版本（例如 ），也可以是基于特定[提交](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Pseudo_versions)（例如 ， 的伪版本）。伪版本是预发行版本的特殊类型。当用户需要依赖于尚未发布任何语义版本标记的项目，或者针对尚未标记的提交进行开发时，伪版本非常有用，但用户不应假定伪版本提供了稳定或经过良好测试的 API。使用显式版本标记模块，向用户发出信号，表明特定版本已全面测试并随时可以使用。</font>```go.mod``````v1.5.2``````v0.0.0-20170915032832-14c0d48ead0c```

<font _mstmutation="1" _msthash="305682" _msttexthash="2473532165">使用版本开始标记存储库后，在开发模块时继续标记新版本非常重要。当用户请求模块的新版本（使用 或）时，命令将选择可用的最大语义版本，即使该版本已使用多年，并且主分支后面有许多更改。继续标记新版本将使您的持续改进可供用户使用。</font>```go get -u``````go get example.com/hello``````go```

不要从存储库中删除版本标记。如果发现版本有错误或安全问题，请发布新版本。如果用户依赖于您已删除的版本，则其生成可能会失败。同样，发布版本后，不要更改或覆盖它。模块[镜像和校验和](https://zshipu.com/t?url=https://blog.golang.org/module-mirror-launch)数据库存储模块、其版本和已签名的加密哈希，以确保给定版本的生成在一段时间中保持可重复性。

#### v0：初始的不稳定版本

<font _mstmutation="1" _msthash="306618" _msttexthash="450694634">让我们用语义版本标记模块。版本不提供任何稳定性保证，因此几乎所有项目都应从优化其公共 API 时开始。</font>```v0``````v0``````v0```

标记新版本有几个步骤：

1.  <font _mstmutation="1" _msthash="609947" _msttexthash="176891299">运行 ，这将删除模块可能累积的任何不再需要的依赖项。</font>```go mod tidy```

2.  <font _mstmutation="1" _msthash="610337" _msttexthash="85205757">运行最后一个时间，以确保一切工作。</font>```go test ./...```

3.  使用 git 标记使用新版本标记[```项目```](https://zshipu.com/t?url=https://git-scm.com/docs/git-tag)。

4.  将新标记推送到源存储库。

<code>$ go mod tidy
$ go test ./...
ok      example.com/hello       0.015s
$ git add go.mod go.sum hello.go hello_test.go
$ git commit -m "hello: changes for v0.1.0"
$ git tag v0.1.0
$ git push origin v0.1.0
$</code> 

<font _mstmutation="1" _msthash="307866" _msttexthash="2881945690">现在，其他项目可以依赖于 。对于您自己的模块，可以运行以确认最新版本可用（此示例模块不存在，因此没有可用的版本）。如果您没有立即看到最新版本，并且正在使用 Go 模块代理（自 Go 1.13 以来的默认值），请在几分钟内重试，为代理提供加载新版本的时间。</font>```v0.1.0``````example.com/hello``````go list -m example.com/hello@v0.1.0```

<font _mstmutation="1" _msthash="308178" _msttexthash="796769545">如果添加到公共 API、对模块进行大改换、或升级其中一个依赖项的次要或版本，请增加下一个版本的版本。例如，之后的下一个版本将是 。</font>```v0``````MINOR``````v0.1.0``````v0.2.0```

<font _mstmutation="1" _msthash="305669" _msttexthash="280430722">如果在现有版本中修复了 Bug，请增加该版本。例如，之后的下一个版本将是 。</font>```PATCH``````v0.1.0``````v0.1.1```

#### v1：第一个稳定版本

<font _mstmutation="1" _msthash="306293" _msttexthash="7505636333">一旦您绝对确定模块的 API 是稳定的，就可以发布 。主要版本向用户传达不会对模块的 API 进行不兼容的更改。他们可以升级到新的次要版本和修补程序版本，并且其代码不应中断。函数和方法签名不会更改，导出的类型不会删除，等等。如果 API 有更改，则它们向后兼容（例如，向结构添加新字段），并将包含在新的次要版本中。如果有错误修复（例如，安全修补程序），它们将包含在修补程序版本中（或作为次要发布的一部分）。</font>```v1.0.0``````v1``````v1```

有时，保持向后兼容性可能会导致 API 尴尬。没关系。不完美的 API 比破坏用户的现有代码更好。

<font _mstmutation="1" _msthash="306917" _msttexthash="169391612">标准库的包是以 API 一致性为成本保持向后兼容性的一个示例。</font>```strings```

*   [```将```](https://zshipu.com/t?url=https://godoc.org/strings#Split)字符串拆分为由分隔符分隔的所有子字符串，并返回这些分隔符之间的子字符串切片。
*   [```拆分```](https://zshipu.com/t?url=https://godoc.org/strings#SplitN)可用于控制要返回的子字符串数。

<font _mstmutation="1" _msthash="307541" _msttexthash="280287254">但是[```，Replace```](https://zshipu.com/t?url=https://godoc.org/strings#Replace)从一开始就计算了要替换的字符串的实例数（与 不同）。</font>```Split```

<font _mstmutation="1" _msthash="307853" _msttexthash="1790871576">给定 和 ，您将期望函数如 和 。但是，我们不能改变现有的不打破调用，我们承诺不这样做。因此，在 Go 1.12 中，我们添加了一个新函数"[```替换所有"。```](https://zshipu.com/t?url=https://godoc.org/strings#ReplaceAll)生成的 API 有点奇怪，因为和行为不同，但这种不一致比中断更改好。</font>```Split``````SplitN``````Replace``````ReplaceN``````Replace``````Split``````Replace```

<font _mstmutation="1" _msthash="308165" _msttexthash="175963931">假设您对 的 API 很满意，并且希望作为第一个稳定版本发布。</font>```example.com/hello``````v1```

<font _mstmutation="1" _msthash="308477" _msttexthash="363262952">标记使用与标记版本相同的过程：运行 和 标记版本，然后将标记推送到源存储库：</font>```v1``````v0``````go mod tidy``````go test ./...```

<code>$ go mod tidy
$ go test ./...
ok      example.com/hello       0.015s
$ git add go.mod go.sum hello.go hello_test.go
$ git commit -m "hello: changes for v1.0.0"
$ git tag v1.0.0
$ git push origin v1.0.0
$</code> 

<font _mstmutation="1" _msthash="306280" _msttexthash="322569104">此时，的 API 已稳定。这向每个人传达我们的 API 是稳定的，他们应该放心地使用它。</font>```v1``````example.com/hello```

