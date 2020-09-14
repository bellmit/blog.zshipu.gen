
title: 阿里巴巴优化flutter到底有多彻底
author: 知识铺
date: 2020-09-13 21:16:34
tags: 
---
  高性能高流畅度一直是Flutter团队宣传的一大亮点，也是当初闲鱼选择Flutter的重要因素之一，但是随着复杂业务的应用落地，通过Flutter页面和原生页面滑动流畅度对比，我们开始产生怀疑——

因为部分Flutter页面流畅度明显低于Native，是Flutter的宣传言过其实？还是我们开发人员使用姿势有问题？今天我们就来具体分析下。

## **Flutter渲染原理简介**

优化之前我们先来介绍下Flutter的渲染原理，通过这部分基础了解渲染流程以及主要耗时花费。

Flutter视图树包含了三颗树：Widget、Element、RenderObject

*   Widget: 存放渲染内容、它只是一个配置数据结构，创建是非常轻量的，在页面刷新的过程中随时会重建
*   Element: 同时持有Widget和RenderObject，存放上下文信息，通过它来遍历视图树，支撑UI结构
*   RenderObject: 根据Widget的布局属性进行layout，paint ，负责真正的渲染

从创建到渲染的大体流程是：根据Widget生成Element，然后创建相应的RenderObject并关联到Element.renderObject属性上，最后再通过RenderObject来完成布局排列和绘制。例如下面这段布局代码

对应三棵树的结构如下图：

了解了这三棵树，我们再来看下页面刷新的时候具体做了哪些操作？

当需要更新UI的时候，Framework 通知 Engine，Engine 会等到下个 Vsync 信号到达的时候，会通知 Framework 进行 animate, build，layout，paint，最后生成 layer 提交给 Engine。Engine 会把 layer 进行组合，生成纹理，最后通过 Open Gl 接口提交数据给 GPU， GPU 经过处理后在显示器上面显示，如下图：

结合前面的例子，如果text文本或者image内容发生变化会触发哪些操作呢？

Widget 是不可改变，需要重新创建一颗新树，build开始，然后对上一帧的element树做遍历，调用他的updateChild，看子节点类型跟之前是不是一样，不一样的话就把子节点扔掉，创造一个新的，一样的话就做内容更新，对renderObject做updateRenderObject操作，updateRenderObject内部实现会判断现在的节点跟上一帧是不是有改动，有改动才会别标记dirty，重新layout、paint，再生成新的layer交给GPU，流程如下图：

到这里大家对Flutter在渲染方面有基本的理解，作为后面优化部分内容理解的基础。

## **性能分析工具及方法**

下面来看下性能分析工具，注意，统计性能数据一定要在真机+profile模式下运行，拿到最接近真实的体验数据。

**performance overlay**平时常用的性能分析工具有performance overlay，通过他可以直观看到当前帧的耗时，但是他是UI线程和GPU线程分开展示的，UI Task Runner是Flutter Engine用于执行Dart root isolate代码，GPU Task Runner被用于执行设备GPU的相关调用。绿色的线表示当前帧，出现红色则表示耗时超过16.6ms，也就是发生丢帧现象。

**Dart DevTool**

另一个工具是Dart DevTool ，就是早期的Observatory，官方提供的性能检测工具。它的 timeline 界面可以让逐帧分析应用的 UI 性能。但是目前还是预览版，存在一些问题。profile模式下运行起来，点击android studio底部的菜单按钮，会弹出一个网页。

点击顶部的 Timeline 菜单

" data-caption="" data-size="normal" data-rawwidth="836" data-rawheight="594" data-default-watermark-src="https://pic1.zhimg.com/50/v2-fb5863882eb9564c40b4523ca3d21def_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="836" data-original="https://pic4.zhimg.com/v2-c9afaf07c1bbfb77be69f3a534c9619b_r.jpg?source=1940ef5c" data-actualsrc="https://pic2.zhimg.com/50/v2-c9afaf07c1bbfb77be69f3a534c9619b_hd.jpg?source=1940ef5c">

这个时候滑动页面，每一帧的耗时会以柱形 bar 的形式显示在页面上，每条bar代表一个 frame，同时用不同颜色区分 UI/GPU 线程耗时，这个时候我们要分析卡顿的场景就需要选中一条红色的bar（总耗时超过16.6ms），中间区域的Frame events chart显示了当前选中的frame的事件跟踪，UI 和 GPU 事件是独立的事件流，但它们共享一个公共的时间轴。

选中Frame events chart中的某个事件，以上图为例Layout耗时最长，我们选中它，会在底部Flame chart区域显示一个自顶向下的堆栈跟踪，每个堆栈帧的宽度表示它消耗CPU的时长，消耗大量CPU时长的堆栈是我们首要分析的重点，后面就是具体分析堆栈，定位卡顿问题。

**debug 调试工具**另外还有一些debug调试工具可以辅助查看更多信息，注意，只能在debug模式下使用分析，拿到的数据不能作为性能标准

debugProfileBuildsEnabled：向 Timeline 事件中添加每个widget的build 信息debugProfilePaintsEnabled：向 timeline 事件中添加每个renderObject的paint 信息debugPaintLayerBordersEnabled：每个layer会出现一个边框，帮助区分layer层级debugPrintRebuildDirtyWidgets：打印标记为dirty的

widgetsdebugPrintLayouts：打印标记为dirty的renderObjectsdebugPrintBeginFrameBanner/debugPrintEndFrameBanner：打印每帧开始和结束

**实例分析**了解这些工具下面我们来看个简单的demo具体分析下，一个由Column、Container、ListView嵌套的布局，其中有个定时器控制Text中显示的文本实时更新

" data-caption="" data-size="normal" data-rawwidth="859" data-rawheight="1293" data-default-watermark-src="https://pic3.zhimg.com/50/v2-f1533dc73d533148acdd32c7e8fa7ff7_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="859" data-original="https://picb.zhimg.com/v2-f261bb5e192fdf2dfe2958ead66eb377_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-f261bb5e192fdf2dfe2958ead66eb377_hd.jpg?source=1940ef5c">

大部分 widget 都是静态的，只有黄色 Container 中包含一个内容一直刷新的 Text ，这个时候我们打开 debugProfileBuildsEnabled，用 Timeline 分析下它的渲染耗时，可以通过 Frame events chart 中显示的 build 层级非常深

" data-caption="" data-size="normal" data-rawwidth="878" data-rawheight="526" data-default-watermark-src="https://pic3.zhimg.com/50/v2-ab8e5a030eeba996cebcb0e3948d6353_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="878" data-original="https://pic3.zhimg.com/v2-528163b7704946a7f0b55172ad1a5814_r.jpg?source=1940ef5c" data-actualsrc="https://pic2.zhimg.com/50/v2-528163b7704946a7f0b55172ad1a5814_hd.jpg?source=1940ef5c">

结合第一部分渲染原理我们了解到，每次定时器刷新text数字的时候，整个页面widget树都会重新build，但其实只有最底层Container中的Text内容在改变，没有必要刷新整颗树，所以这里我们的优化方案是提高build效率，降低 Widget tree 遍历的出发点，将 setState 刷新数据尽量下发到底层节点，所以将 Text 单独抽取成独立的 Widget，setState 下发到抽取出的 Widget 内部

" data-caption="" data-size="normal" data-rawwidth="513" data-rawheight="556" data-default-watermark-src="https://pic4.zhimg.com/50/v2-219a92362ae2456f1052abe97d6a41c7_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="513" data-original="https://pic2.zhimg.com/v2-8c274b8856a96cde0506e1c641e1d830_r.jpg?source=1940ef5c" data-actualsrc="https://pic2.zhimg.com/50/v2-8c274b8856a96cde0506e1c641e1d830_hd.jpg?source=1940ef5c">

修改后的Timeline显示如下图：

" data-caption="" data-size="normal" data-rawwidth="866" data-rawheight="460" data-default-watermark-src="https://pic2.zhimg.com/50/v2-1b1fff4102724428e65879fd8d525111_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="866" data-original="https://pic4.zhimg.com/v2-3d9f5a6a80a7395276ffa16ea2d9cc2b_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-3d9f5a6a80a7395276ffa16ea2d9cc2b_hd.jpg?source=1940ef5c">

build 层级明显减少，总耗时也明显降低。

接下来分析下 Paint 过程有没有可以优化的部分，我们打开 debugProfilePaintsEnabled 变量分析可以看到 Timeline 显示的 paint 层级

" data-caption="" data-size="normal" data-rawwidth="863" data-rawheight="371" data-default-watermark-src="https://pic3.zhimg.com/50/v2-fe657464423ff48f3ab9e7de5155ddcc_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="863" data-original="https://pic3.zhimg.com/v2-4364784f73cccd24c153e2ef05b78b2a_r.jpg?source=1940ef5c" data-actualsrc="https://pic1.zhimg.com/50/v2-4364784f73cccd24c153e2ef05b78b2a_hd.jpg?source=1940ef5c">" data-caption="" data-size="normal" data-rawwidth="842" data-rawheight="1288" data-default-watermark-src="https://pic1.zhimg.com/50/v2-d9a6b5c6c84f61365608f14a2524a261_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="842" data-original="https://pic4.zhimg.com/v2-9ee461d535192ba3c41f0dc95fd80501_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-9ee461d535192ba3c41f0dc95fd80501_hd.jpg?source=1940ef5c">

通过 debugPaintLayerBordersEnabled=true;显示layer边框可以看到不断变化的 Text 和其他 Widget 都是在同一个 layer 中的，这里我们想到的优化点是利用RepaintBoundary提高paint效率，它为经常发生显示变化的内容提供一个新的隔离layer，新的layer paint不会影响到其他layer。

" data-caption="" data-size="normal" data-rawwidth="506" data-rawheight="198" data-default-watermark-src="https://pic2.zhimg.com/50/v2-85aa76dfe0874286c46b7bd0f4962555_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="506" data-original="https://pic2.zhimg.com/v2-39771960da5925c93dc745aea2674907_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-39771960da5925c93dc745aea2674907_hd.jpg?source=1940ef5c">

看下优化后的效果

" data-caption="" data-size="normal" data-rawwidth="866" data-rawheight="364" data-default-watermark-src="https://picb.zhimg.com/50/v2-9414af0e2e63a80e371c2fbc300b28b0_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="866" data-original="https://pic1.zhimg.com/v2-244b50e52ae42c008efb67e9a90612c9_r.jpg?source=1940ef5c" data-actualsrc="https://pic1.zhimg.com/50/v2-244b50e52ae42c008efb67e9a90612c9_hd.jpg?source=1940ef5c">" data-caption="" data-size="normal" data-rawwidth="865" data-rawheight="1301" data-default-watermark-src="https://pic4.zhimg.com/50/v2-efdafba83bf4f648a51d0ac26af61ec7_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="865" data-original="https://pic3.zhimg.com/v2-38132af1b420bb24016016c2fd63e104_r.jpg?source=1940ef5c" data-actualsrc="https://pic1.zhimg.com/50/v2-38132af1b420bb24016016c2fd63e104_hd.jpg?source=1940ef5c">

可以看到我们为黄色的Container建立了单独的layer，并且paint的层级减少很多。

**常见问题总结**

*   提高build效率，setState刷新数据尽量下发到底层节点
*   提高paint效率，RepaintBoundry创建单独layer减少重绘区域

这两个我们之前的例子已经具体分析过

*   减少build中逻辑处理，因为widget在页面刷新的过程中随时会通过build重建，build调用频繁，我们应该只处理跟UI相关的逻辑
*   减少saveLayer（ShaderMask、ColorFilter、Text Overflow）、clipPath的使用，saveLayer会在GPU中分配一块新的绘图缓冲区，切换绘图目标，这个操作是在GPU中非常耗时的，clipPath会影响每个绘图指令,做相交操作，之外的部分剔除掉，所以这也是个耗时操作
*   减少Opacity Widget 使用，尤其是在动画中，因为他会导致widget每一帧都会被重建，可以用 AnimatedOpacity 或 FadeInImage 进行代替

以上内容介绍了些Flutter常见的性能问题以及我们怎么用工具检测这个问题，在平时开发过程中要留意规避这类问题。

## **Flutter-DX案例分析**

近期我们做了个Flutter端的动态化模板渲染方案Flutter-DX，它使用集团DinamicX的DSL，通过下发DSL模板，在Flutter侧实现动态解析渲染。具体介绍可以参考之前的文章：

<u>[《如何在Flutter上实现高性能的动态模板渲染》](https://zshipu.com/t?url=https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzU4MDUxOTI5NA%3D%3D%26mid%3D2247484759%26idx%3D1%26sn%3D6ebb553cec9adf09300ea01c260b71d5%26chksm%3Dfd54d146ca235850b516ae303fe79d5716b035ac1f465d064ce2c17b249449636031acd0e844%26scene%3D21%23wechat_redirect)[《做一个高一致性、高性能的Flutter动态渲染，真的很难么？》](https://zshipu.com/t?url=https://link.zhihu.com/?target=http%3A//mp.weixin.qq.com/s%3F__biz%3DMzAxNDEwNjk5OQ%3D%3D%26mid%3D2650405380%26idx%3D1%26sn%3D8c78cd72a8d7611c85865c9076417f9c%26chksm%3D8395321cb4e2bb0a4993e9ef19f9d4fe5cf2320277654d3ffaa30b6aba74c109f09335e7e6c2%26scene%3D21%23wechat_redirect)</u>这里不再详细介绍。尽管进行了一次渲染架构升级，很大程度上提升性能表现，但是通过高可用线上统计，发现在长列表场景下fps值没有达到预期值，所以需要进一步分析哪些操作导致的耗时问题。以搜索页页面结构为例，外部是GridView的容器，里面都是一个个DX模板组成的宝贝card，滑动过程中发现流畅度要明显偏低所以我们做了以下的优化措施

*   针对Sliver滑动的优化，sliver在滑动过程中，有一个超出屏幕上下250像素的一个缓存区

" data-caption="" data-size="normal" data-rawwidth="462" data-rawheight="455" data-default-watermark-src="https://pic2.zhimg.com/50/v2-14a824f71707a58c38f49201440a7370_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="462" data-original="https://pic1.zhimg.com/v2-4a3f53094e4b964a88aff0f08bb21893_r.jpg?source=1940ef5c" data-actualsrc="https://pic2.zhimg.com/50/v2-4a3f53094e4b964a88aff0f08bb21893_hd.jpg?source=1940ef5c">

在列表滚动过程中，DX card不断的被重建和销毁，没有任何缓存机制，我们在其中加了个缓存池，流程如下，避免element不断的被销毁和创建，一定程度提高流畅度。

" data-caption="" data-size="normal" data-rawwidth="735" data-rawheight="967" data-default-watermark-src="https://pic4.zhimg.com/50/v2-5d54f0ff225830e65da86800837bc73a_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="735" data-original="https://pic4.zhimg.com/v2-b2a6698629b965b74db2e1ebddbc2b00_r.jpg?source=1940ef5c" data-actualsrc="https://pic2.zhimg.com/50/v2-b2a6698629b965b74db2e1ebddbc2b00_hd.jpg?source=1940ef5c">

*   通过Timeline分析发现TextPaint的layout耗时显著，进一步对比分析发现，同样的UI显示，带换行符的长文本长度layout耗时明显偏高，

后来确认带换行符的文本会影响布局效率，具体分析可以查看 issue

" data-caption="" data-size="normal" data-rawwidth="552" data-rawheight="570" data-default-watermark-src="https://picb.zhimg.com/50/v2-fdc40aa8bf2adfc275584e2a974d44f9_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="552" data-original="https://pic4.zhimg.com/v2-52103c7191253ea6bb5420453c7e7564_r.jpg?source=1940ef5c" data-actualsrc="https://pic4.zhimg.com/50/v2-52103c7191253ea6bb5420453c7e7564_hd.jpg?source=1940ef5c">

这里我们做的优化措施是在判断只有一行文本显示的情况下，截取换行符前的内容作为text文本，从而提升TextPaint layout效率。

除此之外，还有一些减少布局层级和简化build流程，预加载缓存等措施，实现将FPS提升3个点，达到一定程度的优化效果。

## **总结**

以上内容分析了flutter的渲染原理以及遇到卡顿问题可以用哪些工具从哪些方向入手分析，Flutter 虽然一直宣称流畅度是一大亮点，但也存在一定的优化空间，以及需要开发者掌握一定的开发技巧才能达到更丝滑的体验。

——————————————————————————————————

本篇回答内容来自阿里巴巴淘系技术部无线开发专家三莅。

本账号主体为阿里巴巴淘系技术，淘系技术部隶属于阿里巴巴新零售技术事业群，旗下包含淘宝技术、天猫技术、农村淘宝技术、闲鱼、躺平等团队和业务，是一支是具有商业和技术双重基因的螺旋体。

刚刚入驻知乎，将会给大家带来超多干货分享，立体化输出我们对于技术和商业的思考与见解。

详情介绍可以看这里 [阿里巴巴淘系技术介绍](https://zshipu.com/t?url=https://zhuanlan.zhihu.com/p/141070026)

欢迎收藏点赞关注我们！共同进步~ ：） > 作者：阿里巴巴淘系技术
