---
title: "必知必会！计算机里一些基本又重要的概念"
date: 2020-10-17T00:25:59+08:00
toc: true
images:
tags: 
  - 程序员的自我修养
---

最近在翻阅文章时，看到全成推荐的《程序员的自我修养》，这是一本讲链接、装载与库的计算机图书，看了下目录后觉得挺有意思。

因此决定每读一章就将其读书笔记整理记录下来，分享给大家。

目录：

![image](/posts/images/bf202dccad8c3f8efb3726854b72e850.jpg)

## 不要让 CPU 打盹

在计算机发展早期，CPU 资源十分昂贵。如果一个 CPU 只能运行一个程序，那么当程序在读写磁盘（进行 I/O 操作）时，CPU 就空闲下来了。这在当时简直就是巨大的浪费。

![image](/posts/images/df419c04c95fc7d58cc6f6f34a2fb7fd.jpeg)

CPU 只能和一个程序A “聊天“，其他来再多的程序BCD，都没有任何操作的空间。就像早年的手机，打电话和上网（语音/数据）只能二选一，作为 CPU 的你，并不能多线程操作。

因此机智的人们很快就编写了一些监控程序，希望来解决这个问题。

### 多道程序（Multiprogramming）

多道程序起，操作系统正式具有同时运行多个程序的能力。

其是让 CPU 一次读取多个程序放入内存中。当某个程序暂时无须使用 CPU 时，监控程序就把另外的正在等待 CPU 资源的程序启动，以此使得 CPU 能够充分地利用起来。这种策略的确大大的提高了 CPU 资源的利用率。

#### 真实场景

你在 Windows 上点击鼠标 10 分钟以后系统才有反应，那是多么无奈的事情。因为没有优先级区分，自然一路排下来也就不知道要等到什么时候了，相当于半饿死。

#### 存在的问题

核心问题在于程序之间的调度策略太粗糙。对于多道程序来删，程序之间部分轻重缓急，也就是说不存在优先级的区分。因此如果有些程序急需使用 CPU 来完成一些任务，那么很有可能会很长时间后才有机会被分配到 CPU，才得以继续往下运行。

### 分时系统（Time-Sharing System）

程序运行模式改为协作的模式，在原有的多道程序继续升级改造，即每个程序运行一段时间以后都主动让出 CPU 给其他程序，使得一段时间内每个程序都有机会运行一小段。

#### 真实场景

比如你点击一下鼠标或按下一个键盘按键后，他会相较前者能够更快的得到响应，因为他好歹是存在切换的可能性。

#### 存在问题

这时候的监控程序已经比原有多道程序的模式已经复杂了不少，完整的操作系统雏形已经基本形成，很早期的 Windows（Windows 95 和 Windows NT 之前），MacOS X 之前的 MacOS 版本都是采用这种分时系统的方式来进行程序调度。

其仍然存在问题，核心在于若一个程序一直在进行一个耗时计算，便会一直霸占着 CPU 不放，那么操作系统也没有不放，就会导致其他程序都只能无限等待，相当于就是系统假死了。

### 多任务系统（Multi-tasking）

#### 背景

在分时系统中，一个程序死循环就会导致系统假死，并且其运行效率并不高，只能解决当时的交互式环境。

放在现在来讲，已经完全没法很好的运行。因此当时业界也在研究更为先进的操作系统模式，也就是现在最为流行也是最熟悉的多任务系统。

#### 解决方案

在多任务系统中，所有的应用程序都以进行（Process）的方式运行，其有以下特点：

- 每个进程都有自己独立的地址空间，因此各进程之间相互隔离。
- 每个 CPU 都由操作系统统一进行分配。
- 每个进程根据其优先级的高低都有机会得到 CPU。

但需要注意的是，若是进程运行超出了指定的时间，操作系统就会暂停该进程，将 CPU 资源分配给其他等待运行的进程。这种 CPU 的分配方式一般称作抢占式（Preemptive）。

通过这种方式，操作系统就可以强制剥夺 CPU 资源并且分配给它认为目前最需要资源的进程，如果分配给每个进程的时间都很短，即 CPU 在多个进程间快速切换，就可以造成多个进程同时在运行的假象。

## 内存不够用怎么办

在早期的计算机中，程序是直接运行在物理内存上的，访问的内存地址都是物理地址。假设只是一个进程在跑，可能内存资源还够用，但实际上为了更有效地利用硬件资源，我们必须运行多个程序，CPU 的利用率才会比较高。这时候就会遇到一个严重的问题，那就是如何将计算机上有限的物理内存分配给多个程序使用？

![image](/posts/images/e029f8694bf3d0f79b9fe3e30451f141.jpg)

就像上图，每个程序他都想申请 1GB 的内容，而计算机本身只有 1GB 的物理内存，根本没有办法真正的执行。

### 真实场景和问题

可能会有小伙伴想，知识铺你举的例子太极端了，我们举个 ”正常“ 点的例子。假设计算机有 128MB 内存，程序 A 运行需要 10MB，程序 B 需要 100MB，程序 C 需要 20 MB。假设该几个程序运行时，我们按照其想要的一分配，不就好了吗？

但现实并不是这样，这种简单的内存分配策略存在许多的问题：

- 地址空间不隔离：所有程序都直接访问物理地址，各程序所使用的内存空间并不是相互独立，很容易改写到其他程序的内存地址。

- 内存使用效率低：没有有效的内存管理机制，一会运行程序 A，一会运行程序 B，就需要经常要将大量数据换出换入，效率十分低下。

- 程序运行的地址不确定：每次程序运行时，都需要从内存中给其分配一块足够大的空闲区域，但这些内存区域位置是不确定的，给程序编写造成了一定的麻烦。

### 解决方法

解决上述问题的解决思路，就是万能的法宝：增加中间层，即使用一种间接的地址访问方法。把程序给出的地址看作是一种虚拟地址（Virtual Address），然后通过某些映射的方法，将这个虚拟地址最终转换成实际的物理地址。

上述提到了两个非常重要的内存概念：

- 物理地址空间：是实实在在存在的，存在于计算机中，且对每一台计算机来说只有唯一的一个，你可以将其想象为物理内存。

- 虚拟地址空间：是指虚拟的、人们想象出来的地址空间。其实它并不存在，每个进程都有自己的独立虚拟空间，且每个进程只能访问自己的地址空间。

如此一来，操作系统只需要控制虚拟地址到物理地址的映射过程，就可以保证任意一个程序锁你访问的物理内存区域和另外一个程序不重叠，以达到地址空间隔离的效果。

![进程虚拟空间、物理空间和磁盘之间的页映射关系](/posts/images/fb70d293e18832881e96330c2388614f.jpg)

另外需要清楚虚拟存储的实现需要依靠硬件的支持，对于不同的 CPU 来说不同。但大多采用 MMU（Memory Management Unit）的部件来进行页映射：

![虚拟地址到物理地址的转变](/posts/images/d1be0cd17fc6b36c54c9d33c95baae92.jpg)

CPU 发出的是虚拟地址（Virtual Address），也就是日常程序中所看到的是虚拟地址。经过 MMU 转换后就会变成物理地址（Physical Address）。

目前常见的 MMU 均已集成在 CPU 内部了，不会再以独立部件存在。

## 线程的那些事

线程（Thread），有时候被称为轻量级进程，是程序执行流程的最小单元。一个标准的线程由线程 ID、当前指令指针（PC）、寄存器集合和堆栈组成。

通常一个进程由一个到多个线程组成，各个线程之间共享程序的内存空间（包括代码段、数据段、堆等）及一些进程级的资源（如打开文件和信号）。

![image](/posts/images/1b00bbf5766fd7fb6f2c3fa68bdf7b38.jpg)

### 为什么需要多线程

- 某个操作可能会陷入长时间等待，等待的线程会进入睡眠状态，无法继续执行。多线程执行可以有效利用等待的时间。典型的例子是等待网络响应，这时候就可以切换了。

- 某个操作会消耗大量的时间，如果只有一个线程，程序和用户之间的交互会中断。多线程的情况下，可以让一个线程负责交互，另外一个线程负责计算。

- 程序逻辑本身就要求并发操作，例如一个多端下载软件。

- 多 CPU 或多核计算机，其本身就具备同时执行多个线程的能力。

- 相对于多进程应用，多线程在数据共享方面效率会高很多。

### 线程的访问权限

线程可以访问进程内存里的所有数据，甚至在知道堆栈地址的情况下，可以访问其他线程里的堆栈信息。其私有存储空间主要分为：栈、线程局部存储（Thread Local Storage，TLS）、寄存器（包括 PC 寄存器）。

### 线程调度和时间片

在单处理器对应多线程的情况下，并发是一种模拟处理的状态。操作系统会让这些多线程程序轮流执行，每次仅执行一小段时间（通常是几十到几百毫秒），这样子线程就 “看起来” 在同时执行。

不断在处理器上切换不同的线程行为称之为线程调度（Thread Schedule），通常拥有至少三种状态，分别是：

- 运行（Running）：此时线程正在执行。

- 就绪（Ready）：此时线程可以立刻运行，但 CPU 已经被占用，暂时无法分配。

- 等待（Waiting）：此时线程正在等待某一事件（例如：I/O 事件）发生，无法执行。

处于运行状态中的线程都会拥有一段可以执行的时间，这段时间段称为时间片（Time Slice）。其基本流转：

- 当时间片用尽的时候，进程进入就绪状态。

- 当时间片用尽之前，进程若开始等待某个事件，那么它将进入等待状态。

每当一个线程离开运行状态时，调度系统就会选择一个当前是就绪状态的线程继续执行。而一个处于等待状态的线程在完成所等待的事件后，就会进入就绪状态。

![image](/posts/images/b7cec2f55d30a4ed9d46f2d0e50387a7.jpg)

### 线程优先级

在 Windows 和 Linux 中，线程的优先级可以通过用户手动设置，系统也会根据线程的表现自动调整优先级，以使得调度更有效率。常见的一般有两类线程：

- IO 密集型线程（IO Bound Thread）：频繁等待，像是网络调用。

- CPU 密集型线程（CPU Bound Thread）：很少等待，主要是计算为主。

常见的线程调度方式如下：

- 轮转法：让各个线程轮流执行一小段时间，这也决定了线程之间存在交错执行的特点。

- 优先级调度：在具有优先级调度的系统中，线程都拥有各自的线程优先级，具有高优先级的线程会更早的执行，低优先级的线程常常要等待到系统中已经没有高优先级的可执行线程时才可以执行。

IO 密集型线程总是会比 CPU 密集型线程容易得到优先级的提升。但在优先级调度下，存在一种线程饿死的现象。一个线程被饿死，是说它的优先级比较低，在它执行之前，总是有较高优先级的线程要执行。因此低优先级线程始终无法执行。

为了避免饿死现象，调度系统会逐步提升那些等待了过长时间的得不到执行的线程优先级。这样的方式，一个线程只要等待足够长的时间，其优先级最终一定会提高到足够让他执行的程度。线程优先级改变一般有三种方式：

- 用户指定优先级。

- 根据进入等待状态的频繁程度提升或降低优先级。

- 长时间得不到执行而被提升优先级。

### 可抢占线程和不可抢占线程

线程在用尽时间片之后会被强制剥夺继续执行的权利，而进入就绪状态，这个过程叫做抢占（Preemption），即之后执行的别的线程抢占了当前线程。

目前以可抢占式线程居多，非抢占式线程在今日已经十分少见。

### 三种线程模型

日常在程序中使用的线程其实并不是内核线程，而是存在于用户态的用户线程。用户态并不一定在操作系统内核中对应同等数量的内核线程。接下来将介绍三种常见的用户态多线程库的实现方式。

#### 一对一模型

一对一模型指的是一个用户使用的线程就唯一对应一个内核使用的线程。

![一对一线程模型](/posts/images/af87eb0e79d373560bdbf4e7ed8ca630.jpg)

优点：

- 线程之间的并发是真正的并发。

- 线程阻塞时，其他线程执行不会受到影响。

缺点：

- 操作系统限制了内核线程的数量，因此一对一线程会让用户的线程数受限。

- 内核线程调度时，上下文切换的开销较大，导致用户线程的执行效率下降。

#### 多对一模型

多对一模型指的是多个用户线程映射到一个内核线程上，线程之间的切换由用户态的代码来进行。

![多对一模型](/posts/images/daf4659747a2f7edcc317493ec7ebf96.jpg)

优点：

- 线程切换相对于一对一模型来说高效许多。

缺点：

- 如果一个用户线程阻塞，那么所有的线程豆浆无法执行，因为内核线程也被阻塞住了。


#### 多对多模型

多对多模型指的是将多个用户线程映射到少数但不止一个内核线程上。

![多对多模型](/posts/images/25cdc9b99b8543ca33a6494b88e2d482.jpg)

优点：

- 一个用户线程阻塞，并不会导致其它用户线程也阻塞。

缺点：

- 性能提升不如一对一模型高。

## 总结

本文主要涉及到 CPU、内存、线程。我们能够从其的一些关注点知道为什么 CPU 调度会这样子发展，又经历了什么东西。内存为什么会出现虚拟内存，物理内存，其之间又是如何相互转换的。

另外还了解到线程的基本分类和常见调度方式等，这些都是计算机基本的软硬件知识，非常值得大家仔细思考。
