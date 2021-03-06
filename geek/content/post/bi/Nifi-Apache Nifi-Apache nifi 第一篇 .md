---
title: Nifi-Apache Nifi-Apache nifi 第一篇 
date: 2021-10-30 13:01:00
tags: [nifi]
---



## 1、什么是 Apache NiFi？



　　简单地说，NiFi 是为了自动化系统之间的数据流。虽然*数据流这种形式很容易理解*，但我们在此使用它来表示系统之间的自动化和不同系统之间数据的流转。企业拥有多个系统，其中一些系统创建了数据，部分系统消耗了数据，那么问题就出现了。出现的问题和解决方案已经广泛讨论和阐述。*nifi 就是一个致力于数据对接的集成框架*。

**数据流面临的一些比较高级的挑战包括：**

1、系统故障

　　网络故障、硬盘故障、软件宕机、人员操作失误。

2、数据接入超出处理能力

　　有时候一个数据源的输出可能超出，系统所能处理的能力。此外，有可能传递链出现问题，比如某一个弱连接处出现问题。

- 3、很少对边界做出界定
- 　　你可能经常遇到数据量太大、太小、太快、太慢、损坏、错误、格式不对等问题。
- 4、系统的调整
- 　　系统地某一部分经常需要改动，需要快速的使用一个新的数据流，或者调整现有的一个流。
- 5、系统以不同的速度发展
- 　　给定系统使用的协议和格式可以随时改变，而不管其周围的系统如何。数据流存在的连接本质上是大量分散的组件系统，这些组件松散地或者不是全部设计在一起工作。
- 6、合规性和安全性
- 　　法律法规和政策变化。企业对企业协议的变化。系统对系统和系统与用户的交互必须是安全，可靠，负责任的。
- 7、生产中持续改善
- 　　实验室通常不可能接近复制生产环境。
- 
- 　　多年以来，数据流已经成为一种架构中必不可少的恶性循环之一。现在虽然有一些积极和快速发展的运动，使得数据流更有趣，对于给定企业的成功更为重要。这些包括像 面向服务的架构 [SOA ](http://nifi.apache.org/docs/nifi-docs/html/overview.html#soa)，API 的兴起，物联网 [IOT ](http://nifi.apache.org/docs/nifi-docs/html/overview.html#iot)，和大数据 [bigdata ](http://nifi.apache.org/docs/nifi-docs/html/overview.html#bigdata)。此外，合规性，隐私性和安全性所需的严谨程度不断增加。即使仍然存在所有这些新概念，数据流的模式和需求仍然基本相同。主要的差异在于复杂性的范围，适应需要的变化率，并且在规模上，边缘情况变得普遍存在。NiFi 旨在帮助解决这些现代数据流挑战。
- 
- 

##  

##  

## 2、NiFi 核心概念

Nifi 的设计理念接近于基于流的编程 Flow Based Programming [[fbp\]](http://nifi.apache.org/docs/nifi-docs/html/overview.html#fbp). 下面是 nifi 的一些核心概念，还有他和 FBP 的对于关系:

| NiFi Term          | FBP Term           | Description                                                  |
| ------------------ | ------------------ | ------------------------------------------------------------ |
| FlowFile           | Information Packet | A FlowFile represents each object moving through the system and for each one, NiFi keeps track of a map of key/value pair attribute strings and its associated content of zero or more bytes. |
| FlowFile Processor | Black Box          | Processors actually perform the work. In [[eip\]](http://nifi.apache.org/docs/nifi-docs/html/overview.html#eip) terms a processor is doing some combination of data routing, transformation, or mediation between systems. Processors have access to attributes of a given FlowFile and its content stream. Processors can operate on zero or more FlowFiles in a given unit of work and either commit that work or rollback. |
| Connection         | Bounded Buffer     | Connections provide the actual linkage between processors. These act as queues and allow various processes to interact at differing rates. These queues can be prioritized dynamically and can have upper bounds on load, which enable back pressure. |
| Flow Controller    | Scheduler          | The Flow Controller maintains the knowledge of how processes connect and manages the threads and allocations thereof which all processes use. The Flow Controller acts as the broker facilitating the exchange of FlowFiles between processors. |
| Process Group      | subnet             | A Process Group is a specific set of processes and their connections, which can receive data via input ports and send data out via output ports. In this manner, process groups allow creation of entirely new components simply by composition of other components. |

设计模型, 和 [seda](http://nifi.apache.org/docs/nifi-docs/html/overview.html#seda) 也很相似, 提供了许多优点，可以帮助 NiFi 成为构建强大而可扩展的数据流的非常有效的平台。其中一些好处包括：

- 适用于视觉创建和管理处理器的有向图
- 本质上是异步的，即使在处理和流量波动时也允许非常高的吞吐量和自然缓冲
- 提供高度并发的模型，而开发人员不必担心并发性的典型复杂性
- 促进发展粘性和松散耦合的部件，然后可以在其他情况下重复使用，并促进可测试的部件
- 资源受限的连接使关键功能（如背压和压力释放）非常自然和直观
- 错误处理变得与基本逻辑一样自然，而不是粗粒度的一网打尽
- 数据进出系统的点以及流程如何被很好的理解和易于跟踪

##  

## 3、NiFi 架构

![img](http://nifi.apache.org/docs/nifi-docs/html/images/zero-master-node.png)

NiFi 在主机操作系统上的 JVM 内执行。JVM 上的 NiFi 的主要组件如下：

- 网络服务器

  Web 服务器的目的是托管 NiFi 的基于 HTTP 的命令和控制 API。

- 流控制器

  流控制器是操作的大脑。它提供用于扩展程序运行的线程，并管理扩展程序接收资源以执行的时间表。

- 扩展

  有各种类型的 NiFi 扩展在其他文档中描述。这里的关键是扩展在 JVM 中运行和执行。

- FlowFile 存储库

  FlowFile 存储库是 NiFi 跟踪目前在流程中活动的给定 FlowFile 的知识状态。存储库的实现是可插拔的。默认方法是位于指定磁盘分区上的持久写入前端日志。

- 内容存储库

  Content Repository 是给定 FlowFile 的实际内容字节。存储库的实现是可插拔的。默认方法是一个相当简单的机制，它将数据块存储在文件系统中。可以指定多个文件系统存储位置，以便获得不同的物理分区，以减少任何单个卷上的争用。

- 源头存储库

  Provenance Repository 是存储所有来源的事件数据的地方。存储库构造是可插入的，默认实现是使用一个或多个物理磁盘卷。在每个位置内，事件数据被索引和可搜索。

NiFi 还能够在集群内运行。

![img](http://nifi.apache.org/docs/nifi-docs/html/images/zero-master-cluster.png)

从 NiFi 1.0 版本开始，采用零主分类范例。NiFi 集群中的每个节点对数据执行相同的任务，但是每个节点都在不同的数据集上进行操作。Apache ZooKeeper 选择单个节点作为群集协调器，故障转移由 ZooKeeper 自动处理。所有群集节点向群集协调器报告心跳和状态信息。集群协调器负责断开连接节点。此外，每个群集都有一个主节点，也由 ZooKeeper 选择。作为 DataFlow 管理器，您可以通过任何节点的用户界面（UI）与 NiFi 集群进行交互。您所做的任何更改都会复制到群集中的所有节点，从而允许多个入口点。

##  

## 4、NiFi 的性能期望和特点

　　NiFi 旨在充分利用其正在运行的底层主机系统的功能。对于 CPU 和磁盘，资源最大化特别强。有关其他详细信息。

- 　　对于 IO

  可以看到的吞吐量或延迟可能会有很大的不同，这取决于系统的配置方式。考虑到大多数主要的 NiFi 子系统都有可插拔的方法，性能取决于实现。但是，对于具体和广泛适用的内容，请考虑开箱即用的默认实现。这些都是持续的保证交付，并使用本地磁盘。因此，保守的，假设典型服务器中适度的磁盘或 RAID 卷上的读 / 写速率大约为每秒 50 MB。对于大量数据流，NiFi 应该能够有效地达到每秒 100 MB 或更多的吞吐量。那是因为每个物理分区和内容存储库都预期添加到 NiFi 的线性增长。这将在 FlowFile 存储库和来源存储库的某个时间点出现瓶颈。我们计划提供一个基准测试和性能测试模板，以包含在构建中，从而允许用户轻松测试他们的系统，并确定瓶颈在哪里，以及哪些可能成为一个因素。此模板还可使系统管理员轻松进行更改并验证其影响。

- 　　对于 CPU

  流控制器用作引擎，指定特定处理器何时被执行线程。写处理器一经执行任务就会立即返回线程。流控制器可以给出一个配置值，指示其维护的各种线程池的可用线程。使用的理想线程数取决于主机系统资源的核心数量，无论该系统是否运行其他服务，以及流程中的处理特性。对于典型的 IO 大流量，可以使数十条线程可用。

- 　　对于 RAM

  NiFi 存在于 JVM 中，因此限于由 JVM 提供的内存空间。JVM 垃圾收集成为限制实际堆大小的一个非常重要的因素，同时优化应用程序运行时间。当定期阅读相同的内容时，NiFi 工作可能是 I / O 密集型的。配置足够大的磁盘以优化性能。

##  

##  

## 5、关键 NiFi 功能的高级概述

- 流量管理

  保证交货NiFi 的核心理念是，即使在非常高的规模，保证交付是必须的。这是通过有效使用专用的持久预写日志和内容存储库来实现的。它们一起设计成允许非常高的事务速率，有效的负载传播，写时复制以及发挥传统磁盘读 / 写功能的优势。数据缓冲带背压和压力释放NiFi 支持对所有排队的数据进行缓冲，以及当队列达到指定限制时提供背压的能力，或者在数据达到指定年龄时使其老化（其值已经消失）的能力。优先排队NiFi 允许设置一个或多个优先级排序方案来了解如何从队列中检索数据。默认值是最早的，但有时候数据应该被拉到最新，最大的第一个或其他一些自定义方案。流特定 QoS（延迟 v 吞吐量，丢失容限等）数据流的一些点数据绝对关键，并且是不容忍的。还有一段时间，它必须在几秒钟内被处理和交付成为任何价值。NiFi 使得细粒度流特定配置这些问题。

- 使用方便

  视觉指挥与控制数据流可能变得相当复杂。能够可视化这些流程并在视觉上表达它们可以大大减少复杂性并确定需要简化的领域。NiFi 不仅可以直观地建立数据流，而且可以实时地实现。而不是*设计和部署*它更像是成型粘土。如果对更改的数据流进行更改立即生效。更改是细粒度的，并且与受影响的组件隔离。您不需要停止整个流程或流程只是为了进行一些具体的修改。流模板数据流往往是高度模式化的，而通常有许多不同的方式来解决问题，它可以大大地分享这些最佳实践。模板允许主题专家构建和发布他们的流程设计，并为其他人创造和合作。资料来源NiFi 自动记录，索引并提供可用的来源数据，因为对象即使在扇入，扇出，转换等过程中也可以流经系统。该信息在支持合规性，故障排除，优化和其他场景方面变得非常重要。恢复 / 记录细粒历史的滚动缓冲区NiFi 的内容存储库旨在作为历史的滚动缓冲区。只有当数据从内容存储库中老化或者需要空间时才会被删除。这与数据来源功能相结合，使得在对象的生命周期中甚至跨越世代的特定点上实现点击内容，内容下载和重放非常有用的基础。

- 安全

  系统到系统数据流只是安全的一样好。数据流中每一点的 NiFi 都可以通过使用诸如双向 SSL 等加密协议提供安全交换。此外，NiFi 使得流可以加密和解密内容，并使用发件人 / 收件人方程的任一侧上的共享密钥或其他机制。用户到系统NiFi 支持双向 SSL 身份验证，并提供可插拔授权，从而可以正确控制用户的访问和特定级别（只读，数据流管理器，管理员）。如果用户在流程中输入密码等敏感属性，则立即加密服务器端，即使在加密形式下也不会再次暴露在客户端。多租户授权给定数据流的权限级别适用于每个组件，允许管理员用户具有细粒度的访问控制。这意味着每个 NiFi 集群都能够处理一个或多个组织的要求。与独立拓扑相比，多租户授权可实现数据流管理的自助服务模式，从而允许每个团队或组织对流程进行管理，同时充分了解流程的其他部分，无法访问。

- 可扩展架构

  延期NiFi 的核心是扩展的核心，因此它是数据流处理可以以可预测和可重复的方式执行和交互的平台。扩展点包括：处理器，控制器服务，报告任务，优先级和客户用户界面。分类器隔离对于任何基于组件的系统，可能会迅速发生依赖问题。NiFi 通过提供自定义类加载器模型来解决这个问题，确保每个扩展捆绑包都暴露在非常有限的依赖关系中。因此，可以构建扩展，而不用担心它们是否可能与另一个扩展冲突。这些扩展束的概念称为 *NiFi Archives，*并在开发人员指南中有更详细的讨论。站点到站点通信协议NiFi 实例之间的首选通信协议是 NiFi 站点到站点（S2S）协议。S2S 可以方便，高效，安全地将数据从一个 NiFi 实例传输到另一个。NiFi 客户端库可以轻松构建并捆绑到其他应用程序或设备中，以通过 S2S 与 NiFi 通信。S2S 中都支持基于套接字的协议和 HTTP（S）协议作为底层传输协议，从而可以将代理服务器嵌入到 S2S 通信中。

- 灵活的缩放模型

  横向扩展（聚类）NiFi 旨在通过如上所述将多个节点聚类在一起使用来展开。如果单个节点被配置并配置为每秒处理数百 MB，则可以配置适度的集群来处理每秒的 GB 数。这将带来 NiFi 与获取数据的系统之间的负载平衡和故障转移的有趣挑战。使用基于异步排队的协议（如消息传递服务，Kafka 等）可以帮助您。使用 NiFi 的*站点到站点*功能也非常有效，因为它是允许 NiFi 和客户端（包括另一个 NiFi 集群）相互通话，共享关于加载的信息以及在特定授权端口上交换数据的协议。放大和缩小NiFi 也被设计成以非常灵活的方式进行放大和缩小。在从 NiFi 框架的角度增加吞吐量方面，可以在配置时增加 “计划” 选项卡下的处理器上的并发任务数量。这允许更多的进程同时执行，提供更大的吞吐量。另一方面，您可以将 NiFi 完美地缩放到适合于在硬件资源有限的边缘设备上运行，因为需要较小的占用空间。为了专门解决第一个英里数据收集挑战和边缘用例。完事了，可以开始尝试一把了。