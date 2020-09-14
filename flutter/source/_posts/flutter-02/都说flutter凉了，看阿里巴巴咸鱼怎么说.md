
title: 都说flutter凉了，看阿里巴巴咸鱼怎么说
author: 知识铺
date: 2020-09-13 21:17:13
tags: 
---
  0907更新，阿里巴巴淘系技术近期推出阿里 Flutter 体系化建设的系列直播，话题涵盖**基础设施、框架体系、研发支撑、能力拓展、研发模式**五方面，关注【淘系技术】公众号，回复数字 06 即可获取直播地址。（零门槛）

直播时间：9月10日起，9月28日结束。总计6场。

————————————————————————————————————————————

去年，2019 年无疑是 Flutter 技术如火如荼发展的一年。

每一个移动开发者都在为 Flutter 带来的“快速开发、富有表现力和灵活的 UI、原生性能”的特色和理念而痴狂，从超级 App 到独立应用，从纯 Flutter 到混合栈，开发者们在不同的场景下乐此不疲的探索和应用着 Flutter 技术，也在面临着各种各样不同的挑战。

阿里巴巴集团内也有越来越多的业务和团队开始尝试 Flutter 技术栈，从闲鱼的一支独秀引领潮流，到如今淘宝特价版、盒马、优酷、飞猪等BU业务相继入局，Flutter的业务应用在集团内也已经逐渐形成趋势。

那么，**是什么原因让集团内越来越多的开发者选择拥抱Flutter技术栈？Flutter的哪些优势吸引了集团Native开发者们通过Flutter开发并交付业务？**

我们分享一下阿里集团内进行Flutter体系化建设的情况，以供参考和交流。

从技术上看，阿里巴巴新零售淘系技术部的思牧认为Flutter最核心的3个特点最为吸引开发者：

*   极高的开发与交付效率，良好的开发体验
*   优秀的跨多端多平台能力
*   极强的 UI 表现力

先说一下**开发效率**。从集团电商业务属性出发，业务响应效率及其背后的研发效率从来都是最为重要的指标。在保证体验的前提下，尽可能的提高研发效率，就意味着更高的生产力。传统的 Native 业务研发 iOS/Android 双端需要分别投入，研发成本高，端差异性大且依赖端侧发版，这也是为什么集团电商业务的活动类技术栈一直较为依赖前端体系，从H5到Weex到小程序，很大程度上就是在追求研发和交付效率以及灵活性。如今 Flutter 很好的解决了跨端一致性问题，一套代码无差异的同时跑在 iOS 与 Android 两端；开发体验基本接近前端，支持 on device 的 Hot Reload ，去年年底 Flutter 又推出了在 Android Studio 中通过插件实现实时预览并支持交互的 Hot UI 能力，以及 Layout Explorer 可视化布局，让Flutter的开发效率和前端效率基本持平。

电商业务发展到当前阶段，已经不再仅仅局限于移动端场景，越来越多的业务需求对跨端跨平台性提出了更高的要求。钉钉/千牛桌面端应用场景，甚至天猫精灵、线下门店等业务场景，从长远看都需要一个比 Web 性能一致性更好适配成本更低的多端方案。目前跨多端技术方案主要依赖于浏览器和前端体系，但浏览器本身的沙盒属性、与系统较低的结合度、以及在低端设备上较差的性能都降低了研发效率和用户体验，提高了业务的交付门槛。

可以说目前集团内的跨多端多平台方案是实质缺失的。Flutter 从设计上就天然支持多平台开发，它的底层基于 Skia 跨平台图形引擎，向上构建出了一整套平台无关的渲染体系和事件处理体系，并紧贴 Native 研发模式自定义了基于 widgets 的声明+响应式编程范式，对系统能力依赖度低，并具备出色的跨平台还原度；支持多平台也是 Flutter 的战略目标之一。

目前除了 iOS 和 Android ，官方宣布支持的平台有 Mac、Windows 和 Web，Linux 也在开发中，它的技术特性也让将 Flutter移植到 Linux based IoT 平台上成本很低，同时 Flutter 还是未来 Google 的下一代操作系统 Fuschia 的官方应用研发框架。可以说Flutter已经具备了成为下一代跨多端多平台研发模式的一切条件，围绕Flutter建立集团的多端多平台研发体系是非常可行的选择。

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="473" data-default-watermark-src="https://pic2.zhimg.com/50/v2-e83396c07ca65640460f7d7b823de7f2_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic2.zhimg.com/v2-b477f5fe1e70ec575c398b1b8cc64dc9_r.jpg?source=1940ef5c" data-actualsrc="https://pic1.zhimg.com/50/v2-b477f5fe1e70ec575c398b1b8cc64dc9_hd.jpg?source=1940ef5c">

最后讲一下 **UI 表现力**。电商业务重体验，重交互，尤其对于流量精细化运营场景，富交互的游戏化表现方式已经成为流量促活的重要手段。在 UI 表现力方面，前端体系一直具备着优势，通过 CSS3 强大的动画能力，开发者可以非常容易的实现复杂的动画效果和交互体验，而基于 Native UI ，需要借助各种动画特效三方库，双端开发体验不一致，实现复杂且交付效率低。

Flutter很好的解决了这个问题，从补间（Tween）动画、基于物理属性的动画，到相对复杂的页面间Hero动画、parallax交错动画等特效，Flutter都可以跨平台低成本的高效实现。

## **Flutter体系化建设现状**

目前集团内有多个业务 BU 均已开始尝试应用 Flutter 技术栈，涵盖了从电商详情业务、导购频道，到 Feeds 流、游戏化交互以及国际化等多个业务场景。目前 Flutter 技术在集团应用的痛点在于，研发基础设施的中台基建不够完善，研发支撑能力与数据运维能力未实现标准化，集团 Flutter 开发者生态还未完全拉通，暂时未能形成合力。这些问题将是我们后面在集团层面建设 Flutter 技术体系的重点。

另一方面从行业趋势上看，Flutter 技术已经成为越来越多行业伙伴重点投入的技术建设方向。字节跳动、美团等公司均建设了自己的 Flutter 工程化体系，并服务了各自的业务场景；腾讯也基于 Flutter 在多个 App 上进行了应用尝试，并在 Flutter 渲染能力服务小程序的场景下做了有益探索。行业伙伴们在 Flutter 技术上的投入力度和决心，一方面让我们对 Flutter 技术的应用前景和社区更有信心，另一方面也让我们感到联合集团各方力量共建 Flutter 生态的必要性和紧迫性。

### ▐ 手淘的尝试和思考

最后，简单讲一下我们从18年到现在在 Flutter 上做的探索和思考。手淘从18年10月开始探索 Flutter 渲染引擎应用在小程序场景；19年下半年开始建设 Flutter 基础能力，并服务了淘宝特价版业务，在引擎、图片库、内存优化和加载性能等关键技术上做了沉淀；同时通过对 Flutter 的引擎改造，封装出 Flutter 2D Canvas 能力，向上支持小程序 Canvas 组件及小游戏引擎，服务 2D/2.5D 游戏化业务，并在业务场景中落地。

在这个过程中，我们也沉淀了解决内存问题和图片问题等方案，以及 Flutter 技术与 Web 技术的对比与思考，取得了一定的技术及业务价值。 通过这些尝试，加深了我们对 Flutter 技术的掌控力和理解。在我们看来， Flutter 的横空出世，完全可以被看作吹响了 Native 体系复兴的号角。在保持 Native 性能优势的前提下，Flutter 带来了优秀的跨端一致性、贴近前端的研发效率，以及强大的 UI 表现力，为集团业务使用 Native技术栈带来了新的可能。

**从业务应用上看：**Flutter 目前带来的最大价值是研发效率的提升。在基建和 native 扩展能力完备的前提下，开发基于 Flutter 的纯 Dart 业务的人效比之前各端分别开发的效率提高了接近 2 倍，单位时间内的需求响应能力也相应提高了接近2倍，目前已在闲鱼和特价版业务开发中得到了很好的工程化验证。

**从适应场景看：**Flutter 目前比较适合承载富图文内容，如详情、Feeds 流、用户主页等常规业务开发，以及 2D/2.5D 游戏场景以及富动效业务。Flutter 通过单端技术栈可以同时满足以前需要 iOS、Android 以及前端技术栈分别负责的业务场景，甚至可以通过端云一体化的开发模式使用 Dart 负责一部分服务端业务逻辑开发，可以帮助业务团队拓展业务边界的同时，实现前后端研发能力闭环。Flutter 目前的限制在于，动态性能力及前期的投入成本。

前期投入成本主要指技术学习与团队研发模式升级的成本，涉及到技术路线选择，是我们和每个业务团队需要一起思考和判断的，这里不展开谈。动态性能力是 Flutter 的相对短板，目前能够通过 Flutter 模板化技术实现基于模板的组件级动态化能力，但基于性能、审核及对原生 Flutter 体系的侵入性等多种因素，目前还不能去直接实现UI + 逻辑动态化能力。Flutter Web 方案虽然不存在审核限制，但受限于浏览器 DOM API 与 widgets 体系的差异性，目前仍旧存在较严重的性能瓶颈和渲染差异性，仅可作为降级的备用方案，暂时无法作为动态化的主要实现方案。

未来在动态化方向的探索也将是个长期的博弈过程。如果后面我们可以解决好 Flutter 动态化的问题，那么 Flutter 完全有机会成为集团业务的核心研发模式之一。综上我们认为，入局 Flutter 的时机已成熟，合力共建 Flutter 集团移动生态，这件事情大有可为。

## **AliFlutter - 经济体移动小组Flutter共建项目**

在这样的背景下，经济体移动技术小组今年也将端侧架构治理的重点方向放在了 Flutter 上。移动技术小组从战略角度提出了 AliFlutter 项目，目标非常明确：

*   从经济体层面拉通 Flutter 体系建设，打造 Flutter 的公共技术基础设施，制定 Flutter 容器、中间件与 API 标准，建设 Flutter 研发支撑与数据运维能力，复用关键技术；
*   联合各 BU 构建经济体Flutter技术社区，沉淀共享集团 Flutter 技术及业务组件、能力与解决方案，服务集团 Flutter 业务，共建集团 Flutter 技术生态；
*   在经济体层面构建 Flutter 的对外影响力，联合各 BU 一致对外，打造阿里在行业内的 Flutter 技术制高点。

为经济体的 Flutter 技术体系“建基础、育社区、扛大旗”，我们责无旁贷。未来 AliFlutter 的整体架构如下所示：

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="579" data-default-watermark-src="https://pic1.zhimg.com/50/v2-1c9c16cd9c8b8ef6468521a5b46ece02_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic3.zhimg.com/v2-9af294ed11d118077467a02d0d068631_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-9af294ed11d118077467a02d0d068631_hd.jpg?source=1940ef5c">

**AliFlutter 建设的第一步，**就是要构建集团的 Flutter 基础设施、提供公共容器与组件、研发支撑服务与标准化研发流程，为集团的 Flutter 业务提供一个基础的Flutter公共研发服务能力，搭建好技术共建共享的基础和平台；

**第二步，**我们要服务好 Flutter 业务应用，探索业务应用模式与 Flutter 技术特性的结合点，并在过程中打磨技术，形成针对业务特点的解决方案与技术沉淀，真正盘活集团内的 Flutter 社区共建氛围与生态；

**第三步，**面向未来，解决好Flutter应用的几个核心关键问题：跨端与交互能力、业务研发效率与业务交付效率，通过技术赋能业务，让 Flutter 真正成为集团移动业务的核心研发模式。接下来，就详细讲一讲每个阶段 AliFlutter 所做的工作和面向未来的思考。

## **基础设施建设**

从19年10月 AliFlutter 项目启动开始到现在，我们基本构建起了一套 Flutter 的公共基础设施，包括 Artifacts 与 pub 库，Flutter 标准容器与 API 标准，并实现了 Flutter 的构建打包自动化，定义了标准的引擎定制工作流与业务研发工作流。目前基础设施已经具备支撑集团 Flutter 业务研发的能力，并支持各 BU 按需定制。

### ▐ Artifacts仓库

产物服务器主要是为了配合引擎定制，加速通过 Flutter 命令获取 Engine 中间产物的后端服务，便于统一 Flutter 开发者的工作环境。开发者可通过设置 FLUTTER_STORAGE_BASE_URL来将Flutter工具链获取 artifacts 的地址指向该服务，同时通过 namespace 便可实现定制化的获取 artifacts 的能力以及内网加速服务。 Namespace 设计为区分不同 BU 的引擎产物，同时提供了公共 namespace 来存储公共产物，确保定制性和公共能力的按需配置；若后端存储上不存在需要获取的产物地址，则会触发从 Flutter 官方镜像做一次获取并缓存在服务端。 各 BU 可按需定制引擎，并按规定的路径格式上传至自己 namespace 中，即可实现从 namespace 中获取定制版本的引擎中间产物。

### ▐ pub仓库

" data-caption="" data-size="normal" data-rawwidth="1060" data-rawheight="554" data-default-watermark-src="https://pic4.zhimg.com/50/v2-f3068466e311817d08feece53166117b_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1060" data-original="https://pic2.zhimg.com/v2-f31b881b2fe0c52148b145612fbbdda8_r.jpg?source=1940ef5c" data-actualsrc="https://picb.zhimg.com/50/v2-f31b881b2fe0c52148b145612fbbdda8_hd.jpg?source=1940ef5c">

类似于 Node.js 世界的 npm，Flutter 使用 pub 来管理三方组件与依赖。考虑到易用性、安全性等需求，为了管理集团内的公共二方组件，我们也搭建了内网环境的 Flutter pub 库。该库的目标是成为集团的 pub 发布平台，管理集团内所有二、三方 pub package。用户可通过设置 PUB_HOSTED_URL 指向内部地址，来实现通过 Flutter 工具链获取配置以及发布二方 pub 的能力，用户也可以通过 Web portal 的方式访问 pub 库并查询已发布的 pub 组件。

### ▐ 容器、中间件与API

对于业务的接入而言，现阶段核心要解决的问题就是提供一个统一的 Flutter 运行时容器，以及一系列集团标准化移动中间件的 Flutter 封装与 API 能力，并提供集团标准的插件扩展方式供业务方独立开发业务功能。

鉴于集团应用基本上均以混合栈为主，我们将 FlutterBoost 作为 Flutter 容器混合栈的基础，并配合集团标准路由与导航中间件提供了统一的混合栈路由导航能力，业务通过标准路由注册即可快速实现 Flutter 页面和 Native 页面的混合导航能力。

容器通过对接高可用平台，提供了初始化性能埋点与 Crash 数据上报等标准监控能力，为 Flutter 业务的技术性能分析和问题排查提供了基础。集团移动端积累了一整套的标准中间件体系，包括网络库、图片库、push 消息、配置下发、数据采集与监控等一系列基础能力，在 Flutter 体系内无缝使用移动中间件能力对于业务是刚需。

同时，小程序体系建设过程中形成的一系列标准 API，也很大程度上实现了一个完整的小程序运行环境的底层能力抽象，对于 Flutter 体系标准化的访问系统能力，实现平台无关的跨端能力是个非常好的补充。

我们联合淘宝中间件团队与小程序团队，对基础中间件和小程序 API 实现做了 Flutter 侧的封装与标准化，未来也将对 Flutter 中间件和 API 能力进行系统支持。

### ▐ 标准化Flutter构建

由于 Flutter 研发体系较新，且构建 Pipeline 相较传统的移动构建流程又存在一定特殊性，产物构建配置复杂耗时长易出错，给 Flutter 业务的构建和发版带来了很大阻碍。因此我们也联合研发支撑部的同学，以插件的形式实现了 Flutter 脚本化的构建流程，支持双端自动整包打包和 Flutter Module 打包。 目前 AliFlutter 的构建流程默认使用 AliFlutter 的 Flutter 仓库以及集团内部 pub 仓库，引擎产物也统一按配置从 artifacts 仓库获取，较好的实现了支持 Flutter 业务的自动化构建需求。

## **业务应用**

在夯实 Flutter 集团共建基础之后，第二步，我们 AliFlutter 在业务应用方面也做了大量工作。一方面通过原生 Flutter 的工程化能力持续服务淘系与集团业务；另一方面通过 Flutter Canvas 项目服务了小程序场景及游戏化场景下的互动业务

### ▐ 淘系与集团业务支撑

目前淘宝特价版已完成详情业务的 Flutter 改造并上线，采用 Flutter 使业务在需求节奏不变的情况下人力投入减少一半，对缓解业务研发压力起到了明显的作用；同时应用的整体性能和稳定性与 Native 基本持平。

后续特价版将基于 Flutter 继续拓展业务改造范围，并沉淀基于 Flutter 的业务域解决方案。

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="533" data-default-watermark-src="https://pic4.zhimg.com/50/v2-6f61079e9ea3b2c0200fdf8ed6d20657_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic1.zhimg.com/v2-a1dd21d4acf38f6d96460a53073c08d0_r.jpg?source=1940ef5c" data-actualsrc="https://pic3.zhimg.com/50/v2-a1dd21d4acf38f6d96460a53073c08d0_hd.jpg?source=1940ef5c">

目前盒马、ICBU 、优酷也基于 AliFlutter 进行了容器接入升级与业务适配，盒马依托闲鱼的 Flutter 游戏引擎实现了盒马小镇业务，ICBU 在主链路相关页面使用了 Flutter，优酷则基于 Flutter 实现了会员订单页等场景。

同时我们也在和钉钉及 Google 一起探索 Flutter 桌面端的解决方案。

### ▐ Flutter Canvas

在电商活动营销中互动场景日益增多，对性能要求持续提升的前提下，如何提供一个高性能且稳定的Canvas基础能力服务好富交互的互动场景就成为了一个重点的课题。

在小程序场景中 Canvas 作为承载互动游戏的主要能力发挥了重要作用。然而受限于小程序架构下 app context 和 page context 的隔离设计，存在从 app worker 到 page renderer 的通信瓶颈，无法充分发挥出 web canvas 的性能，如果有一个 native 版的 canvas 实现将可直接在 native 层对接 app worker ，降低通信成本，充分发挥 Canvas 的性能。

Flutter 底层基于 Skia，其性能和移动端复杂异构机型的适配性均得到过长期的检验，且 Flutter 基于浏览器的设计实现了一条平台无关的渲染管线，并对浏览器实现做了极大的简化，提供了很好的可靠性和性能。那么如果能够将这条渲染管线直接用于向业务容器提供 Canvas 能力，通过 binding 方式直接向小程序和小游戏容器提供与 Web Canvas 一致的标准 API，一方面可以复用 Flutter 的底层能力，为非 Dart 环境提供渲染支持，另一方面可以借助 Flutter 简化高效的渲染管线实现提供更好的渲染性能。

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="690" data-default-watermark-src="https://pic2.zhimg.com/50/v2-c39d7a69fcd37929bdd572898ac0957b_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic4.zhimg.com/v2-7ac66316849f554a1ae431cb9a7667f9_r.jpg?source=1940ef5c" data-actualsrc="https://picb.zhimg.com/50/v2-7ac66316849f554a1ae431cb9a7667f9_hd.jpg?source=1940ef5c">

目前 Flutter Canvas 已落地手机淘宝，并在小程序运动银行业务进行了灰度试点，初步具备了承载小程序 Canvas 业务的能力；其性能在 Android 低端机上的表现有优势，可以作为 Web Canvas 方案的有益补充。

未来 Flutter Canvas 一方面将借助 Flutter 渲染管线的跨平台与高性能特点，以及 Flutter 对 Vulkan 和 Metal 的适配支持，在移动端获得更好的适配性以及性能；同时将继续实现 3D API ，支撑未来互动类的业务应用。

## **未来建设**

扎根业务之后，接下来的第三步，我们要紧贴 Flutter 体系在阿里集团未来的建设目标，持续回答好Flutter面向未来建设路径中的几个关键问题。那么首先，Flutter体系在阿里集团的建设目标应该是什么？个人以为：Flutter应成为阿里集团未来跨多端多平台的核心业务研发模式之一。那么，我们目前离这个目标还有多大差距？在我看来，如果要想让Flutter成为业务的核心研发模式，那么必须解决好跨端能力、交互能力、业务研发效率以及业务交付效率四个核心问题。

*   **从跨端能力看：**Flutter虽然已具备了很好的跨多端能力与高还原度，但涉及到平台能力时，仍然需要通过各端扩展实现，还未形成小程序体系这样的标准化的容器和API封装能力。那么如何更好的解决Flutter的容器化问题，让业务不感知平台差异性？
*   **从交互能力看：**Flutter如何利用好自身交互能力的优势，在提供媲美前端的富交互体验的同时，降低Native富交互特性开发的门槛，真正吸引Native开发者使用Flutter技术开发业务？
*   **从业务研发效率看：**虽然 Flutter 的 Hot Reload/Hot UI 机制已经让开发 Native 页面的效率追上了前端，但在工程解耦方面仍然有很大提升空间，目前还无法高效的支持多业务团队并行开发；另一方面如何与现今流行的 Serverless 能力结合，实现端云一体研发模式，使业务实现研发闭环，也需要实践的检验。
*   **从业务交付效率看：**目前 Flutter 仍属于 Native 方案，依赖端侧发版，交付效率低，无法很好的承载电商系灵活性和实效性的需求；那么如何解决Flutter的动态化，帮助业务实现快速迭代？

解决好这几个问题，才能真正让 Flutter 成为集团移动业务的核心研发模式，为集团业务研发带来一个飞跃性的提升。下面讲讲我们在这几个方向的思考和探索。

### ▐ 提升跨端能力：Flutter 容器化

从工程角度看，虽然 Flutter 通过 Skia 跨平台图形渲染和自建事件体系基本实现了对宿主平台的最小依赖，但对于平台侧能力，目前 Flutter 还未也没有必要从应用框架角度做到一个统一的抽象，这就需要我们根据业务的诉求和特点进行有选择的封装。小程序 API 就做了一个非常好的示范，目前阿里小程序体系提供的API达到了200+，很好的对移动端的UI、多媒体、文件缓存、网络、设备能力、数据安全以及业务相关能力进行了封装，让业务开发者在小程序侧针对API进行系统能力调用，无需关心平台实现。 因此 AliFlutter 容器接下来的规划就是从工程体系的角度，提供一套标准化的 API 能力，以规范并抽象移动端的端基础能力，使业务尽量少甚至不关心平台差异性，专注于业务；同时借助标准化 API 的能力，实现跨多端多平台部署。

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="460" data-default-watermark-src="https://pic3.zhimg.com/50/v2-1b80877e8a84625770a99e349024bae3_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic3.zhimg.com/v2-4bc1a521573f0368b2986438a3be988a_r.jpg?source=1940ef5c" data-actualsrc="https://pic1.zhimg.com/50/v2-4bc1a521573f0368b2986438a3be988a_hd.jpg?source=1940ef5c">

从移动端架构角度看，各个时期的跨平台方案都对 API 能力有着共同的诉求，从 H5 到 Weex ，再到后面的小程序，以及 Flutter 等容器环境，进行了多轮的 API 重复建设，造成了缺少 API 接口的标准化定义，以及缺少实现层统一管控的现状。如果能够在 API 的 native 实现上做到接口统一，再通过各个容器分别提供接口供业务使用，可以更好的做到实现收口，并在统一实现层跨容器实现对系统资源的统一调度、管控和度量。

### ▐ 提升交互能力：UI + 游戏引擎

前文提到过，Flutter 目前最大的价值在于研发效率的提升，这是吸引业务团队应用Flutter技术的起点；但仅仅依靠研发提效还远远不够，当通过各种工程化手段解决好当前研发痛点，提升研发效率之后，如何说服业务继续使用Flutter体系进行业务开发？Flutter带来的长远价值在哪里？个人认为，这个落脚点应该在通过游戏交互能力的泛化，打破 UI 与游戏引擎的边界，用游戏化的方式创造更有表现力的交互体验，创造新的业务玩法和价值。 大家知道传统的 UI 和游戏引擎是相互独立的两个体系，在 H5 应用中，往往是通过 DOM 或者上层应用框架做 UI，通过建立在 canvas 上的 H5 游戏引擎实现游戏能力。

如果在游戏应用中有 UI 的需求，解决方案一般是自建一套简单的 UI 体系与事件体系，通过自绘的方式在游戏中叠加 UI ，独立游戏引擎亦是如此。Flutter 从技术原理上看更像是一个建立在 Skia 图形库上的游戏引擎，它通过细粒度的 widgets 设计向上构建 UI 系统；同样得益于这样的细粒度设计，我们也完全可以直接通过 widgets 能力组合出一个完整的游戏引擎，提供Game，Scene 及 Sprite 动效等 widgets 并扩展对应的 elements 和 render objects，并与 UI 体系共用一套事件处理机制、分层与渲染合成机制。

这样做就相当于打破了原来H5中DOM UI和Canvas游戏的边界，让两个体系在 widgets 概念下完美融合起来，通过游戏引擎的能力赋能UI实现更多以前UI体系难以低成本实现的动效效果（比如一只小盒马一口吃掉了一个订单组件等等）。我们相信，这个方向的探索将会进一步释放 Flutter 的技术潜力，带来更多的业务可玩性与创造性，解放产品和设计的想象力，为业务创造更多价值。

### ▐ 提升研发效率：工程解耦与端云一体化

### **Flutter 工程解耦**

前端体系的研发效率很大程度上来自于基于 URI 的统一路由体系带来的页面间解耦性，与页面内基于 Web API 的标准化带来的内聚性。然而目前的 Flutter 研发模式，仍需要多个业务团队工作在同一个工程下，互相之间存在源码依赖，未来如果跨业务团队大规模应用Flutter技术，必将拖慢业务的研发效率。 从工程解耦角度看，目前 AliFlutter 容器通过混合栈与标准路由能力基本实现了页面研发的解耦，未来的容器化建设通过提供小程序对等的 API 能力封装，业务对平台无感知，能够让我们有机会解耦业务研发，实现与小程序开发接近的研发体验和效率。

**理想的方案是：**业务可以从业务维度创建一个独立的 Dart 工程，只包含业务相关的页面和逻辑代码，通过 Flutter 的 Hot UI 开发页面，通过IDE提供的基于 Flutter Web 的能力本地预览工程并调试 API 与系统调用，完成研发期工作；也可生成预览二维码，使用预装有 AliFlutter SDK 环境的宿主应用扫码预览；研发与构建链路分离，云端主动拉取业务仓库代码参与整包构建。以此达到类似小程序研发方式的前端研发体验，同时实现业务间的研发解耦和并行发布，提高业务的交付效率。

### **端云一体化**

如今 Serverless 概念越来越多的受到业务研发的重视和应用，集团在新一代的端云一体化研发模式上的探索这一年多来也做的如火如荼。结合轻量级容器环境、多语言支持能力与统一的 API 服务端编程，端侧同学可以很容易的使用客户端语言如 Java、JS、Swift 甚至 Dart 来开发服务端业务能力，实现服务编排、服务端 FaaS 业务逻辑与 API 自动生成，达到前后端工程体系归一，业务研发闭环的效果。

目前闲鱼在 Dart FaaS 云端一体化的探索走在了前面，通过集团的容器规范实现了Dart function容器，并联合服务端为部分业务需要的领域服务抽象出来 BaaS 层（存储、消息队列等），并封装了面向前端的 BFF（Backend for Frontend）能力层，使移动端开发者可以很容易的使用Dart封装FaaS业务逻辑，同时进行移动端和服务端 FaaS 开发，大大提高了业务研发效率。通过将原有的端侧请求接口、组装数据并转换为 ViewModel 的逻辑都后移到了服务端，经过字段映射与页面编排，移动端可直接获取 ViewModel 并刷新页面，通过 BinderAction 双向交互状态数据，有效屏蔽了通信细节，提高了开发效率。

云端一体化除了带来了研发与协同效率的提升，同时也重塑了生产关系，使端侧业务从只关注端侧体验和逻辑的开发角色，变成能够向业务整体结果负责；同时也让服务端更专注于领域服务的沉淀。Flutter 良好的跨端特性，能够屏蔽掉端差异化，配合 Flutter 容器化改造，更近一步的简化了业务的全链路研发模式。未来如何在 FaaS 模式下，沉淀出一套可以服务集团业务研发的通用端侧和服务端通信调度框架，让集团 Flutter 开发者和业务都能共享到 Serverless 技术和云端一体化提效的红利，是需要我们共同去探索和定义的新问题。

### ▐ 提升交付效率：Flutter 动态化

实现动态化是交付效率提升的重要方式。对于电商强运营强时效性特性来说，动态化几乎是一个必备的诉求，但从技术上看也是一个非常敏感的需求，是一个在系统厂商平台管控下长期博弈的过程。在我看来，动态化技术需要解决的核心问题，是在保证业务发布确定性的前提下，寻求技术性能、业务迭代效率与灵活性三者之间合理的平衡点。

下面讲讲我们在 Flutter 动态化上的两个思路与尝试：**Flutter 模板化方案与 Web on Flutter。Flutter 模板化方案**动态模板化方案是集团内较为成熟的一套基于Native技术的模板化方案，专注于 UI 模板渲染，没有执行逻辑和运行时环境，目前被广泛应用于电商系的一些核心业务场景。同时该方案提供了配套的组件平台，支持在线模板编辑、预览、测试及发布整套流程，结合发布平台形成了一整套完善的业务开发生态闭环。 在 Flutter 体系下，目前闲鱼团队依据标准模板协议在 Flutter 侧实现了一套 Dart 版 SDK ，通过模板下发实现了Flutter端的轻量级动态化组件编排能力；并通过一年多的迭代逐步解决了渲染性能与渲染一致性问题，较好的赋能了Flutter业务的组件动态化能力。

那么，未来 Flutter 与动态模板化方案有没有更好的结合点？答案是肯定的。从 DSL 角度看，目前模板的写法基本上来自 Android XML ，对组件开发者尤其是非 Android 开发者不够友好，具备一定的学习成本；而 Flutter 的结构与属性均可通过 widgets 表达，可以极为灵活且平台中立的用声明式代码构建UI并绑定数据，易于开发者编写组件并通过 Flutter 框架独立调试与测试；在移动端运行时，可以按需按场景翻译成 native 组件或 Flutter 组件。未来我们也将持续在这个方向上做探索。

### **Web on Flutter**

相比贴近 Native 研发模式的模板组件化渲染方案，Web on Flutter 希望通过类 H5 的 DSL + JS ，借助Flutter的渲染能力，实现贴前端技术栈的动态化能力。 目前基于 Web 渲染的小程序方案存在启动耗时高，渲染性能距原生 UI 有较大差距等性能问题，这些问题很大程度上都源自于浏览器引擎的设计历史包袱（渲染管线复杂、CSS multi-pass layout及legacy实现等），以及JS到Native通信效率低（bridge）。

Flutter 的设计思路源自浏览器，一方面直接吸收了前端框架近年来的演进成就，原生支持了声明式-响应式编程范式，提高了移动端的研发效率；另一方面，Flutter 紧贴 native 开发模式有限定义了 UI 结构、布局与渲染的必要元素，在满足native UI开发模式的前提下简化了能力定义与布局算法（single-pass layout与repaint boundary等概念），很大程度上简化了渲染管线的复杂度，直接为Flutter带来了接近原生的性能体验。

同时，Flutter 的 widgets 设计巧妙，结构布局属性等基础元素均使用 widgets 表达，且可通过基础 widgets 的组合来构成复杂组件，这种细粒度+组合能力设计让 Flutter 有极强的表现力，并具备向上对接各种研发模式的可能性。 因此，通过 widgets 组合小程序 DSL，支持小程序 CSS 有限集，实现渲染层替换浏览器引擎，并对接JS引擎支持JS执行能力，是一个将Flutter应用于小程序生态的合理探索方向。

相比把开发者惯坏了的浏览器，这种方案在 CSS 的能力支持上必然是受限的，无法满足所有 CSS3 标准的实现，更多通过紧贴 Flutter widgets 的现有能力以及必要的 widgets 扩展，在不破坏 single-pass layout 的前提下组合出 CSS 能力。但从 Flutter 原生开发的角度看，只要 Flutter 现有的原生能力能够满足业务需求，那么受限的 CSS 实现也一样可以提供和 Flutter 对等的能力解决业务问题。同时，通过受限的 CSS 可以换来与 Flutter 相当的高性能，与基于 Web 的实现相比，在性能上带来了质变。

" data-caption="" data-size="normal" data-rawwidth="1080" data-rawheight="521" data-default-watermark-src="https://pic2.zhimg.com/50/v2-1bc8732e3ea41f09b5c8d9e904832f19_hd.jpg?source=1940ef5c" class="origin_image zh-lightbox-thumb lazy" width="1080" data-original="https://pic3.zhimg.com/v2-89fc4ee6b21ebebbeccd84ce4352a349_r.jpg?source=1940ef5c" data-actualsrc="https://pic2.zhimg.com/50/v2-89fc4ee6b21ebebbeccd84ce4352a349_hd.jpg?source=1940ef5c">

我们在18年底通过一个内部项目实现了这个思路的原型，通过使用 C++ 重写 Flutter 的 widgets、rendering、painting 及事件管理等 Dart framework 中的中低层能力，并在 widget 上用 C++ 实现了 CSSOM + DSL -> Widgets 的响应式框架，直接从 C++ 层提供 render 实现，将传统由 JS 承担的模板展开、tree-diff计算与渲染工作交给C++层，通过Flutter提供的Widgets tree到RenderObjects tree的diff能力实现，显著提高了性能。

从实现的简单的demo看，相对小程序的web渲染性能有了大幅的提升。这种方案的问题在于和Google代码库分裂后的长期维护性。<u>[“Flutter和Web生态如何对接”](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s%3F__biz%3DMzAxNDEwNjk5OQ%3D%3D%26mid%3D2650405725%26idx%3D1%26sn%3D0b7476f7c7c01df7fdafda578f9ceb98%26scene%3D21%23wechat_redirect)</u>这篇文章对集团内在这个方向上尝试的几种思路做了较为全面的对比，未来我们也将继续在这个方向上做深入和持续的探索。

## 
**总结与展望**

Flutter 体系化建设目前在淘系刚刚起步，仍然有大量工作需要去做，我们在基础设施、工程化以及通过Flutter定义和收敛业务域研发模式上做的许多建设性的事情，正朝着把Flutter打造为统一移动应用基础研发框架，助力业务回归移动端研发模式这个大目标一点点迈进。 在移动技术小组启动 AliFlutter 项目之前，闲鱼技术部已经在 Flutter 技术建设上做了大量探索和投入。

一方面通过 Flutter 技术赋能业务提效升级，拿到了很好的业务成绩；另一方面沉淀Flutter的技术与业务解决方案，并通过开源反哺社区，在海内外Flutter技术社区中建立了显著的技术影响力与领导力，也涌现出一众Flutter技术专家。 接下来AliFlutter的重点任务，就是要和闲鱼、财富等先驱应用者以及盒马、钉钉、飞猪、优酷、饿了么、CBU等Flutter的实践者一起，在集团层面把Flutter的场子建起来，把集团Flutter生态拉起来，让技术和经验能够共同沉淀和分享，一起来把Flutter技术体系在阿里的应用生态内做大做强，真正成为集团业务的核心研发模式，并让每个参与者都能从中受益。

**我们一直坚信 Flutter 技术的先进性和应用前景，未来我们将继续立足淘系服务集团业务，和集团开发者携手前行，在 Flutter 这个技术方向上坚定的走下去。**

——————————————————————————————————

本账号主体为阿里巴巴淘系技术，淘系技术部隶属于阿里巴巴新零售技术事业群，旗下包含淘宝技术、天猫技术、农村淘宝技术、闲鱼、躺平等团队和业务，是一支是具有商业和技术双重基因的螺旋体。

刚刚入驻知乎，将会给大家带来超多干货分享，立体化输出我们对于技术和商业的思考与见解。

详情介绍可以看这里 [阿里巴巴淘系技术介绍](https://zshipu.com/t?url=https://zhuanlan.zhihu.com/p/141070026)

欢迎收藏点赞关注我们！共同进步~ ：） > 作者：阿里巴巴淘系技术
