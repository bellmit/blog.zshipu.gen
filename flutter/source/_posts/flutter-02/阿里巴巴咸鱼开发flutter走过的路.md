
title: 阿里巴巴咸鱼开发flutter走过的路
author: 知识铺
date: 2020-09-13 21:18:44
tags: 
---
  闲鱼是第一个使用Flutter混合开发的大型应用，但闲鱼客户端开发最深入体会的痛点就是编译时长影响开发体验。

在Flutter+Native这种开发模式下，Native编译速度慢，模块开发无法突破。闲鱼集成了集团众多中间件，很多功能无法通过flutter直接调用，需使用各种channel到native去调用对应功能。

总而言之，闲鱼目前Flutter开发面临如下几个痛点：

*   Flutter侧混合编译速度慢，Android首次编译**10min+**，iOS首次编译**20min+**；
*   混合栈编程中历史包袱导致IOS/Android双端返回给Flutter侧的数据可能存在**不一致性**；
*   集成模块**开发效率相比模块开发较低**，单模块页面测试性能数据无法展开；

下面我们详细来分享一下阿里巴巴淘系技术闲鱼客户端的Flutter开发经验和遇到的问题。

——————————————————————————————————————————

## **方案一：模块化开发方案概述**

此项目从立项至今已经很长一段时间，由于业务迭代快，native插件满天飞情况下，想要做到工程模块化拆分难度可想而知；如下图是项目立项为模块化拆分，业务方需要将各个业务拆分解耦合，拆分集团中间件，业务封装组件，Native业务代码，Flutter桥代码，Flutter组件库，Flutter侧业务代码等多个模块；项目初衷就是整理代码，提供一个Flutter可运行的干净环境，同时需要让flutter可以获取到native几乎所有能力，但是编译开发调试时候有想要速度快，效率高。能想到的最直接解决方案就是拆包，从0-1建立一个最小壳工程，然后拆分集团基本中间件，封装业务组件，Flutter插件等，如下是整个项目架构：

日常模块化单页面级需要使用最小壳工程，其内部有channel的声明和实现，通过运行最小壳工程运行得到结果，Flutter侧模块开发通过IOC调用到最小壳工程的channel得到返回结果，最后将模块化开发以一种pub或者git依赖方式集成到闲鱼FWN主工程即可；

## **阶段性效果**

业务模块化拆分从来都是一种吃力不讨好的活，明知道拆出来有收益，但是投入产出比不足，因此历史包袱代码越来越厚重，以至于下一个接收的人都不敢轻易修改代码；在模块化拆分时候，开始项目时候提出过新起一个干净的工程，然后一步步拆分集团中间件，期间拆出了Mtop/Login/FlutterBoost/UI Plugin，耗时3周/2人，得到部分结果就是新业务，新界面开发满足基本快速迭代开发，缺点也很明显如下所示：

*   拆分梳理Native的中间件繁琐，工作量巨大，最小化壳工程**耗时3周/2人**
*   推动业务方拆分基础组件库更难，目前项目**进展不顺**
*   **维护成本高**，拆分壳工程运行结果和主工程可能**不一致**
*   业务迫切其结果，但**投入产出比不足**，比如Flutter单页面性能测试，Flutter侧模块化拆分，Fass工程一体基石

## **方案二：跨进程开发换位思考**

*   若自己是业务方，需要为Flutter侧去拆分包，去构建一个最小化壳工程，其成本是巨大的。
*   Fass工程一体化依赖一个最小化壳工程的Native运行环境去运行Flutter侧代码，可是并非所有的业务方都会提供一个最小化壳工程去运行Fass，那么Fass工程一体化/模块开发如果在集团其他运行环境下进展？
*   最小化壳工程运行环境无法紧跟Native侧的各种版本，会导致运行结果不一致情况下也不敢随便使用；

如果解决此问题呢？个人提出过跨进程实现方式，在Android端侧跨进程调用实现方式一直很常见的场景，client访问server的结果，而Flutter侧和Native侧不就是client和server双端么？如下图所示，其实Flutter获取数据就是通过MethodChannel/EventChannel获取，因此可以换一种方式思考？

## **IPC跨进程通信，Android Binder**

期间在Android侧我使用过Android Binder去实现，新起一个APP做为壳工程，其内部实现了各种插件去访问主工程服务，获取结果然后返回给壳工程的Flutter调用，但是维护成本依然在；同时iOS侧没有对应的实现机制，因此此方式被抛弃；

## **具体方案：Hook代理+Socket服务**

Android开发应该都熟悉hook和插件化技术，其实从之前的Flutter到Native的Chanel架构就可以想到一种思路，既然解决不了Native问题，那就解决Channel的问题吧，Native端侧的IPC方式无法实现，换到Flutter侧和Native侧的Channel通信侧去实现IPC吧。参考业务对于插件化hook机制/IPC机制的理解，结合自身对于flutter channel的理解，可以实现一种利用socket服务去hook method channel和event channel实现方式，去代理客户端的method channel和event channel，将处理结果通过socket交给服务端去处理拿到服务端真正的method channel和event channel数据即可，这才是我心中想要的实现方式就是如此，整个架构图如下：

" data-caption="" data-size="normal" data-rawwidth="946" data-rawheight="644" data-default-watermark-src="https://pic1.zhimg.com/50/v2-9c02e063a0cfcc2907ad0d98e5a8bdb9_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="946" data-original="https://pic3.zhimg.com/v2-58a1372470eb2a67a40f9d742e3c5299_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-58a1372470eb2a67a40f9d742e3c5299_hd.jpg?source=1940ef5c">

客户端是一台手机，服务端也是一台手机，服务端跑闲鱼FWN主工程，客户端跑一个干净的Flutter工程；客户端先通过Flutter侧代码去找使用本端有对应的Channel，如果有则使用返回结果，如果没有则通过Socket请求结果到服务端主工程上，主工程根据Socket定义的协议字段去解析然后发起一个channel拿结果，之后通过socket将解决返回给客户端，客户端拿到了socket结果数据后执行想要的渲染方式即可；或许你有质疑点：比如为什么要用2台手机，使用一台不可以么？这里我推荐使用2台手机有如下2个原因：

*   一台手机运行2个APP，如果server在后台可能会导致进程资源被回收，Socket通信中断；
*   使用2台手机有一个极大好处是，你运行Android的Flutter侧Client代码，但是往往你需要验证Native侧双端Server代码数据，如果客户端手机/服务端手机是2台，只需要改下客户端的IP地址去请求Android手机的Server还是IOS手机的Server就可以验证结果；

## **尝试验证**

比如如下的method channel代码如下：

 <code class="language-text">Future
<T> invokeMethod<T>(
String
 method, [ 
dynamic
 arguments ]) 
async
{

assert
(method != 
null
);

final
ByteData
 result = 
await
 binaryMessenger.send(

      name,

      codec.encodeMethodCall(
MethodCall
(method, arguments)),

);

if
(result == 
null
) {

throw
MissingPluginException
(
'No implementation found for method $method on channel $name'
);

}

final
 T typedResult = codec.decodeEnvelope(result);

return
 typedResult;

}</code>

修复result == null的场景，如果是我们指定的客户端，则通过socket去拿server数据,重点理解Fish MOD:START到Fish MOD:END代码思想就理解了；

 <code class="language-text">Future
<T> invokeMethod<T>(
String
 method, [
dynamic
 arguments]) 
async
{

assert
(method != 
null
);

final
ByteData
 result = 
await
 binaryMessenger.send(

      name,

      codec.encodeMethodCall(
MethodCall
(method, arguments)),

);

if
(result == 
null
) {

//Fish MOD:START

//throw MissingPluginException(

//      'No implementation found for method $method on channel $name');

//socket从服务端手机获取值

finaldynamic
 serverData =

await
SocketClient
.methodDataForClient(clientParams);

//Fish MOD:END

}

final
 T typedResult = codec.decodeEnvelope(result);

return
 typedResult;

}</code>

最后通过此种方式验证了MethodChannel/EventChannel数据正常收发的可行性，后续还需要在业务场景具体实验耕田。

## **效果对比与后续**

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="206" data-default-watermark-src="https://pic4.zhimg.com/50/v2-1cc86d320087b48abc8b6ca2eaaaf1a0_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic4.zhimg.com/v2-3b7a3dc97a238769fb40ce43765d8aac_r.jpg?source=1940ef5c" data-actualsrc="https://pic1.zhimg.com/50/v2-3b7a3dc97a238769fb40ce43765d8aac_hd.jpg?source=1940ef5c">

无法方案1和方案2最终都可以解决编译运行时长的问题，但方案1在拆分模块和维护模块时候都有很高的成本，运行时长虽然降低了，但是模块化工作量却加大很多，方案2可以完美解决拆分成本和维护成本，但是不足之处就是运行环境苛刻，可操作性不足，其需要2部手机作为运行环境，另针对于一些页面跳转逻辑，可能客户端手机A触发到服务端手机B上，操作性不在同一台手机上；当然方案二虽然有一定缺陷，却可以解决很多问题，因此后续在闲鱼模块化拆分落地项目中，在思考是否有更加完美的解决方法。

————————————————————————————————————————

本账号主体为阿里巴巴淘系技术，淘系技术部隶属于阿里巴巴新零售技术事业群，旗下包含淘宝技术、天猫技术、农村淘宝技术、闲鱼、躺平等团队和业务，是一支是具有商业和技术双重基因的螺旋体。
入驻知乎，将会给大家带来超多干货分享，立体化输出我们对于技术和商业的思考与见解。
详情介绍可以看这里 [阿里巴巴淘系技术介绍](https://zshipu.com/t?url=https://zhuanlan.zhihu.com/p/141070026)
欢迎收藏点赞关注我们！共同进步~ ：）更多技术干货可关注【淘系技术】公众号 > 作者：阿里巴巴淘系技术
