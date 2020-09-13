title: dart 多核CPU利用
author: 知识铺
date: 2020-09-13 13:53:36
tags:
---

# 多核CPU利用

[https://juejin.im/post/5d7f5e7c6fb9a06b0c089920#heading-16](https://juejin.im/post/5d7f5e7c6fb9a06b0c089920#heading-16)  

#### Isolate的理解

在Dart中，有一个Isolate的概念，它是什么呢？

- 我们已经知道Dart是单线程的，这个线程有自己可以访问的内存空间以及需要运行的事件循环；
- 我们可以将这个空间系统称之为是一个Isolate；
- 比如Flutter中就有一个Root Isolate，负责运行Flutter的代码，比如UI渲染、用户交互等等；

在 Isolate 中，资源隔离做得非常好，每个 Isolate 都有自己的 Event Loop 与 Queue，

- Isolate 之间不共享任何资源，只能依靠消息机制通信，因此也就没有资源抢占问题。

但是，如果只有一个Isolate，那么意味着我们只能永远利用一个线程，这对于多核CPU来说，是一种资源的浪费。

如果在开发中，我们有非常多耗时的计算，完全可以自己创建Isolate，在独立的Isolate中完成想要的计算操作。

**创建Isolate**

```
import "dart:isolate";

main(List<String> args) {
  Isolate.spawn(foo, "Hello Isolate");
}

void foo(info) {
  print("新的isolate：$info");
}
```

#### Isolate通信机制

但是在真实开发中，我们不会只是简单的开启一个新的Isolate，而不关心它的运行结果：

- 我们需要新的Isolate进行计算，并且将计算结果告知Main Isolate（也就是默认开启的Isolate）；
- Isolate 通过发送管道（SendPort）实现消息通信机制；
- 我们可以在启动并发Isolate时将Main Isolate的发送管道作为参数传递给它；
- 并发在执行完毕时，可以利用这个管道给Main Isolate发送消息

```
import 'dart:isolate';

main(List<String> args) async {
  ReceivePort receivePort = ReceivePort();
  // Isolate isolate = Isolate.spawn(entryPoint, message)
  Isolate isolate = await Isolate.spawn<SendPort>(foo, receivePort.sendPort);
  receivePort.listen((data) {
    print('Data：$data');
    // 不再使用时，我们会关闭管道
    receivePort.close();
    // 需要将isolate杀死
    isolate?.kill(priority: Isolate.immediate);
  });
}

void foo(SendPort sendPort) {
  sendPort.send("Hello world!");
}
```

### compute

Flutter提供了支持并发计算的`compute`函数，它内部封装了Isolate的创建和双向通信

```
main(List<String> args) async {
  int result = await compute(powerNum, 5);
  print(result);
}

int powerNum(int num) {
  return num * num;
}
```


