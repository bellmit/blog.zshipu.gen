
title: Git技术：Git 流以及正确维护历史记录
author: 知识铺
date: 2020-09-28 21:39:40
tags: 
---
 如何使用git和选择每个项目的最佳方法。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--gsdWZ81J--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6l8p92eh4fs48rpkhdlr.jpg)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--gsdWZ81J--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/6l8p92eh4fs48rpkhdlr.jpg)

维护历史记录时，请尝试遵循以下两条规则：

1.  主分支应仅包含逻辑完成的提交，例如，任务 A 已完成或 Bug B 已修复。

2.  历史不应是分支的，并且与许多合并提交混淆。换句话说，最好使用重基而不是合并。

离散窗体的历史记录（在逻辑上完成每个提交时）允许您更快地工作并在将来解决问题。例如，您需要在一段时间后执行与任务"A"相同的任务，或者发现添加此任务后，一些工作方式不正确。您可以轻松地在一次提交中查看所有更改的文件，或签出到此提交以测试此逻辑是否不再在项目中，或者是否已更改。此外，在 git 中，还有一种模式可帮助您使用 git 二分项搜索 Bug。它帮助开发人员在出现 Bug 的给定范围内查找提交。如果您有很多中间提交，或者更糟的是，如果您的提交包含未编译的代码，则很难使用，并且开发过程将至少慢 20%。

重基而不是合并更好，让我来说明一下。例如，我在开发分支工作一段时间，我完成了 3 个任务（f1、f2、f3），我的同事 Alex 也完成了 3 次任务（c1、c2、c3）。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--Cmu4SFhj--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/smb8ou7tr8uv2tp1hl6g.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--Cmu4SFhj--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/smb8ou7tr8uv2tp1hl6g.png)

然后，有必要将我们所有的更改放在一起，我们决定使用合并。如果我们将我的分支合并到开发人员中，然后使用 Alex 的分支进行，那么我们得到的就是：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--tb7u5hgB--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/vzcqpq4odylgw2ofdvzf.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--tb7u5hgB--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/vzcqpq4odylgw2ofdvzf.png)

以上是只有两个开发人员提交的结果，因此很难想象当 3-4 个人在项目上工作，并且每个开发人员在每个分支中执行多个提交时会发生什么。显然，在这种情况下，你的历史将更混乱。

如果使用 rebase 并一个个地将所有分支加起来，则获得以下结果：

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--EY8_8jKn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/9apy4fo2fx9oq9fomapi.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--EY8_8jKn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/9apy4fo2fx9oq9fomapi.png)

但是，只有仅对只有 1-2 个提交进行重新基础的分支，或者如果您知道与开发中已有的代码没有很多冲突，则这才方便。由于 rebase 应用了一个又一个提交，因此存在以下情况：您可以解决第一个提交之一的冲突，然后在以下提交中，您与使用的同一文件发生冲突，因此，您自行解决代码的冲突非常不方便且非常耗时。您可能认为在这种情况下，最好使用合并。这个问题是有争议的，取决于您的分支中存在什么样的提交。如果他们是大，你工作他们每个人约一个星期，那么是的，但如果他们都涉及到一些任务，那么最好是通过从这个分支进行一个提交，然后重新基地这个提交到开发。

问题是，什么是最好的选择，修改或重置您的提交，然后上传任务到开发与1-2提交，或作出大量的提交，然后挤压。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--_MDBtQ6i--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fokzbq0qif005tg6gbpj.jpg)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--_MDBtQ6i--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fokzbq0qif005tg6gbpj.jpg)

这取决于您的选择和项目的要求。事实是，您的团队领导或客户可以要求每日提交，即使代码不稳定，以便监视您的进度。在这种情况下，你别无选择，只能做壁球。

为了说明，我将创建一个分支 f4，并在它中进行 4 个每日提交，从我们开始的位置创建一个临时分支 f4_temp，它将为我替换远程源/f4，如果我使用远程存储库，我会创建它。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--zPiSTQoy--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fohcw4pf532ms5frg8ju.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--zPiSTQoy--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/fohcw4pf532ms5frg8ju.png)

然后压缩提交和重新基点。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--RdkxhRez--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/08h23hw21kmzw0naxdas.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--RdkxhRez--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/08h23hw21kmzw0naxdas.png)

现在，f4 分支具有与 f4_temp 相同的更改，如果转到提交设置，则可以看到注释也已保存。
但是，如果要将任务拆分为多个提交，会怎么样？例如，如果您已创建与任务相关的内部逻辑，则您希望它位于单独的提交中，但尚未完成上载到开发人员，因为还需要完成 UI。例如，f4 分支是内部逻辑，正如您所看到的，我还没有将其上载到开发人员中，我们根据相同的原则重复所有内容，创建 f4_ui 分支，并进行 3 次提交。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--dOVbtdQM--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/brud0h2w5kzua9ax4tqn.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--dOVbtdQM--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/brud0h2w5kzua9ax4tqn.png)

现在，我们挤压，上传到开发，并保留f4_ui_temp（源）分支的团队领导，它始终可以删除以后。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--7LvAK0G---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/2zqjtha1yyc3yuyq972h.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--7LvAK0G---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/2zqjtha1yyc3yuyq972h.png)


