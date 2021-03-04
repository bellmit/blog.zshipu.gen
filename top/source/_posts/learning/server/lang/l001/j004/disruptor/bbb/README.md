#   Disruptor

Disruptor 是一款高性能的有界内存队列，线程间通信高效低延时的内存消息组件。

##  背景

-   应用领域

队列，异步消息处理

-   Java 实现

数据结构有各种实现版本，Java 还提供了线程安全版和线程不安全版。

-   并发需求

需要能够每秒应对百万请求。

LMAX是一种新的零售的金融交易平台。它的业务创新 – 允许任何人在一系列的金融衍生产品交易。这就需要非常低的延迟，非常快速的处理，因为市场变化很快，这个零售平台因为有很多人同时操作自然具备了复杂性，用户越多，交易量越大，不断快速增长。

能够在一个线程里每秒处理6百万订单，业务逻辑处理器完全是运行在内存中，使用事件源驱动方式。

----

##  主要问题

Java 实现的队列较为通用，适合普遍场景。

Java 同步并发队列容器，使用锁，性能较低。

Java 并发队列容器大量是无界，容易 OOM

ArrayBlockingQueue 和 LinkedBlockingQueue 是有界队列，也是阻塞的，高并发场景下，锁的效率不高

----

##  解决方案

两个方面：利用无锁算法避免锁的争用、将硬件(CPU)的性能发挥到极致

-   内存分配更加合理，使用 RingBuffer 数据结构，数组元素在初始化时一次性全部创建，提升缓存命中率；对象循环利用，避免频繁 GC
-   能够避免伪共享，提升缓存利用率
-   采用无锁算法，避免频繁加锁、解锁的性能消耗
-   支持批量消费，消费者可以无锁方式消费多个消息

----


##  设计实现

----


##  应用模式


----

##  典型案例

-   Log4j2
-   Spring Messaging
-   HBase
-   Storm

----
