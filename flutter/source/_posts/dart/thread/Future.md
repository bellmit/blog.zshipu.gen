title: dart future
author: 知识铺
date: 2020-09-13 13:53:36
tags:
---

# Future

对上一节的同步代码进行改进, 使用Future对象将耗时的操作放在了其中传入的函数中

```
Future<String> getNetworkData() {
  return Future<String>(() {
      sleep(Duration(seconds: 3));
      return "network data";
    }
  );
}
```

程序打印: 

```和之前直接打印结果不同，这次我们打印了一个Future实例dart
flutter: main function start
flutter: Instance of 'Future<String>'
flutter: main function end
```

和之前直接打印结果不同，这次我们打印了一个Future实例, 这说明我们将一个耗时的操作隔离了起来，这个操作不会再影响我们的主线程执行了  

问题：我们如何去拿到最终的结果呢？  

有了Future之后，可以通过.then回调获取请求到的结果:  

```
import 'dart:io';

Future<String> getNetworkData() {
  return Future<String>(() {
    sleep(Duration(seconds: 3));
    return "network data";
  });
}

main(List<String> args) {
  print("main function start");
  var future = getNetworkData();
  future.then((value) {
    print("!!! get future result: $value");
  });
  print("hello flutter");
  print("main function end");
}
```

执行结果:  

```
main function start
hello flutter
main function end
// 3s后输出下面文本行:
!!! get future result: network data
```

### Future异常的捕获

```
import 'dart:io';

Future<String> getNetworkData() {
  return Future<String>(() {
    sleep(Duration(seconds: 3));
    throw Exception("网络请求出现错误");
  });
}

main(List<String> args) {
  print("main function start");
  var future = getNetworkData();
  future.then((value) {
    print("!!! get future result: $value");
  }).catchError((error) {
    print("!!! get future error: $error");
  });
  print("hello flutter");
  print("main function end");
}
```

运行打印: 

```
main function start
hello flutter
main function end
!!! get future error: Exception: 网络请求出现错误
```

### Future使用总结

1、创建一个Future（可以是我们创建的，也可以是调用内部API或者第三方API获取到的一个Future，总之你需要获取到一个Future实例，Future通常会对一些异步的操作进行封装）；  
2、通过.then(成功回调函数)的方式来监听Future内部执行完成时获取到的结果；  
3、通过.catchError(失败或异常回调函数)的方式来监听Future内部执行失败或者出现异常时的错误信息

-----------------------------------

### Future的两种状态

Future在执行的整个过程中, 分为两种状态: 
- Uncompleted
  - When you call an asynchronous function, it returns an uncompleted future. That future is waiting for the function's asynchronous operation to finish or to throw an error
- Completed
  - if the asynchronous operation succeeds, the future completes with a value. Otherwise it completes with an error

### Future的链式调用 

可以在then中继续返回值，会在下一个链式的then调用回调函数中拿到返回的结果 

```
import 'dart:io';

Future<String> getNetworkData() {
  return Future<String>(() {
    sleep(Duration(seconds: 3));
    return "net work data";
  });
}

main(List<String> args) {
  print("main function start");
  var future = getNetworkData();
  future.then((value) {
    print(value);
    return "value 2";
  }).then((value) {
    print(value);
    return "value 3";
  }).then((hahaha) {
    print(hahaha);
    return "value4"; // 这里的return没有被catch也没关系
  }).catchError((error) {
    print("!!! get future error: $error");
  });
  print("hello flutter");
  print("main function end");
}
```

程序打印:  

```
main function start
hello flutter
main function end
net work data
value 2
value 3
```

-----------------------------------

### Future.value 

```
import 'dart:io';

main(List<String> args) {
  print("start");
  Future.value("哈哈").then((value) {
    print(value);
  });
  print("end");
}
```

程序打印:  

start
end
哈哈

疑惑：为什么立即执行，但是`哈哈哈`是在最后打印的呢？

- 这是因为Future中的then会作为新的任务会加入到事件队列中（Event Queue），加入之后你肯定需要排队执行了

### Future.error

```
main(List<String> args) {
  print("main function start");

  Future.error(Exception("错误信息")).catchError((error) {
    print(error);
  });

  print("main function end");
}
```

程序打印:  

main function start  
main function end  
Exception: 错误信息

### Future.delayed(时间, 回调函数)

```
main(List<String> args) {
  print("main function start");

  Future.delayed(Duration(seconds: 3), () {
    return "3秒后的信息";
  }).then((value) {
    print(value);
  });

  print("main function end");
}
```
程序打印:  

main function start
main function end
3秒后的信息
















































