
---
title: Go基础系列：迁移转到模块
author: 知识铺
date: 2020-11-01 11:05:44+08:00
tags: [go]
---
<font _mstmutation="1" _msthash="291590" _msttexthash="2124701813">Go 项目使用各种依赖项管理策略。[dep](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Vendor_Directories)和滑翔[等](https://zshipu.com/t?url=https://github.com/golang/dep)[供应商工具](https://zshipu.com/t?url=https://github.com/Masterminds/glide)很受欢迎，但它们在行为上存在很大差异，而且并不总是很好地协同工作。某些项目将其整个 GOPATH 目录存储在单个 Git 存储库中。其他人只是依赖并期望在 GOPATH 中安装相当新版本的依赖项。</font>```go get```

<font _mstmutation="1" _msthash="291889" _msttexthash="651587872">Go 的模块系统在 Go 1.11 中引入，它提供了命令中内置的官方依赖管理解决方案。本文介绍将项目转换为模块的工具和技术。</font>```go```

<font _mstmutation="1" _msthash="292188" _msttexthash="1041440205">请注意：如果项目已在 v2.0.0 或更高版本标记，则需要在添加文件时更新模块路径。我们将解释如何在不中断您的用户在将来的一篇文章中，重点是 v2 和以后。</font>```go.mod```

#### 迁移到项目中的 Go 模块

在开始过渡到 Go 模块时，项目可能为三种状态之一：

*   一个全新的 Go 项目。
*   具有非模块依赖管理器的已建立的 Go 项目。
*   没有任何依赖项管理器的已建立的 Go 项目。

第一个案例在"使用[Go 模块"中介绍](https://zshipu.com/t?url=https://blog.golang.org/using-go-modules);我们将在这篇文章中讨论后两个。

#### 使用依赖关系管理器

若要转换已使用依赖项管理工具的项目，请运行以下命令：

<code>$ git clone https://github.com/my/project
[...]
$ cd project
$ cat Godeps/Godeps.json
{
    "ImportPath": "github.com/my/project",
    "GoVersion": "go1.12",
    "GodepVersion": "v80",
    "Deps": [
        {
            "ImportPath": "rsc.io/binaryregexp",
            "Comment": "v0.2.0-1-g545cabd",
            "Rev": "545cabda89ca36b48b8e681a30d9d769a30b3074"
        },
        {
            "ImportPath": "rsc.io/binaryregexp/syntax",
            "Comment": "v0.2.0-1-g545cabd",
            "Rev": "545cabda89ca36b48b8e681a30d9d769a30b3074"
        }
    ]
}
$ go mod init github.com/my/project
go: creating new go.mod: module github.com/my/project
go: copying requirements from Godeps/Godeps.json
$ cat go.mod
module github.com/my/project

go 1.12

require rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca
$</code> 

```go mod init```<font _mstmutation="1" _msthash="306943" _msttexthash="728541957">创建一个新的 go.mod 文件，并自动从 导入依赖项，或从[中导入许多其他受支持的格式](https://zshipu.com/t?url=https://go.googlesource.com/go/+/362625209b6cd2bc059b6b0a67712ddebab312d9/src/cmd/go/internal/modconv/modconv.go#9)。参数是模块路径，即可能找到模块的位置。</font>```Godeps.json``````Gopkg.lock``````go mod init```

<font _mstmutation="1" _msthash="307255" _msttexthash="977207946">这是暂停和运行以及继续运行的好去点。以后的步骤可能会修改您的文件，因此，如果您喜欢采用迭代方法，这是最接近预模块依赖项规范的文件。</font>```go build ./...``````go test ./...``````go.mod``````go.mod```

<code>$ go mod tidy
go: downloading rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca
go: extracting rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca
$ cat go.sum
rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca h1:FKXXXJ6G2bFoVe7hX3kEX6Izxw5ZKRH57DFBJmHCbkU=
rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca/go.mod h1:qTv7/COck+e2FymRvadv62gMdZztPaShugOCi3I+8D8=
$</code> 

```go mod tidy```<font _mstmutation="1" _msthash="307879" _msttexthash="2592516199">查找模块中由包传输导入的所有包。它为任何已知模块未提供的包添加新的模块要求，并删除对不提供任何导入包的模块的要求。如果模块提供的包仅由尚未迁移到模块的项目导入，则模块要求将用注释标记。在将文件提交到版本控制之前运行始终是一种好的做法。</font>```// indirect``````go mod tidy``````go.mod```

让我们通过确保代码生成和测试通过：

<code>$ go build ./...
$ go test ./...
[...]
$</code> 

<font _mstmutation="1" _msthash="305994" _msttexthash="3468825620">请注意，其他依赖项管理器可能在单个包或整个存储库（不是模块）级别指定依赖项，并且通常不识别依赖项文件中指定的要求。因此，您可能不会获得与以前完全相同的每个包版本，并且存在升级过去中断更改的风险。因此，对生成的依赖项进行审核时遵循上述命令非常重要。为此，请运行</font>```go.mod```

<code>$ go list -m all
go: finding rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca
github.com/my/project
rsc.io/binaryregexp v0.2.1-0.20190524193500-545cabda89ca
$</code> 

<font _mstmutation="1" _msthash="306618" _msttexthash="2987658856">并将生成的版本与旧的依赖项管理文件进行比较，以确保所选版本是适当的。如果您找到的版本不是你想要的，您可以找出为什么使用 和/或，并使用 升级或降级到正确的版本。（如果您请求的版本比以前选择的版本要旧，则将根据需要降级其他依赖项以保持兼容性。例如，</font>```go mod why -m``````go mod graph``````go get``````go get```

<code>$ go mod why -m rsc.io/binaryregexp
[...]
$ go mod graph | grep rsc.io/binaryregexp
[...]
$ go get rsc.io/binaryregexp@v0.2.0
$</code>
#### 没有依赖项管理器

<font _mstmutation="1" _msthash="307554" _msttexthash="206939005">对于没有依赖项管理系统的 Go 项目，请首先创建一个文件：</font>```go.mod```

<code>$ git clone https://go.googlesource.com/blog
[...]
$ cd blog
$ go mod init golang.org/x/blog
go: creating new go.mod: module golang.org/x/blog
$ cat go.mod
module golang.org/x/blog

go 1.12
$</code> 

<font _mstmutation="1" _msthash="308178" _msttexthash="1548500304">如果没有以前依赖项管理器的配置文件，将创建一个仅包含 和 指令的文件。在此示例中，我们将模块路径设置为，因为这是其自定义[导入路径](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Remote_import_paths)。用户可以使用此路径导入包，我们必须小心不要更改它。</font>```go mod init``````go.mod``````module``````go``````golang.org/x/blog```

<font _mstmutation="1" _msthash="305669" _msttexthash="283867987">指令声明模块路径，该指令声明用于在模块中编译代码的 Go 语言的预期版本。</font>```module``````go```

<font _mstmutation="1" _msthash="305981" _msttexthash="100820954">接下来，运行以添加模块的依赖项：</font>```go mod tidy```

<code>$ go mod tidy
go: finding golang.org/x/website latest
go: finding gopkg.in/tomb.v2 latest
go: finding golang.org/x/net latest
go: finding golang.org/x/tools latest
go: downloading github.com/gorilla/context v1.1.1
go: downloading golang.org/x/tools v0.0.0-20190813214729-9dba7caff850
go: downloading golang.org/x/net v0.0.0-20190813141303-74dc4d7220e7
go: extracting github.com/gorilla/context v1.1.1
go: extracting golang.org/x/net v0.0.0-20190813141303-74dc4d7220e7
go: downloading gopkg.in/tomb.v2 v2.0.0-20161208151619-d5d1b5820637
go: extracting gopkg.in/tomb.v2 v2.0.0-20161208151619-d5d1b5820637
go: extracting golang.org/x/tools v0.0.0-20190813214729-9dba7caff850
go: downloading golang.org/x/website v0.0.0-20190809153340-86a7442ada7c
go: extracting golang.org/x/website v0.0.0-20190809153340-86a7442ada7c
$ cat go.mod
module golang.org/x/blog

go 1.12

require (
    github.com/gorilla/context v1.1.1
    golang.org/x/net v0.0.0-20190813141303-74dc4d7220e7
    golang.org/x/text v0.3.2
    golang.org/x/tools v0.0.0-20190813214729-9dba7caff850
    golang.org/x/website v0.0.0-20190809153340-86a7442ada7c
    gopkg.in/tomb.v2 v2.0.0-20161208151619-d5d1b5820637
)
$ cat go.sum
cloud.google.com/go v0.26.0/go.mod h1:aQUYkXzVsufM+DwF1aE+0xfcU+56JwCaLick0ClmMTw=
cloud.google.com/go v0.34.0/go.mod h1:aQUYkXzVsufM+DwF1aE+0xfcU+56JwCaLick0ClmMTw=
git.apache.org/thrift.git v0.0.0-20180902110319-2566ecd5d999/go.mod h1:fPE2ZNJGynbRyZ4dJvy6G277gSllfV2HJqblrnkyeyg=
git.apache.org/thrift.git v0.0.0-20181218151757-9b75e4fe745a/go.mod h1:fPE2ZNJGynbRyZ4dJvy6G277gSllfV2HJqblrnkyeyg=
github.com/beorn7/perks v0.0.0-20180321164747-3a771d992973/go.mod h1:Dwedo/Wpr24TaqPxmxbtue+5NUziq4I4S80YR8gNf3Q=
[...]
$</code> 

```go mod tidy```<font _mstmutation="1" _msthash="306605" _msttexthash="965903354">添加了模块中包传输导入的所有包的模块要求，并在特定版本上为每个库构建了一个包含校验和的模块。让我们通过确保代码仍在生成和测试仍然通过：</font>```go.sum```

<code>$ go build ./...
$ go test ./...
ok  	golang.org/x/blog	0.335s
?   	golang.org/x/blog/content/appengine	[no test files]
ok  	golang.org/x/blog/content/cover	0.040s
?   	golang.org/x/blog/content/h2push/server	[no test files]
?   	golang.org/x/blog/content/survey2016	[no test files]
?   	golang.org/x/blog/content/survey2017	[no test files]
?   	golang.org/x/blog/support/racy	[no test files]
$</code> 

<font _mstmutation="1" _msthash="307229" _msttexthash="2726895847">请注意，在添加要求时，它会添加模块的最新版本。如果包含后来发布中断更改的依赖项的较旧版本，则可能会在 中看到 错误， 或 中出现错误。如果发生这种情况，请尝试降级到具有 （例如 ，） 的较旧版本，或花时间使模块与每个依赖项的最新版本兼容。</font>```go mod tidy``````GOPATH``````go mod tidy``````go build``````go test``````go get``````go get github.com/broken/module@v1.1.0```

#### 在模块模式下进行测试

迁移到 Go 模块后，某些测试可能需要调整。

<font _mstmutation="1" _msthash="308165" _msttexthash="1105883116">如果测试需要在包目录中写入文件，当包目录位于模块缓存中（即只读）时，它可能会失败。特别是，这可能会导致失败。测试应复制它需要写入临时目录的文件。</font>```go test all```

<font _mstmutation="1" _msthash="308477" _msttexthash="3084254641">如果测试依赖于相对路径 （） 来查找和读取另一个包中的文件，则如果包位于另一个模块中，则测试将失败，该模块将位于模块缓存的版本子目录或指令中指定的路径中。如果是这种情况，您可能需要将测试输入复制到模块中，或者将测试输入从原始文件转换为嵌入在源文件中的数据。</font>```../package-in-another-module``````replace``````.go```

<font _mstmutation="1" _msthash="305968" _msttexthash="982438639">如果测试要求测试中的命令在 GOPATH 模式下运行，则可能会失败。如果是这种情况，您可能需要将文件添加到要测试的源树中，或者显式设置文件。</font>```go``````go.mod``````GO111MODULE=off```

#### 发布版本

最后，您应该标记并发布新模块的发布版本。如果您尚未发布任何版本，则这是可选的，但如果没有官方版本，下游用户将依赖于使用伪版本的特定提交，这可能更难支持。[](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Pseudo_versions)

<code>$ git tag v1.2.0
$ git push origin v1.2.0</code> 

<font _mstmutation="1" _msthash="307216" _msttexthash="3607291766">新文件为模块定义了规范导入路径，并添加了新的最低版本要求。如果用户已在使用正确的导入路径，并且依赖项尚未进行重大更改，则添加文件是向后兼容的，但这是一个重大更改，可能会暴露现有问题。如果您有现有的版本标记，则应增加[次要版本](https://zshipu.com/t?url=https://semver.org/#spec-item-7)。请参阅[发布转到](/publishing-go-modules)模块，了解如何增加和发布版本。</font>```go.mod``````go.mod```

#### 导入和规范化模块路径

<font _mstmutation="1" _msthash="307840" _msttexthash="3645971524">每个模块在其文件中声明其模块路径。引用模块内包的每个语句都必须将模块路径作为包路径的前缀。但是，该命令可能会遇到一个存储库，其中包含模块通过许多不同的[远程导入路径](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Remote_import_paths)。例如，和 解析为包含托管在 go.googlesource.com/lint 的[存储库](https://zshipu.com/t?url=https://go.googlesource.com/lint)。该[```存储库中包含的 go.mod```](https://zshipu.com/t?url=https://go.googlesource.com/lint/+/refs/heads/master/go.mod)文件声明其路径为 ，因此只有该路径对应于有效的模块。</font>```go.mod``````import``````go``````golang.org/x/lint``````github.com/golang/lint``````golang.org/x/lint```

<font _mstmutation="1" _msthash="308152" _msttexthash="3556894835">Go 1.4 提供了一种使用[```//```](https://zshipu.com/t?url=https://golang.org/cmd/go/#hdr-Import_path_checking)导入注释声明规范导入路径的机制，但包作者并不总是提供它们。因此，在模块之前编写的代码可能为模块使用了非规范的导入路径，而不会出现不匹配的错误。使用模块时，导入路径必须与规范模块路径匹配，因此您可能需要更新语句：例如，您可能需要更改为 。</font>```import``````import "github.com/golang/lint"``````import "golang.org/x/lint"```

<font _mstmutation="1" _msthash="308464" _msttexthash="3880206850">另一种情况是，在主要版本 2 或更高版本中，Go 模块的规范路径可能与其存储库路径不同。主要版本超过 1 的 Go 模块必须在其模块路径中包含主要版本的后缀：例如，版本必须具有后缀 。但是，语句可能引用模块中的包，_但没有_后缀。例如，at 的非模块用户可能已将其导入为"作为"，并且需要更新导入路径以包括后缀。</font>```v2.0.0``````/v2``````import``````github.com/russross/blackfriday/v2``````v2.0.1``````github.com/russross/blackfriday``````/v2```

#### 结论

对于大多数用户来说，转换为 Go 模块应该是一个简单明了的过程。由于非规范的导入路径或依赖项内的更改中断，可能会偶尔出现问题。未来的帖子将[探索发布新版本，v2](/publishing-go-modules)和以后，以及调试奇怪情况的方法。

为了提供反馈并帮助塑造 Go 中依赖项管理的未来，请向我们发送[bug 报告](https://zshipu.com/t?url=https://golang.org/issue/new)或[体验报告](https://zshipu.com/t?url=https://golang.org/wiki/ExperienceReports)。


