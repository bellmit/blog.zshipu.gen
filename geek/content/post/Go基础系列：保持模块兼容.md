
---
title: Go基础系列：保持模块兼容
author: 知识铺
date: 2020-11-01 11:11:00+08:00
tags: [go]
---
随着您添加新功能、更改行为和重新考虑模块公共表面的某些部分，模块将随着时间的推移而演变。如[Go 模块：v2 和以后，](/v2-go-modules)对 v1+ 模块的中断更改必须作为主要版本颠簸的一部分（或采用新的模块路径）发生。

但是，发布新的主要版本对用户来说很难。他们必须找到新版本，学习新的 API，并更改他们的代码。有些用户可能永远不会更新，这意味着您必须永远维护代码的两个版本。因此，最好以兼容的方式更改现有包。

在这篇文章中，我们将探讨一些技术，以引入非中断的更改。常见的主题是：添加、不更改或删除。我们还将讨论如何从一开始就设计 API 的兼容性。

#### 添加到函数

通常，重大更改以函数的新参数的形式出现。我们将介绍一些处理此类变化的方法，但首先让我们看看一种不起作用的技术。

在添加具有合理默认值的新参数时，很容易将它们添加为可变参数。扩展函数

<code>func Run(name string)</code> 

<font _mstmutation="1" _msthash="306007" _msttexthash="107425045">与默认为零的附加参数，有人可能会建议</font>```size```

<code>func Run(name string, size ...int)</code> 

<font _mstmutation="1" _msthash="306631" _msttexthash="420655430">理由是所有现有的呼叫站点将继续工作。虽然这是事实，但其他用途可能会中断，像这样：</font>```Run```

<code>package mypkg
var runner func(string) = yourpkg.Run</code> 

<font _mstmutation="1" _msthash="307255" _msttexthash="366795832">原始函数在这里工作，因为它的类型是 ，但新函数的类型是 ，因此赋值在编译时失败。</font>```Run``````func(string)``````Run``````func(string, ...int)```

此示例说明调用兼容性不足以向后兼容性。事实上，不能对函数的签名进行向后兼容的更改。

<font _mstmutation="1" _msthash="307879" _msttexthash="1375993827">添加新函数，而不是更改函数的签名。例如，在引入包后，将 1 作为第一个参数传递给函数已成为常见做法。但是，稳定的 API 无法更改导出的函数以接受 ，因为它将中断该函数的所有用途。</font>```context``````context.Context``````context.Context```

<font _mstmutation="1" _msthash="305370" _msttexthash="230919624">而是添加了新的函数。例如，包的方法的签名是（现在仍然是）</font>```database/sql``````Query```

<code>func (db *DB) Query(query string, args ...interface{}) (*Rows, error)</code> 

<font _mstmutation="1" _msthash="305994" _msttexthash="93497053">创建包时，Go 团队将新方法添加到 ：</font>```context``````database/sql```

<code>func (db *DB) QueryContext(ctx context.Context, query string, args ...interface{}) (*Rows, error)</code> 

为了避免复制代码，旧方法调用新方法：

<code>func (db *DB) Query(query string, args ...interface{}) (*Rows, error) {
    return db.QueryContext(context.Background(), query, args...)
}</code> 

<font _mstmutation="1" _msthash="307242" _msttexthash="1008950631">添加方法允许用户按照自己的节奏迁移到新的 API。由于方法读取方式类似且排序在一起，并且以新方法命名，因此 API 的此扩展不会降低包的可读性或理解性。</font>```Context``````database/sql```

如果您预计函数将来可能需要更多参数，可以通过将可选参数作为函数签名的一部分提前计划。最简单的方法是添加单个结构参数，如加密[/tls。拨号](https://zshipu.com/t?url=https://pkg.go.dev/crypto/tls?tab=doc#Dial)功能可以：

<code>func Dial(network, addr string, config *Config) (*Conn, error)</code> 

<font _mstmutation="1" _msthash="308178" _msttexthash="3281533086">由 执行的 TLS 握手需要网络和地址，但它具有许多其他参数，且默认为合理。传递 的 for 使用这些默认值;传递包含某些字段集的结构将覆盖这些字段的默认值。将来，添加新的 TLS 配置参数只需要在结构上设置一个新字段，该更改向后兼容（几乎总是-请参阅下面的"维护结构兼容性"）。</font>```Dial``````nil``````config``````Config``````Config```

<font _mstmutation="1" _msthash="305669" _msttexthash="968448182">有时，可以通过使选项结构方法接收器来组合添加新函数和添加选项的技术。考虑包在网络地址侦听的能力的演变。在 Go 1.11 之前，包只提供了一个带签名的功能</font>```net``````net``````Listen```

<code>func Listen(network, address string) (Listener, error)</code> 

<font _mstmutation="1" _msthash="306293" _msttexthash="4530637813">对于 Go 1.11，在侦听中添加了两个功能：传递上下文，并允许调用方提供"控制函数"，以在创建后但在绑定之前调整原始连接。结果可能是一个新的函数，它采取了上下文、网络、地址和控制功能。相反，包作者添加了[```一个侦听配置```](https://zshipu.com/t?url=https://pkg.go.dev/net@go1.11?tab=doc#ListenConfig)结构，预计有一天可能需要更多的选项。他们不是用繁琐的名称定义新的顶级函数，而是将方法添加到：</font>```net``````Listen``````ListenConfig```

<code>type ListenConfig struct {
    Control func(network, address string, c syscall.RawConn) error
}

func (*ListenConfig) Listen(ctx context.Context, network, address string) (Listener, error)</code> 

将来提供新选项的另一种方式是"选项类型"模式，其中选项作为可变参数传递，每个选项都是一个函数，用于更改所构造值的状态。他们更详细地描述了罗布派克后[自我引用函数和选项的设计](https://zshipu.com/t?url=https://commandcenter.blogspot.com/2014/01/self-referential-functions-and-design.html)。一个广泛使用的例子[google.golang.org/grpc](https://zshipu.com/t?url=https://pkg.go.dev/google.golang.org/grpc?tab=doc)的[拨号选项](https://zshipu.com/t?url=https://pkg.go.dev/google.golang.org/grpc?tab=doc#DialOption)。

<font _mstmutation="1" _msthash="307229" _msttexthash="1312224875">选项类型在函数参数中实现与结构选项相同的角色：它们是传递行为修改配置的可扩展方式。决定选择哪种因素很大程度上取决于风格问题。请考虑 gRPC 选项类型的以下简单用法：</font>```DialOption```

<code>grpc.Dial("some-target",
  grpc.WithAuthority("some-authority"),
  grpc.WithMaxDelay(time.Second),
  grpc.WithBlock())</code> 

这也可以作为结构选项实现：

<code>notgrpc.Dial("some-target", &notgrpc.Options{
  Authority: "some-authority",
  MaxDelay:  time.Minute,
  Block:     true,
})</code> 

<font _mstmutation="1" _msthash="308477" _msttexthash="5191723563">功能选项有一些缺点：它们要求在每次调用的选项之前写入包名称;它们会增加包命名空间的大小;如果提供两次相同的选项， 则不清楚该行为应该是什么。另一方面，使用选项结构的函数需要一个参数，该参数可能几乎总是 ，有些人觉得该参数没有吸引力。当类型的零值具有有效含义时，指定选项应具有其默认值（通常需要指针或额外的布尔字段）是笨拙的。</font>```nil```

这两种选择都是确保模块公共 API 未来可扩展性的合理选择。

#### 使用接口

有时，新功能需要更改公开接口：例如，需要使用新方法扩展接口。直接添加到接口是一个突破性的变化，但是，我们如何支持在公开公开的接口上采用新方法呢？

基本思想是使用新方法定义新接口，然后无论使用旧接口，动态检查所提供的类型是较旧类型还是较新的类型。

<font _mstmutation="1" _msthash="307216" _msttexthash="2178848776">让我们用存档/tar 包中的示例[```来说明这一```](https://zshipu.com/t?url=https://pkg.go.dev/archive/tar?tab=doc)点。[```焦油。NewReader```](https://zshipu.com/t?url=https://pkg.go.dev/archive/tar?tab=doc#NewReader)接受 ，但随着时间的推移，Go 团队意识到，如果可以调用[```Seek，```](https://zshipu.com/t?url=https://pkg.go.dev/io?tab=doc#Seeker)从一个文件头跳到下一个文件头会更有效率。但是，他们不能向 中添加方法：这将破坏 的所有实现者。</font>```io.Reader``````Seek``````io.Reader``````io.Reader```

<font _mstmutation="1" _msthash="307528" _msttexthash="1077876943">另一个排除选项是更改为接受[```io。ReadSeeker```](https://zshipu.com/t?url=https://pkg.go.dev/io?tab=doc#ReadSeeker)而不是 ，因为它同时支持方法和 （通过 ）但是，正如我们上面看到的，更改函数签名也是一个突破性的变化。</font>```tar.NewReader``````io.Reader``````io.Reader``````Seek``````io.Seeker```

<font _mstmutation="1" _msthash="307840" _msttexthash="261528293">因此，他们决定保持签名不变，但在方法中键入检查（和支持）：</font>```tar.NewReader``````io.Seeker``````tar.Reader```

<code>package tar

type Reader struct {
  r io.Reader
}

func NewReader(r io.Reader) *Reader {
  return &Reader{r: r}
}

func (r *Reader) Read(b []byte) (int, error) {
  if rs, ok := r.r.(io.Seeker); ok {
    // Use more efficient rs.Seek.
  }
  // Use less efficient r.r.Read.
}</code> 

（[有关实际代码，请参阅 reader. go。](https://zshipu.com/t?url=https://github.com/golang/go/blob/60f78765022a59725121d3b800268adffe78bde3/src/archive/tar/reader.go#L837)

当您遇到要将方法添加到现有接口的情况下，您可能能够遵循此策略。首先使用新方法创建新接口，或使用新方法标识现有接口。接下来，确定需要支持它的相关函数，键入第二个接口的检查，并添加使用它的代码。

此策略仅在没有新方法的旧接口仍受支持时才有效，从而限制了模块的未来可扩展性。

在可能的情况下，最好完全避免此类问题。例如，在设计构造函数时，更喜欢返回具体类型。使用具体类型允许您在将来添加方法，而不会破坏用户，这与接口不同。该属性允许您的模块在将来更容易扩展。

提示：如果您确实需要使用接口，但不打算让用户实现它，可以添加未出口的方法。这样可以防止包外部定义的类型在不嵌入的情况下满足界面，从而释放您以后添加方法的自由，而不会破坏用户实现。例如，请参阅[```测试。TB```的```私有（） 函数```](https://zshipu.com/t?url=https://github.com/golang/go/blob/83b181c68bf332ac7948f145f33d128377a09c42/src/testing/testing.go#L564-L567)。

<code>type TB interface {
    Error(args ...interface{})
    Errorf(format string, args ...interface{})
    // ...

    // A private method to prevent users implementing the
    // interface and so future additions to it will not
    // violate Go 1 compatibility.
    private()
}</code> 

这个话题在乔纳森阿姆斯特丹的"检测不兼容的API变化"谈话（视频，幻灯片）中[也进行了](https://zshipu.com/t?url=https://www.youtube.com/watch?v=JhdL5AkH-AQ)[更详细的探讨](https://zshipu.com/t?url=https://github.com/gophercon/2019-talks/blob/master/JonathanAmsterdam-DetectingIncompatibleAPIChanges/slides.pdf)。

#### 添加配置方法

到目前为止，我们已经讨论过公开中断的更改，其中更改类型或函数将导致用户的代码停止编译。但是，行为更改也会破坏用户，即使用户代码继续编译。例如，许多用户期望[```json。解码```](https://zshipu.com/t?url=https://pkg.go.dev/encoding/json?tab=doc#Decoder)器忽略 JSON 中不在参数结构中的字段。当 Go 团队想要在这种情况下返回错误时，他们必须小心。在没有选择加入机制的情况下这样做意味着许多依赖这些方法的用户可能会开始接收以前没有的错误。

<font _mstmutation="1" _msthash="308451" _msttexthash="1262112163">因此，他们不是改变所有用户的行为，而是向结构中添加了一个配置方法：[```解码器.Disallow未知Fields。```](https://zshipu.com/t?url=https://pkg.go.dev/encoding/json?tab=doc#Decoder.DisallowUnknownFields)调用此方法会选择用户加入新行为，但这样做会保留现有用户的旧行为。</font>```Decoder```

#### 维护结构兼容性

我们在上面看到，对函数签名的任何更改都是一个突破性的变化。结构的情况要好得多。如果具有导出的结构类型，则几乎总是可以添加字段或删除未导出的字段，而不会破坏兼容性。添加字段时，请确保其零值有意义并保留旧行为，以便不设置字段的现有代码继续工作。

<font _mstmutation="1" _msthash="306566" _msttexthash="2165522372">回想一下，该包的作者在 Go 1.11 中添加了该包，因为他们认为可能会有更多的选项。事实证明他们是对的。在 Go 1.13 中，[```添加了 KeepAlive```](https://zshipu.com/t?url=https://pkg.go.dev/net@go1.13?tab=doc#ListenConfig)字段，以允许禁用保持活动状态或更改其周期。默认值为 0 将保留启用默认期间保持活动的原始行为。</font>```net``````ListenConfig```

<font _mstmutation="1" _msthash="306878" _msttexthash="3405920622">有一种微妙的方式，新字段可以意外中断用户代码。如果结构中的所有字段类型都是可比较的，即这些类型的值可以与映射键进行比较并用作映射键，则整个结构类型也是可比较的。在这种情况下，添加不可比较类型的新字段将使整体结构类型不可比较，从而破坏比较该结构类型的值的任何代码。</font>```==``````!=```

为了保持结构的可比性，不要向其添加非可比字段。您可以为此编写一个测试，或者依靠即将推出[的 go 发行工具](https://zshipu.com/t?url=https://pkg.go.dev/golang.org/x/exp/cmd/gorelease?tab=doc)来捕获它。

首先要防止比较，请确保结构具有非可比字段。它可能已经有一个 - 没有切片，地图或函数类型是可比的 - 但如果没有，可以添加一个类似：

<code>type Point struct {
        _ [0]func()
        X int
        Y int
}</code> 

<font _mstmutation="1" _msthash="308126" _msttexthash="364931385">类型无法比较，零长度数组不占用任何空间。我们可以定义一个类型来阐明我们的意图：</font>```func()```

<code>type doNotCompare [0]func()

type Point struct {
        doNotCompare
        X int
        Y int
}</code> 

<font _mstmutation="1" _msthash="308750" _msttexthash="2722644899">你应该在你的结构中使用吗？如果您已经定义了要用作指针的结构，也就是说，它有指针方法，也许还有一个返回指针的构造函数，那么添加字段可能是过头了。指针类型的用户了解该类型的每个值都是不同的：如果他们想要比较两个值，他们应该比较指针。</font>```doNotCompare``````NewXXX``````doNotCompare```

<font _mstmutation="1" _msthash="309062" _msttexthash="2535006955">如果您正在定义一个结构，旨在直接用作值，如我们的示例，则您通常希望它是可比较的。在不常见的情况下，您有一个不需要比较的值结构，那么添加一个字段将为您提供以后更改结构的自由，而不必担心打破比较。缺点是，该类型不能用作地图键。</font>```Point``````doNotCompare```

#### 结论

从头开始规划 API 时，请仔细考虑 API 将来对新更改的可扩展性。当您确实需要添加新功能时，请记住以下规则：添加、不更改或删除，请记住异常情况 — 接口、函数参数和返回值不能以向后兼容的方式添加。

如果您需要大幅更改 API，或者 API 在添加更多功能时开始失去焦点，则可能是新的主要版本的时间。但大多数时候，进行向后兼容的更改很容易，并避免给用户带来痛苦。
