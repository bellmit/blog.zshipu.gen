
title: Flutter 是什么
author: 知识铺
date: 2020-09-13 21:23:04
tags: 
---
  首先 Flutter 是什么？响应式的跨平台 UI 框架，这点和 vue 或者 weex 很像，所以在开发思路上并不会有什么阻碍。

> 那么上手 Flutter 需要做什么？

## 1、Dart 语言

首先就是 Dart 语言，Dart 语言对于有 JS 基础而言很容易上手，**因为可辨识度本高！因为 Dart 起初都是为了Web 而生，所以 Dart 和 JS 在一定程度上有很大的通识性**。

举个例子：如下代码所示， 它们都支持通过 ```var```定义变量，支持 ```async/await``` 语法糖，支持 ```Promise(Future)``` 等链式异步处理，甚至 ```*/yield``` 的语法糖都类似(虽然这个对比不大准确)，但可以看出它们确实存在_“近亲关系”_ 。

 <code class="language-text">/// JS

    var a = 1

    async function doSomeThing() {
        var result = await xxxx()
        doAsync().then((res) => {
            console.log("ffff")
        })
    }
    function* _loadUserInfo () {
        console.log("**********************");
        yield put(UpdateUserAction(res.data));
    }

/// Dart

  var a = 1;

  void doSomeThing() async {
    var result = await xxxx();
    doAsync().then((res) {
      print('ffff');
    });
  }
  _loadUserInfo() async* {
    print("**********************");
    yield UpdateUserAction(res.data);
  }</code>

但是它们之间的差异性也很多，而最大的区别就是： **JS 是动态语言，而 Dart 是伪动态语言的强类型语言。**

如下代码中，在 Dart 中可以直接声明 ```name``` 为 ```String``` 类型，同时 ```otherName``` 虽然是通过 ```var```语法糖声明，但在赋值时其实会通过自推导出类型 ，而 ```dynamic``` 声明的才是真的动态变量，在运行时才检测类型。

 <code class="language-text">// Dart
String name = 'dart'; 
var otherName = 'Dart';
dynamic dynamicName = 'dynamic Dart';</code>

如下图代码最能体现这个差异，在下图例子中：

*   var i 在全局中未声明类型时，会被指定为 dymanic ，从而导致在 init() 方法中编译时不会判断类型，这和 JS 内的现象会一致。

*   如果将 var i = ""; 定义在 init() 方法内，这时候 i 已经是强类型 String了 ，所以编译器会在 i++报错，但是这个写法在 JS 动态语言里，默认编译时是不会报错的。

所以 Dart 和 JS 之间存在例如：**动态和非动态的差异、结尾需要加分号、强类型、伪动态等等的差异，但是很大程度上可辨识度很高**。

> **Dart 的学习保守估计两天内可以解决。**

## 2、Flutter UI

在界面开发上 Flutter 可能就不是很讨 Web 开发的喜欢，首先 Flutter 中没有 ```css``` 的概念，但是有 ```Theme``` 、```TextStyle```、```xxxStyle``` 的概念，基本上都是按照类对象来封装，然后可以通过 ```InheritedWidget``` 来实现全局共享。

**在 Flutter 中使用 Dart 支持函数式编程和面向对象编程，所以这个对于 Web 开发者来说也不陌生**。

Flutter 最大的特点在于： **在 Flutter 宇宙中万物皆 Widget，且 Widget 是不可变的。** 这个概念实现可能需要自己慢慢领悟，```Widget > Element > RenderObject > Layer``` 流程上的实现原理，理解了这些基本上就理解了 Flutter UI 的核心实现。

当然，上手开发可以先不理解这个，举个例子：如下图所示，Flutter 开发中一般是通过继承 **无状态 ```StatelessWidget```控件** 或者 **有状态 ```StatefulWidget``` 控件** 来实现页面，然后在对应的 ```Widget build(BuildContext context)```方法内实现布局，利用不同 ```Widget``` 的 ```child / children``` 去做嵌套，通过控件的构造方法传递参数，最后对布局里的每个控件设置样式等。

就是这样，通过继承 ```StatelessWidget``` 或 ```StatefulWidget``` 作为容器，然后在 ```build``` 方法返回布局，Flutter 内的 ```Widget``` 的颗粒度控制得很细 ，如 ```Padding``` 、```Center``` 都会是一个单独的 ```Widget```，甚至状态共享都是通过 ```InheritedWidget```共享 ```Widget```去实现的。

> **对比起 Weex ，就像是在封装各种组件 ```Template``` ，当然写法和嵌套还有封装文件需要你重新理解，保守估计可能一个星期可以上手。**

## 3、状态管理

Flutter 中出了官方提供的 ```provider``` 和 ```scoped_model``` 之外，类似 ```flutter_redux``` 相信前端开发布会陌生，事实上 Web 上所有的状态管理模型都可以往 Flutter 上迁移，这其中可能需要理解 Stream 、Future、Zone 相关的实现概念。

*   [Flutter完整开发实战详解(十五、全面理解State与Provider)](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//juejin.im/post/5d0634c7f265da1b91639232)

*   [Flutter完整开发实战详解(十二、全面深入理解状态管理设计)](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//juejin.im/post/5cc816866fb9a03231209c7c)

*   [Flutter完整开发实战详解(十一、全面深入理解Stream)](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//juejin.im/post/5cc2acf86fb9a0321f042041)

> **保守估计一周可以熟悉完整个状态管理逻辑。**

## 4、开发工具和打包

最后对于 Web 开发者而言，可能开发工具和打包就是最后一道门槛，如果是使用 ```WebStorm``` 用户推荐使用 ```Android Studio``` ，如果是使用 ```VSCode``` 用户可以继续使用 ```VSCode``` 。

关于打包相关的可以看： [Flutter完整开发实战详解(十九、 Android 和 iOS 打包提交审核指南)](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//juejin.im/post/5e1596eae51d4540dd6c0275)

> **保守估计三天可以熟悉完整个状态管理逻辑。** > 作者：恋猫
