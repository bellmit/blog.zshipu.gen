
---
title: Golang实践：使用 Go+ 第 1 部分创建微服务
author: 知识铺
date: 2020-10-13 22:32:37+08:00
tags: [golang]
---

<font _mstmutation="1" _msthash="39273" _msttexthash="7523966125">来自JavaScript的背景，我一直想学习一种静态类型的编程语言，今年早些时候，我拿起Golang后，阅读了有关语言的评论，Golang得到了谷歌的支持。哦， 当然， 流行的 Devops 工具， 如码头， 库伯内特， Terraform， 是用Golang建造的。在通过 freecodecamp 从这个[令人敬畏](https://zshipu.com/t?url=https://www.youtube.com/watch?v=YS4e4q9oBaU&ab_channel=freeCodeCamp.org)的教程中选取基础知识后，我决定构建一个生产级别的微服务体系结构。该项目将具有单元测试、CI/CD 集成和健壮的体系结构，这些架构将来可以扩展。前端将写在React中。</font>

<font _mstmutation="1" _msthash="28314" _msttexthash="2655542422">这将是一个多部分博客，记录了整个体系结构的创建。代码将托管在这里[：https://github.com/nandangrover/go-microservices。](https://zshipu.com/t?url=https://github.com/nandangrover/go-microservices)本系列的第一部分，这是这个博客文档可以在此分支[找到](https://zshipu.com/t?url=https://github.com/nandangrover/go-microservices/tree/microservices_basic_1)。我会使用 Ubuntu 的系列， 但Golang坐在其他 Os 以及， 所以它不应该是一个问题。</font>

<font _mstmutation="1" _msthash="33384" _msttexthash="5551259012">我选择的代码编辑器是视觉工作室，我建议你使用它。它有许多开箱即用的好处。Visual Studio 代码支持"开箱即用"突出显示的 Go 语法。vscode-go[插件提供了其他功能](https://zshipu.com/t?url=https://github.com/Microsoft/vscode-go)，该插件与十几种标准 Go 工具集成。如果您没有设置 GOPATH，插件将要求您在尝试编辑 Go 语言文件时尽快设置它;您可以为项目和/或系统环境设置它。如果您没有安装 Go 工具，插件将要求将它们安装在 GOPATH 确定的标准位置。</font>

# <font _mstmutation="1" _msthash="27612" _msttexthash="29193541">文件结构如何？</font>

<font _mstmutation="1" _msthash="24414" _msttexthash="901021823">我的 go 工作区将转到二进制文件以及我的个人项目分开。在我看来，这让工作空间变得不那么杂乱无章。我们将利用 GOPATH 环境变量来形成这样的工作区。</font>



![image-20211005082249193](https://cdn.jsdelivr.net/gh/zshipu/images/202110050822543.png)



<font _mstmutation="1" _msthash="35256" _msttexthash="329389970">如上图所示，go 库/二进制文件存储在 golib 文件夹中，而我们的个人项目将存储在 goCode 中。</font>

<font _mstmutation="1" _msthash="22490" _msttexthash="466665030">现在，让我们看看 goCode 文件夹。它由一个 go-microservices 目录组成，该目录以相同的名称推送在 git 上。</font>



![image-20211005082324707](https://cdn.jsdelivr.net/gh/zshipu/images/202110050823288.png)



<font _mstmutation="1" _msthash="28444" _msttexthash="297809564">它包含一个 main.go 文件和一个名为处理程序的文件夹。我们有我们的 gitgnore 和 README.md GitHub 的一个。</font>

# <font _mstmutation="1" _msthash="29549" _msttexthash="17330404">深入到代码中</font>

<font _mstmutation="1" _msthash="32045" _msttexthash="306491783">让我们看看我们的 main.go 文件，它包含构建两个简单的微服务的逻辑 - 你好再见。</font>

func main() {
 l := log.New(os.Stdout, "product-api", log.LstdFlags)
 hh := handlers.NewHello(l)
 gh := handlers.NewGoodbye(l)sm := http.NewServeMux()
 sm.Handle("/", hh)
 sm.Handle("/goodbye", gh)s := &http.Server{
  Addr:         ":9090",
  Handler:      sm,
  IdleTimeout:  120 * time.Second,
  ReadTimeout:  1 * time.Second,
  WriteTimeout: 1 * time.Second,
 }
 // wrapping ListenAndServe in gofunc so it's not going to block
 go func() {
  err := s.ListenAndServe()
  if err != nil {
   l.Fatal(err)
  }
 }()// make a new channel to notify on os interrupt of server (ctrl + C)
 sigChan := make(chan os.Signal)
 signal.Notify(sigChan, os.Interrupt)
 signal.Notify(sigChan, os.Kill)// This blocks the code until the channel receives some message
 sig := <-sigChan
 l.Println("Received terminate, graceful shutdown", sig)
 // Once message is consumed shut everything down
 // Gracefully shuts down all client requests. Makes server more reliable
 tc, cancel := context.WithTimeout(context.Background(), 30*time.Second)
 defer cancel()
 s.Shutdown(tc)
}

<font _mstmutation="1" _msthash="43823" _msttexthash="672819459">我们首先通过调用日志创建新记录器。新增功能。我们可以有多个记录器在未来，所以我们创建一个简单的记录器的名称产品api开始。</font>

<font _mstmutation="1" _msthash="22945" _msttexthash="3773283020">下一步是使用记录器初始化我们的处理程序。处理程序是我们的自定义方法，实现处理程序接口。在内部，在 http 模块中，Handler 接口实现 ServeHTTP 方法，该方法又接受 http。响应编写器和指向 *http 的指针。请求。Golang 很好地记录了 http 服务器，您可以查看其官方文档中的处理程序[接口，](https://zshipu.com/t?url=https://golang.org/src/net/http/server.go)以更好地了解 http 模块的内部工作。</font>

## <font _mstmutation="1" _msthash="44499" _msttexthash="43058340">运行我们的服务器和服务Mux</font>

<font _mstmutation="1" _msthash="27729" _msttexthash="1303150719">而不是使用 http 创建新服务器。ListenAndServe （"9090"），我们使用很少使用的 NewServeMux 函数与指向 http 的指针相结合。用于自定义服务器的服务器。名称描述的 NewServeMux 返回一个 ServeMux。</font>

<font _mstmutation="1" _msthash="35139" _msttexthash="1128797293">ServeMux 是 HTTP 请求多路复用器。它根据已注册模式的列表匹配每个传入请求的 URL，并调用与 URL 最匹配的模式的处理程序。你可以在官方文档中阅读更多[关于它。](https://zshipu.com/t?url=https://golang.org/pkg/net/http/#ServeMux)</font>

sm := http.NewServeMux()
sm.Handle("/", hh)
sm.Handle("/goodbye", gh)

s := &http.Server{
  Addr:         ":9090",
  Handler:      sm,
  IdleTimeout:  120 * time.Second,
  ReadTimeout:  1 * time.Second,
  WriteTimeout: 1 * time.Second,
 }
 // wrapping ListenAndServe in gofunc so it's not going to block
 go func() {
  err := s.ListenAndServe()
  if err != nil {
   l.Fatal(err)
  }
 }()

<font _mstmutation="1" _msthash="33605" _msttexthash="6553513252">服务器定义运行 HTTP 服务器的参数。使用初始参数初始化后，我们调用 ListenandServe 函数。这将在指定的端口中启动我们的 http 服务器，该端口目前为 9090。我们为什么要用一条古例来包装这个？ListenandServe 是一个阻塞代码。它阻止该过程，因此不会执行该行下方的任何东西。Go 程序本质上是非阻塞的。这样，服务器可以在单独的 CPU 进程中启动。这也是我们必须采取的第一步，以便在 Go 中运行多台服务器。</font>

> <font _mstmutation="1" _msthash="28743" _msttexthash="1585112984">💡_与__方法调用__不同，方法调用不需要任何参数，因为服务器的配置存在于结构__本身中。函数__内部使用函数在__地址上__创建侦听器__，函数返回 和__函数一__起使用它，使用字段值__（ServeMux 对象）侦听传入连接。_</font>```_http.ListenAndServe(addr string, handler Handler)_``````_server._[_ListenAndServe_](https://zshipu.com/t?url=https://golang.org/pkg/net/http/#Server.ListenAndServe)_()_``````_server_``````_server.ListenAndServe_``````_tcp_``````_addr_``````_net._[_Listen_](https://zshipu.com/t?url=https://golang.org/pkg/net/#Listen)``````_net._[_Listener_](https://zshipu.com/t?url=https://golang.org/pkg/net/#Listener)``````_server._[_Serve_](https://zshipu.com/t?url=https://golang.org/pkg/net/http/#Server.Serve)``````_server.Handler_```

## <font _mstmutation="1" _msthash="37674" _msttexthash="23249889">正常关闭服务器</font>

<font _mstmutation="1" _msthash="40261" _msttexthash="6431144005">为什么关闭服务器非常重要？假设客户端已发送请求以将其映像保存在数据库中。同时，我们必须做一些维护工作，我们关闭服务器。映像在后端应有多个调用来处理它。第一个是 aws， 以实际保存它， 并得到文件 ID 和链接。假设此部分已完成执行，但为了将映像注册为已保存，我们不必将 aws 数据保存在内部数据库中。此时，服务器将停止。因此，映像保存在 aws 中，但我们不知道，当服务器在执行客户端请求时停止时。</font>

<font _mstmutation="1" _msthash="28730" _msttexthash="438132370">为了防止发生此类情况，我们必须正常关闭服务器，以便处理所有当前处于活动状态的客户端请求。</font>

<font _mstmutation="1" _msthash="33774" _msttexthash="3662126364">关闭正常关闭服务器，而不会中断任何活动连接。关闭的工作原理是首先关闭所有打开的侦听器，然后关闭所有空闲连接，然后无限期地等待连接返回到空闲状态，然后关闭。如果提供的上下文在关闭完成之前过期，则"关机"将返回上下文的错误，否则，它将返回关闭服务器的基础侦听器返回的任何错误。</font>

<font _mstmutation="1" _msthash="39975" _msttexthash="688530167">为了触发关机，我们侦听来自 os 的中断信号。我们通过传递 os 创建一个 go 通道。信号。通知用于注册以中断和终止来自服务器的信号。</font>

<font _mstmutation="1" _msthash="22295" _msttexthash="1650977952">去通道是自然阻塞的。因此，如果我们从 out sigChan 读取消息，则它随后会阻止它下面的所有代码。收到中断信号后，我们将打印关机消息并创建 30 秒的超时上下文。我们将此传递给我们的服务器。关机功能。</font>

<font _mstmutation="1" _msthash="23855" _msttexthash="502143031">关闭方法需要**传入请求**的基本上下文。如果尚未配置结构的字段，可以使用 ，因为它是该字段的默认值。</font>```[BaseContext](https://zshipu.com/t?url=https://golang.org/pkg/net/http/#Server.BaseContext)``````Server``````context.[Background](https://zshipu.com/t?url=https://golang.org/pkg/context/#Background)()``````BaseContext```

// make a new channel to notify on os interrupt of server (ctrl + C)
 sigChan := make(chan os.Signal)
 signal.Notify(sigChan, os.Interrupt)
 signal.Notify(sigChan, os.Kill)// This blocks the code until the channel receives some message
 sig := <-sigChan
 l.Println("Received terminate, graceful shutdown", sig)
 // Once message is consumed shut everything down
 // Gracefully shuts down all client requests. Makes server more reliable
 tc, cancel := context.WithTimeout(context.Background(), 30*time.Second)
 defer cancel()
 s.Shutdown(tc)
## <font _mstmutation="1" _msthash="33007" _msttexthash="7750756">处理器</font>

<font _mstmutation="1" _msthash="34619" _msttexthash="1880634288">如前所述，处理程序是我们的自定义方法，实现处理程序接口。以下代码显示 Hello 处理程序的创建。当请求发送到本地主机：9090 时，将执行此命令。我们还可以发送数据。在 Linux 中，我们可以通过以下命令轻松做到这一点</font>```curl -v localhost:9090 -d "World"```

// Hello handler
type Hello struct {
 l *log.Logger
}// NewHello Function which gives reference to Hello handler
func NewHello(l *log.Logger) *Hello {
 return &Hello{l}
}func (h *Hello) ServeHTTP(rw http.ResponseWriter, r *http.Request) {
 h.l.Println("Hello world")
 d, err := ioutil.ReadAll(r.Body)if err != nil {
  http.Error(rw, "Oops", http.StatusBadRequest)
  return
 }
 fmt.Fprintf(rw, "Hello %s\n", d)
}

<font _mstmutation="1" _msthash="28522" _msttexthash="396006130">我们首先定义一个名为 Hello 的结构，其类型为***log。记录器**（指向记录器模块的指针）。</font>

<font _mstmutation="1" _msthash="32526" _msttexthash="2593876155">ServeHTTP 是 Hello 处理程序上的方法，当我们向本地主机：9090 发送请求时，由 http/server 模块执行该方法。该方法当前仅在服务器日志中记录 Hello world。如果随一些数据一起发送**，则 ioutil**会从请求正文和 http 读取**数据。响应**编写器用于将数据打印为响应。</font>

# <font _mstmutation="1" _msthash="34255" _msttexthash="6674577">结论</font>

<font _mstmutation="1" _msthash="28431" _msttexthash="904819539">我们创建了一个非常基本的 http 服务器，可用于以标准化格式进一步创建更多 API。使用 go 通道实现了正常关闭。我们可以期待在博客的下一部分创建 RESTful 服务。</font>

# <font _mstmutation="1" _msthash="27404" _msttexthash="5334199">引用</font>

*   <font _mstmutation="1" _msthash="27625" _msttexthash="18526599">代码库： [https://github.com/nandangrover/go-microservices](https://zshipu.com/t?url=https://github.com/nandangrover/go-microservices)</font>
*   <font _mstmutation="1" _msthash="27651" _msttexthash="46143188">第 1 部分 github 链接： [https://github.com/nandangrover/go-microservices/tree/microservices_basic_1](https://zshipu.com/t?url=https://github.com/nandangrover/go-microservices/tree/microservices_basic_1)</font>
*   <font _mstmutation="1" _msthash="32136" _msttexthash="68295487">Golang的自由代码营地教程： [https://www.youtube.com/watch?v=YS4e4q9oBaU&ab_channel=freeCodeCamp.org](https://zshipu.com/t?url=https://www.youtube.com/watch?v=YS4e4q9oBaU&ab_channel=freeCodeCamp.org)</font>
*   <font _mstmutation="1" _msthash="27924" _msttexthash="42324373">Golang的服务器文档： [https://golang.org/src/net/http/server.go](https://zshipu.com/t?url=https://golang.org/src/net/http/server.go)</font>
*   <font _mstmutation="1" _msthash="27794" _msttexthash="19986109">服务器Mux： [https://golang.org/pkg/net/http/#ServeMux](https://zshipu.com/t?url=https://golang.org/pkg/net/http/#ServeMux)</font>

