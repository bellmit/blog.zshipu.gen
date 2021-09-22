
---
title: Monorepo：Monorepo 是什么，为什么大家都在用
author: 知识铺
date: 2020-11-01 12:53:27+08:00
tags: [Monorepo]
---
## Monorepo 是什么，为什么大家都在用？

Dan Luu 很早很早就写了篇[文章](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//danluu.com/monorepo/)，给大家介绍 monorepo 。在我之前那篇[推荐 Buck / Bazel 的文章](https://zshipu.com/t?url=https://zhuanlan.zhihu.com/p/53287816)之后就想讲讲 monorepo，结果一直没来得及写。

Monorepo 的概念要和互联网公司里怎样训练新人上手一起讲。很多公司要花超过半个月的时间才能让新人开始动手干活，并不是内部系统要学的东西很多，只是因为有很多的部落知识（Tribe Knowledge）并没有写下来，需要手把手地教。其中一项，就是怎么把项目的所有依赖从网上拉下来，配置好开发环境，可以干活。之后，还要教为什么提交的修改不应该包含一些配置修改之类的，或者为什么要用祖传数年前的依赖版本。

这些如果用 monorepo 的话都不是问题。

Monorepo 简单的说，是指将公司的所有代码放到一个 Git / Mercurial / Subversion 的代码仓库中。对于很多没听说过这个概念的人而言，无异于天方夜谭。Git 仓库不应该是每个项目一个吗？对于很多用 monorepo 的公司，他们的 Git 仓库中不止有自己的代码，还包括了很多的依赖。基本上，只要把 monorepo 用 Git 拖下来，跑一下 ```./scripts/install```，就可以直接用 Buck / Bazel （在安装脚本中就装到了本地）编译仓库中的所有项目，并且提交修改（安装脚本配置好了代码提交环境，如果用的 Phabricator 的话，Gerrit 不用）。

## 所有项目在一起？

Monorepo 的核心观点是所有的项目在一个代码仓库中。这并不是说代码没有组织都放在 ```./src``` 文件夹里面。相反，通过使用 Buck / Bazel，monorepo 中的代码都是分割到一个个小的模块中的。比如一个普通的互联网公司，代码仓库的构架可能是这样的：

 <code class="language-text">./frontend/web/vendors
./frontend/web/vendors/vue.js
./frontend/web/ui/registration
./frontend/web/ui/login
./frontend/ios/apps/app1
./frontend/ios/vendors/yoga
./frontend/ios/features/authentication
./frontend/ios/libraries/network
./frontend/android/apps/app1
./frontend/android/vendors/sqldelight
./shared/protobuf_schema
./backend/vendors/envoy_proxy
./backend/messaging/gateway
....</code>

这样的分割，每个人大部分时间其实仍然只是工作在少数的几个文件夹以内的，并不会导致一个 IDE 打不开太大的项目之类的事情。但是很多事情就简单了很多。

比如编译。在这样的一个代码仓库中，所有的依赖都已经在仓库里了，用 ```bazel run``` 就可以执行任意的一个项目，不需要多余的配置。大大加快了开发的速度。

比如要修改前端和后端的通信协议，只需要一个 commit 就可以把 protobuf 改掉，同时把使用 protobuf 的后端和三个前端的代码一起改了。

## 编译时间很慢？

在很多小公司，许多别的组的项目提供的是一个二进制包或者 jar，然后再用来链接到最终的发行文件里。似乎这样编译速度快了。但因为在生成最终发行文件的时候系统已经不知道具体的依赖变化了，编译系统很难将中间结果给缓存住。相比而言，无论是 Buck 还是 Bazel 都提供了完整的基于输入的缓存系统，可以更有效的缓存中间结果，提升编译速度。

## 怎么发布新版本的库？

在传统的多项目多代码仓库的公司，每个代码仓库都有自己的发布规则，比如每周发布一个新的版本，再让依赖它们的其他项目在新版本发布后慢慢升级。似乎一顿操作猛如虎地忙，但是搞了一个半月，只是把一个函数加了个参数罢了。在 monorepo 中，这种假工作是不存在的。因为所有人用的都是公司里别人最新的库，完全不存在版本升级的问题。需要修改函数参数的话，只需要一个新的 commit 就能解决了。

## 其他的好处？

如果一开始做项目的时候就知道项目的范围有多大，应该怎么划分模块，而且几十年不变的话，自然是好的。但是除了开源项目，很多公司内部的项目是决定不了这些的。开源项目做了错误的选择就死了。而公司内部的项目基本上就是发布出去了慢慢迭代慢慢改直到满意。在这种时候，将一段代码从一个功能移动到另一个功能去，是很常见的需求。这个时候如果代码是在好几个仓库中的话，就将一天的工作一下变成了一个月的工作，给自己找了很多麻烦。

## 还有什么？

前面吹的这么好，其实还是有一些需要说明的。比如：因为 monorepo 将大部分的依赖都放到了代码仓库中，所以需要有能够部分维护这些第三方依赖的能力。如果不改的话还是很方便的，但是很多时候 monorepo 用太爽了大家也忍不住顺手把第三方依赖的 bug 给先修了，再报修复给开源的版本。这个时候要升级第三方依赖就会麻烦一点，最好是有一套自己的管理方案。

有的公司对一些核心代码需要有读权限的限制，开源的代码仓库管理软件比如 Git 和 Mercurial 对此是不支持的。这时候把那部分代码移到一个 git-submodule 或者 subrepository 里面也是可以的解决方案。submodule / subrepository 大家捏着鼻子也是可以用的。

因为所有人的 commit 在 monorepo 里都在一个线性历史里面，所以很嘈杂。比如要二分找一个导致网页出错的 bug 需要搜索的版本可能就不必要的多。这种时候用 Buck / Bazel 的优势就体现出来了，可以很方便的确定某个 commit 对于某个功能是不是真的有影响，不是的话可以直接跳过。

我吹了这么多，其实最后还是回到 [Dan Luu 的文章](https://zshipu.com/t?url=https://link.zhihu.com/?target=https%3A//danluu.com/monorepo/)大家去读读，解释了很多细节。

顺便一说，担心 Git 或者 Mercurial 管理不过来贵司代码量的可能大部分时候都多虑了，几十上百个 GiB 的仓库还是可以的，再说了，大文件也不放在里面，都是用的 Git LFS 对吧。


