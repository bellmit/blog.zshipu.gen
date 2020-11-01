
---
title: Go基础系列：Go模块v2 和 Beyond
author: 知识铺
date: 2020-11-01 11:10:05+08:00
tags: [go]
---
随着成功的项目的成熟和新的要求被添加，过去的功能和设计决策可能会停止意义。开发人员可能希望通过删除已弃用函数、重命名类型或将复杂包拆分为可管理部分来整合他们学到的经验教训。这些类型的更改需要下游用户努力将代码迁移到新的 API，因此不应在不考虑收益大于成本的情况下进行这些更改。

<font _mstmutation="1" _msthash="291889" _msttexthash="2460448887">对于仍在实验的项目（主要版本）用户预计偶尔会发生重大更改。对于被宣布为稳定的项目（主要版本或更高版本），必须在新的主要版本中完成重大更改。本文将探讨主要版本语义、如何创建和发布新的主要版本，以及如何维护模块的多个主要版本。</font>```v0``````v1```

#### 主要版本和模块路径

模块在 Go 中正式化了一个重要原则，[**导入兼容性规则**](https://zshipu.com/t?url=https://research.swtch.com/vgo-import)：

<code>If an old package and a new package have the same import path,
the new package must be backwards compatible with the old package.</code> 

<font _mstmutation="1" _msthash="305383" _msttexthash="3508578489">根据定义，新的主要版本的包与以前的版本不向后兼容。这意味着模块的新主要版本必须具有与以前版本的不同的模块路径。从 开始，主要版本必须出现在模块路径的末尾（在文件中的语句中声明）。例如，当模块的作者开发时，他们使用了新的模块路径。想要使用的用户必须将包导入和模块要求更改为 。</font>```v2``````module``````go.mod``````github.com/googleapis/gax-go``````v2``````github.com/googleapis/gax-go/v2``````v2``````github.com/googleapis/gax-go/v2```

<font _mstmutation="1" _msthash="305695" _msttexthash="8534931418">对主要版本后缀需求是 Go 模块与大多数其他依赖项管理系统不同的方法之一。解决钻石依赖性问题[需要后缀](https://zshipu.com/t?url=https://research.swtch.com/vgo-import#dependency_story)。在 Go 模块[gopkg.in，](https://zshipu.com/t?url=http://gopkg.in)允许包维护者遵循我们现在所说的导入兼容性规则。使用 gopkg.in，如果依赖于导入的包和另一个导入的包，则没有冲突，因为两个包具有不同的导入路径 - 它们使用版本后缀，就像使用 Go 模块一样。由于 gopkg.in与 Go 模块共享相同的版本后缀方法，因此 Go 命令接受 in 作为有效的主要版本后缀。这是与用户兼容的特殊情况：gopkg.in域中的模块需要斜杠后缀，如 。</font>```gopkg.in/yaml.v1``````gopkg.in/yaml.v2``````yaml``````.v2``````gopkg.in/yaml.v2``````/v2```

#### 主要版本策略

<font _mstmutation="1" _msthash="306319" _msttexthash="152639565">建议的策略是在以主要版本后缀命名的目录中开发模块。</font>```v2+```

<code>github.com/googleapis/gax-go @ master branch
/go.mod    → module github.com/googleapis/gax-go
/v2/go.mod → module github.com/googleapis/gax-go/v2</code> 

<font _mstmutation="1" _msthash="306943" _msttexthash="748836296">此方法与不知道模块的工具兼容：存储库中的文件路径与模式中预期的路径相匹配。此策略还允许在不同目录中一起开发所有主要版本。</font>```go get``````GOPATH```

<font _mstmutation="1" _msthash="307255" _msttexthash="1322343516">其他策略可能将主要版本保留在单独的分支上。但是，如果源代码位于存储库的默认分支（通常），则不具有版本感知功能的工具（包括模式下的命令）可能无法区分主要版本。</font>```v2+``````master``````go``````GOPATH```

<font _mstmutation="1" _msthash="307567" _msttexthash="751615813">本文中的示例将遵循主要版本子目录策略，因为它提供了最大的兼容性。我们建议模块作者遵循此策略，只要他们有用户在模式下开发。</font>```GOPATH```

#### 发布 v2 及以后

<font _mstmutation="1" _msthash="305370" _msttexthash="29907904">本文用作示例：</font>```github.com/googleapis/gax-go```

<code>$ pwd
/tmp/gax-go
$ ls
CODE_OF_CONDUCT.md  call_option.go  internal
CONTRIBUTING.md     gax.go          invoke.go
LICENSE             go.mod          tools.go
README.md           go.sum          RELEASING.md
header.go
$ cat go.mod
module github.com/googleapis/gax-go

go 1.9

require (
    github.com/golang/protobuf v1.3.1
    golang.org/x/exp v0.0.0-20190221220918-438050ddec5e
    golang.org/x/lint v0.0.0-20181026193005-c67002cb31c3
    golang.org/x/tools v0.0.0-20190114222345-bf090417da8b
    google.golang.org/grpc v1.19.0
    honnef.co/go/tools v0.0.0-20190102054323-c2f93a96b099
)
$</code> 

<font _mstmutation="1" _msthash="305994" _msttexthash="194723438">若要在 上开始开发，我们将创建一个新目录，并复制我们的包。</font>```v2``````github.com/googleapis/gax-go``````v2/```

<code>$ mkdir v2
$ cp *.go v2/
building file list ... done
call_option.go
gax.go
header.go
invoke.go
tools.go

sent 10588 bytes  received 130 bytes  21436.00 bytes/sec
total size is 10208  speedup is 0.95
$</code> 

<font _mstmutation="1" _msthash="306618" _msttexthash="238143269">现在，让我们通过复制当前文件并添加后缀到模块路径来创建 v2 文件：</font>```go.mod``````go.mod``````v2/```

<code>$ cp go.mod v2/go.mod
$ go mod edit -module github.com/googleapis/gax-go/v2 v2/go.mod
$</code> 

<font _mstmutation="1" _msthash="307242" _msttexthash="2010426496">请注意，版本被视为与版本不同的模块：两者可能共存于同一版本。因此，如果您的模块有多个包，您应该更新它们以使用新的导入路径：否则，您的模块将取决于您的模块。例如，若要更新对 的所有引用，可以使用 和 ：</font>```v2``````v0 / v1``````v2+``````/v2``````v2+``````v0 / v1``````github.com/my/project``````github.com/my/project/v2``````find``````sed```

<code>$ find . -type f \
    -name '*.go' \
    -exec sed -i -e 's,github.com/my/project,github.com/my/project/v2,g' {} \;
$</code> 

<font _mstmutation="1" _msthash="307866" _msttexthash="2538814486">现在我们有一个模块，但我们希望在发布版本之前进行试验并进行更改。在发布（或任何没有预发行后缀的版本）之前，我们可以在决定新的 API 时进行开发和进行重大更改。如果我们希望用户能够在正式实现新 API 之前试用新 API，我们可以发布预发行版本：</font>```v2``````v2.0.0``````v2```

<code>$ git tag v2.0.0-alpha.1
$ git push origin v2.0.0-alpha.1
$</code> 

<font _mstmutation="1" _msthash="305669" _msttexthash="351922961">一旦我们满意我们的API，并确保我们不需要任何其他重大的变化，我们可以标记：</font>```v2``````v2.0.0```

<code>$ git tag v2.0.0
$ git push origin v2.0.0
$</code> 

<font _mstmutation="1" _msthash="306293" _msttexthash="562376672">此时，现在有两个主要版本需要维护。向后兼容的更改和 Bug 修复将导致新的次要和修补程序版本（例如、等）。</font>```v1.1.0``````v2.0.1```

#### 结论

主要版本更改会导致开发和维护开销，并且需要下游用户的投资才能迁移。项目越大，这些间接费用往往越大。主要版本更改应仅在确定令人信服的原因之后进行。一旦确定了重大变革的令人信服的理由，我们建议在主分支中开发多个主要版本，因为它与更广泛的现有工具兼容。


