
---
title: NPM起步：将私有 NPM 包发布到 Nexus
author: 知识铺
date: 2020-10-30 18:15:02+08:00
tags: [npm]
---
<font _mstmutation="1" _msthash="29198" _msttexthash="4060932785">我们都在项目上工作，这让我们有机会构建可重用的组件。大多数时候，这些组件最终出现在项目的文件夹中。然后，此文件夹被复制粘贴到多个项目中，随着时间的推移，这成为更新的噩梦，因为我们不能轻易地拥有多个版本的组件，并且在多个分支上维护相同的代码库，因为版本是解决这个问题的一种棘手解决方案。</font>```shared```

<font _mstmutation="1" _msthash="27573" _msttexthash="3268690139">在这篇文章中，我们将看看Nexus存储库管理器（即Nexus），这是一个开源存储库管理器提供的[Synatype](https://zshipu.com/t?url=https://www.sonatype.com/)。我们将讨论如何创建专用存储库（由 Amazon S3 支持），并将它与公共 NPM 注册表相结合，以提供一个全面的解决方案，使我们的私有存储库保持私有性、允许版本控制和缓存存储库。</font>

<font _mstmutation="1" _msthash="39793" _msttexthash="750570808">接近尾声时，我们将创建两个应用程序，其中一个将被推送到 Nexus，另一个将从 Nexus 使用。在整篇文章中，我们将只处理本地部署的 Nexus。</font>

# <font _mstmutation="1" _msthash="27846" _msttexthash="13489840">评估需求</font>

<font _mstmutation="1" _msthash="28145" _msttexthash="4569750471">在我们进入细节之前，值得考虑需要像 Nexus 和 npmjs 提供的专用存储库（价格）。就我个人而言，我认为，如果您的组织没有任何云基础架构，在 npmjs 上托管的存储库是一个更简单、更简洁的解决方案。托管 Nexus、定期备份、运行状况检查都是开销（如果尚未内置于云基础结构中）。现在让我们假设，这一切都已经到位，并继续下去。</font>

# <font _mstmutation="1" _msthash="34424" _msttexthash="12949508">目录：</font>

1.  <font _mstmutation="1" _msthash="34879" _msttexthash="55905447">在本地运行 Nexus 存储库管理器</font>
2.  <font _mstmutation="1" _msthash="27885" _msttexthash="8000317">了解卷</font>
3.  <font _mstmutation="1" _msthash="33787" _msttexthash="4494308">创建 Blob</font>
4.  <font _mstmutation="1" _msthash="34788" _msttexthash="22158006">创建托管存储库</font>
5.  <font _mstmutation="1" _msthash="34138" _msttexthash="22909328">创建 NPM 代理和组</font>
6.  <font _mstmutation="1" _msthash="37518" _msttexthash="48109451">将二进制文件推送到连结</font>
7.  <font _mstmutation="1" _msthash="27495" _msttexthash="42904511">从 Nexus 中拉出二进制文件</font>
8.  <font _mstmutation="1" _msthash="32682" _msttexthash="6674577">结论</font>

# <font _mstmutation="1" _msthash="33605" _msttexthash="55905447">在本地运行 Nexus 存储库管理器</font>

<font _mstmutation="1" _msthash="33592" _msttexthash="1313879645">由于 Docker 的日益普及，现在运行任何软件都像找到正确的（Docker）映像一样简单。幸运的是，Sonatype 为 Nexus 提供了 Docker 映像，可以使用以下拉取命令轻松地在本地提取该映像。</font>

docker pull sonatype/nexus

<font _mstmutation="1" _msthash="27066" _msttexthash="122115786">拔出图像后。要运行，只需执行以下命令：</font>

docker run --rm -it -p 8081:8081/tcp sonatype/nexus3:latest

<font _mstmutation="1" _msthash="28197" _msttexthash="362459201">这将启动运行我们 Nexus 实例的容器。要试用，请打开浏览器，并且，默认凭据为</font>```http://localhost:8081``````admin```/```admin123```

 ![Image for post](https://miro.medium.com/max/60/1*3Y0QrPONIXboQsDHjDCh9g.png?q=20)

![Image for post](https://miro.medium.com/max/2880/1*3Y0QrPONIXboQsDHjDCh9g.png)

<noscript>![Image for post](https://miro.medium.com/max/5760/1*3Y0QrPONIXboQsDHjDCh9g.png)</noscript>

<font _mstmutation="1" _msthash="23192" _msttexthash="987338898">Nexus 中有很多不同的功能。此时，我们将仅处理为 NPM 设置专用存储库所需的资源，但这些概念也可以轻松地应用于其他形式的项目（maven、NuGet、Docker 等）。</font>

## <font _mstmutation="1" _msthash="33852" _msttexthash="11149970">基本概念</font>

<font _mstmutation="1" _msthash="33696" _msttexthash="388316812">Nexus 公开存储库，它是我们的存储库（即 Nexus 术语中的存储库）和公共 NPM 注册表的组合。</font>```group``````private``````hosted``````proxy```

<font _mstmutation="1" _msthash="39975" _msttexthash="1411254065">代理到公共注册表是必要的，因为我们仍然需要一种从 NPM 注册表访问所有公开可用的存储库的方法。每当我们使用这些公共包时，它们都会缓存在代理中，我们将在文章末尾看到这些代理。</font>

<font _mstmutation="1" _msthash="29939" _msttexthash="1914037788">因此，当我们想要安装新的私有或公共 NPM 包时，我们将项目注册表指向 （使用 ），以便它可以安装任何必要的包（使用 或 ）。并且，若要创建或更新现有存储库，请将发布操作指向存储库（使用 中的选项）。</font>```group``````.npmrc``````npm``````yarn``````hosted``````publishConfig``````package.json```

<font _mstmutation="1" _msthash="33657" _msttexthash="374154196">这就是为什么我们看到一组默认的组/托管/代理存储库组合为我们创建时，我们首次加载 Nexus。</font>

> <font _mstmutation="1" _msthash="44421" _msttexthash="100006296">组 = 托管 = 代理。从组读取并写入托管存储库</font>

 ![Image for post](https://miro.medium.com/max/60/1*YS1cCeoBxj8GLXMyPtz3vA.png?q=20)

![Image for post](https://miro.medium.com/max/2880/1*YS1cCeoBxj8GLXMyPtz3vA.png)

<noscript>![Image for post](https://miro.medium.com/max/5760/1*YS1cCeoBxj8GLXMyPtz3vA.png)</noscript>

## <font _mstmutation="1" _msthash="28015" _msttexthash="12908337">用户管理</font>

<font _mstmutation="1" _msthash="26650" _msttexthash="4725700434">引导 Nexus 时，将为我们（以及所有使用 Nexus 的用户）创建默认用户。因此，全世界几乎每个 Nexus 用户都知道默认用户名和密码是什么。这就是为什么我们应该删除/禁用默认用户，一旦我们创建一个新的管理员用户。默认情况下，我们只有两个角色，但我们始终可以创建更多角色（这是特权的组合），并根据需要将它们添加到用户。</font>

 ![Image for post](https://miro.medium.com/max/60/1*LLfuKogG1_zkZ8B26Oen7w.png?q=20)

![Image for post](https://miro.medium.com/max/1930/1*LLfuKogG1_zkZ8B26Oen7w.png)

<noscript>![Image for post](https://miro.medium.com/max/3860/1*LLfuKogG1_zkZ8B26Oen7w.png)</noscript>

<font _mstmutation="1" _msthash="24609" _msttexthash="389658672">尽管这不是强制性的，但强烈建议创建自定义角色，并且仅根据用户需要将其分配给用户。</font>

 ![Image for post](https://miro.medium.com/max/60/1*uUtrF1iPCG6mY7JxKnJEHQ.png?q=20)

![Image for post](https://miro.medium.com/max/2880/1*uUtrF1iPCG6mY7JxKnJEHQ.png)

<noscript>![Image for post](https://miro.medium.com/max/5760/1*uUtrF1iPCG6mY7JxKnJEHQ.png)</noscript>

<font _mstmutation="1" _msthash="27847" _msttexthash="503194536">接下来，让我们防止未经授权的用户访问我们的服务器，点击下并取消选中允许访问服务器的选项：</font>```Anonymous``````Security```

 ![Image for post](https://miro.medium.com/max/60/1*hJQCMrkg8wpfXoR6BKdMpw.png?q=20)

![Image for post](https://miro.medium.com/max/1772/1*hJQCMrkg8wpfXoR6BKdMpw.png)

<noscript>![Image for post](https://miro.medium.com/max/3544/1*hJQCMrkg8wpfXoR6BKdMpw.png)</noscript>

<font _mstmutation="1" _msthash="33943" _msttexthash="428961195">现在，我们已创建了名为"新管理员"并阻止匿名用户访问我们的存储库，我们已准备好进入下一步。</font>```npmuser```

# <font _mstmutation="1" _msthash="35087" _msttexthash="8000317">了解卷</font>

<font _mstmutation="1" _msthash="34346" _msttexthash="3528558436">每当我们将 Docker 映像作为容器运行时，所附的所有信息都是无状态的，即如果我们的容器因任何原因重新启动，数据可能会丢失。例如，在我们的示例中，我们已经在 Nexus 中创建了一个管理员用户，如果我们重新启动容器，我们创建的用户在重新启动时将不可用，因为它是一个从头开始的全新的容器。</font>

<font _mstmutation="1" _msthash="32890" _msttexthash="1241575855">为了绕过此问题（以及其他类似的问题），Docker 允许将卷装载到它可以保存数据的容器。在重新启动的情况下，只要将新容器重新安装到与之前相同的卷，就可以保留信息。</font>

<font _mstmutation="1" _msthash="28548" _msttexthash="315464045">首先，让我们创建一个目录，我们将在此示例中放置与此示例生成的所有关系数据。</font>

mkdir nexus-data

<font _mstmutation="1" _msthash="27848" _msttexthash="471084991">这是我们将用作 Nexus 映像的临时卷的文件夹。现在，我们需要在发出容器的 run 命令时提供卷的路径：</font>

docker run --rm -it -p 8081:8081 **-v** **/Users/../../nexus-data:/nexus-data** sonatype/nexus3

<font _mstmutation="1" _msthash="22841" _msttexthash="1007159400">上面突出显示的部分是使所有差异，我们正在指定完整的路径到我们的目录，我们正在安装它到在 Nexus 容器中调用的默认数据目录。此处列出了其他属性和[配置](https://zshipu.com/t?url=https://hub.docker.com/r/sonatype/nexus3/#notes)。</font>```nexus-data``````nexus-data```

<font _mstmutation="1" _msthash="29536" _msttexthash="211233295">运行列出的命令后，我们会看到在创建的文件夹下创建的不同文件夹。</font>```nexus-data```

 ![Image for post](https://miro.medium.com/max/60/1*AKc8q-Y1XkTluXXLAscECQ.png?q=20)

![Image for post](https://miro.medium.com/max/1156/1*AKc8q-Y1XkTluXXLAscECQ.png)

<noscript>![Image for post](https://miro.medium.com/max/2312/1*AKc8q-Y1XkTluXXLAscECQ.png)</noscript>

<font _mstmutation="1" _msthash="28275" _msttexthash="1012972129">我们现在在 Nexus 中所做的任何和所有更改都会同步回此文件夹。如果您感到好奇，请再次创建 带角色，停止容器并重新启动它。新创建的用户将保留为预期。</font>```npmuser``````admin```

# <font _mstmutation="1" _msthash="43940" _msttexthash="4494308">创建 Blob</font>

<font _mstmutation="1" _msthash="33722" _msttexthash="2262333931">现在，我们已准备好创建 Blob 存储，这是一个逻辑分区，我们希望为不同的项目类型强制执行，即我们希望隔离 NPM 二进制文件和 maven 二进制文件，以避免任何冲突（名称或其他）。在内部，Nexus 只是为我们创建的每个 Blob 存储创建不同的文件夹。</font>

<font _mstmutation="1" _msthash="44005" _msttexthash="153809396">要创建 Blob，请转到"设置"页 > 存储库 > Blob 存储 > 创建 Blob 存储</font>

 ![Image for post](https://miro.medium.com/max/60/1*SnqJY8FSh-iXCRXbmkkuaw.png?q=20)

![Image for post](https://miro.medium.com/max/1886/1*SnqJY8FSh-iXCRXbmkkuaw.png)

<noscript>![Image for post](https://miro.medium.com/max/3772/1*SnqJY8FSh-iXCRXbmkkuaw.png)</noscript>

<font _mstmutation="1" _msthash="32123" _msttexthash="118770210">此 Blob 一旦创建，将在卷中如预期显示：</font>

 ![Image for post](https://miro.medium.com/max/60/1*gYu-1jXfkPwVSZyXAPHJIQ.png?q=20)

![Image for post](https://miro.medium.com/max/898/1*gYu-1jXfkPwVSZyXAPHJIQ.png)

<noscript>![Image for post](https://miro.medium.com/max/1796/1*gYu-1jXfkPwVSZyXAPHJIQ.png)</noscript>

<font _mstmutation="1" _msthash="23231" _msttexthash="223986204">我们现在上传到该 Blob 的任何包都会保留在与其关联的文件夹下的卷中。</font>

<font _mstmutation="1" _msthash="37804" _msttexthash="1266651893">我们还将使用基于 AWS S3 的 Blob，这是 Nexus 提供的基于文件的 Blob 的替代方法。要配置基于 S3 的 Blob，只需从下拉列表中选择 S3 并填写所需信息即可。相同的示例如下所示：</font>```Type```

 ![Image for post](https://miro.medium.com/max/60/1*MRnaxfJNTNRavhZJcj1CGg.png?q=20)

![Image for post](https://miro.medium.com/max/1906/1*MRnaxfJNTNRavhZJcj1CGg.png)

<noscript>![Image for post](https://miro.medium.com/max/3812/1*MRnaxfJNTNRavhZJcj1CGg.png)</noscript>

<font _mstmutation="1" _msthash="28639" _msttexthash="107024788">这最终在 S3 存储桶中创建一些默认文件：</font>

 ![Image for post](https://miro.medium.com/max/60/1*HcFgxU7uX75mGKoG8wdn5A.png?q=20)

![Image for post](https://miro.medium.com/max/2678/1*HcFgxU7uX75mGKoG8wdn5A.png)

<noscript>![Image for post](https://miro.medium.com/max/5356/1*HcFgxU7uX75mGKoG8wdn5A.png)</noscript>

<font _mstmutation="1" _msthash="29367" _msttexthash="1437032558">使用此 Blob 推送到存储库的任何和所有内容都将由 S3 更新和管理，但是，我们提供给 Nexus 的有关 S3 存储桶的配置仍保留在我们之前装载的卷上。这就是为什么确保我们有卷的定期备份很重要。</font>

<font _mstmutation="1" _msthash="34333" _msttexthash="117599937">出于多种原因，我们希望减少对卷的依赖：</font>

1.  <font _mstmutation="1" _msthash="28158" _msttexthash="1748373861">在生产群集中，我们必须继续备份与灾难恢复 （DR） 容器连接的卷。虽然这不能完全避免（因为我们需要持久化用户、自定义角色和其他有状态信息），但我们可以将备份减少为无法与云（如 S3）同步的备份。</font>
2.  <font _mstmutation="1" _msthash="37869" _msttexthash="409242041">备份到 S3 允许我们在 AWS S3 存储桶上添加其他规则，如果需要，可以将旧软件包移动到冷存储。</font>

<font _mstmutation="1" _msthash="24167" _msttexthash="179761764">有了这个，我们就可以进入流程的下一阶段，创建存储库。</font>

# <font _mstmutation="1" _msthash="34398" _msttexthash="22158006">创建托管存储库</font>

<font _mstmutation="1" _msthash="28640" _msttexthash="1273209340">如前所述，托管存储库是我们为保存私有包而创建的私人存储库。使这些存储库具有私有性，是无法在没有 的情况下读取这些存储库的内容。我们将在文章末尾的一个示例中看到这一点。</font>```authToken```

<font _mstmutation="1" _msthash="27469" _msttexthash="210845492">若要创建托管存储库，请转到"设置"页 > 存储库 > 存储库 > 创建存储库。</font>

<font _mstmutation="1" _msthash="27612" _msttexthash="1060471282">当我们单击创建存储库时，Nexus 非常亲切，可以向我们提供配方，这些配方定义了需要配置特定类型的存储库，在我们的案例中，我们只关心相关的配方。</font>```npm```

 ![Image for post](https://miro.medium.com/max/60/1*vx-e2X_c9AFKZd3hv_oh9g.png?q=20)

![Image for post](https://miro.medium.com/max/2874/1*vx-e2X_c9AFKZd3hv_oh9g.png)

<noscript>![Image for post](https://miro.medium.com/max/5748/1*vx-e2X_c9AFKZd3hv_oh9g.png)</noscript>

<font _mstmutation="1" _msthash="39455" _msttexthash="1089986404">让我们首先选择选项，因为这就是我们想要开始。它要求我们提供两件事情，托管存储库的名称和需要为该存储库保存数据的 Blob。单击"创建存储库"按钮完成存储库的创建。</font>```npm(hosted)```

 ![Image for post](https://miro.medium.com/max/60/1*irUx2wE6gJ8sMNcCvzYFgw.png?q=20)

![Image for post](https://miro.medium.com/max/2198/1*irUx2wE6gJ8sMNcCvzYFgw.png)

<noscript>![Image for post](https://miro.medium.com/max/4396/1*irUx2wE6gJ8sMNcCvzYFgw.png)</noscript>

<font _mstmutation="1" _msthash="28743" _msttexthash="212504877">就是这个我们已为我们所有的项目创建了专用（托管）存储库。</font>```npm```

# <font _mstmutation="1" _msthash="39182" _msttexthash="22909328">创建 NPM 代理和组</font>

<font _mstmutation="1" _msthash="38649" _msttexthash="976576237">现在，我们已设置了专用存储库，我们已准备好创建 npm 代理，该代理将我们所有的读取请求代理到公共 NPM 注册表。我们可以通过将 和 存储库合并为 来完成更改。</font>```hosted``````proxy``````group```

## <font _mstmutation="1" _msthash="23699" _msttexthash="21322119">创建代理存储库</font>

<font _mstmutation="1" _msthash="33059" _msttexthash="359033116">在创建存储库屏幕中，选择哪个将我们带到配置页，我们希望代理到位于 URL 的 NPM 公共注册表[。](https://zshipu.com/t?url=https://registry.npmjs.org.)</font>```npm (proxy)``````[https://registry.npmjs.org](https://zshipu.com/t?url=https://registry.npmjs.org.)```

<font _mstmutation="1" _msthash="34541" _msttexthash="72795840">我们仅在此处输入 3 个必填字段：</font>

1.  <font _mstmutation="1" _msthash="22997" _msttexthash="5219019">名称 |</font>```npm-proxy```
2.  <font _mstmutation="1" _msthash="38220" _msttexthash="11560562">代理位置 |</font>```[https://registry.npmjs.org](https://zshipu.com/t?url=https://registry.npmjs.org.)```
3.  <font _mstmutation="1" _msthash="27131" _msttexthash="182524043">Blob 存储（用于缓存存储、配置等） = （之前创建）</font>```NPM-S3```

<font _mstmutation="1" _msthash="33124" _msttexthash="33929844">这将创建代理存储库。</font>

 ![Image for post](https://miro.medium.com/max/60/1*C7kqOjCvIbPE0KILqyQy7g.png?q=20)

![Image for post](https://miro.medium.com/max/2868/1*C7kqOjCvIbPE0KILqyQy7g.png)

<noscript>![Image for post](https://miro.medium.com/max/5736/1*C7kqOjCvIbPE0KILqyQy7g.png)</noscript>

## <font _mstmutation="1" _msthash="23855" _msttexthash="18007769">创建组存储库</font>

<font _mstmutation="1" _msthash="26416" _msttexthash="630719167">如前所述，创建组存储库是将托管存储库和代理存储库组合在一起，这样可以使读取更加容易。让我们创建类似于 和 的存储库。</font>```npm (group)``````hosted``````proxy```

<font _mstmutation="1" _msthash="33566" _msttexthash="459162730">这接受与之前类似的配置，如名称、Blob 存储等。我们正在选择 和 存储库，并使其成为此组的活动成员。</font>```npm-private``````npm-proxy```

<font _mstmutation="1" _msthash="29185" _msttexthash="441830779">将来，如果我们有更多的兼容存储库，它们将显示在列表下，可以选择这些存储库并移动到该部分。</font>```Available``````Members```

 ![Image for post](https://miro.medium.com/max/60/1*v5grwfOhbboTA8Wz08bmFw.png?q=20)

![Image for post](https://miro.medium.com/max/1956/1*v5grwfOhbboTA8Wz08bmFw.png)

<noscript>![Image for post](https://miro.medium.com/max/3912/1*v5grwfOhbboTA8Wz08bmFw.png)</noscript>

# <font _mstmutation="1" _msthash="33969" _msttexthash="48109451">将二进制文件推送到连结</font>

<font _mstmutation="1" _msthash="33371" _msttexthash="1158496157">现在，我们已经准备好必要的存储库了，现在我们可以根据需要在项目中使用这些存储库。让我们首先创建一个包含空白文件的示例 NodeJS 项目，然后推送到托管存储库：</font>```index.js```

mkdir npm-app1 && cd npm-app1npm init -ytouch index.js

<font _mstmutation="1" _msthash="27482" _msttexthash="226108961">要发布此项目，我们需要更新文件，其中指向我们新的托管存储库。</font>```package.json``````publishConfig```

<font _mstmutation="1" _msthash="27677" _msttexthash="505080914">如果我们现在尝试使用 命令发布项目，我们会看到以下错误，如预期的那样说我们需要身份验证：</font>```npm publish```

 ![Image for post](https://miro.medium.com/max/60/1*yYy7_ICCyvQQkl2BIsGtvg.png?q=20)

![Image for post](https://miro.medium.com/max/1238/1*yYy7_ICCyvQQkl2BIsGtvg.png)

<noscript>![Image for post](https://miro.medium.com/max/2476/1*yYy7_ICCyvQQkl2BIsGtvg.png)</noscript>

<font _mstmutation="1" _msthash="39351" _msttexthash="368970472">让我们使用与 Nexus 仪表板相同的凭据添加身份验证（如错误消息中的建议）：</font>

> <font _mstmutation="1" _msthash="33995" _msttexthash="87895574">注意： 请注意注册表 URL 包含存储库名称</font>

 ![Image for post](https://miro.medium.com/max/60/1*iMdWS5OwjSsd26HxgQjyww.png?q=20)

![Image for post](https://miro.medium.com/max/1146/1*iMdWS5OwjSsd26HxgQjyww.png)

<noscript>![Image for post](https://miro.medium.com/max/2292/1*iMdWS5OwjSsd26HxgQjyww.png)</noscript>

<font _mstmutation="1" _msthash="23114" _msttexthash="275944240">让我们再试一次！现在我们看到一个不同的错误，说它不能发出请求：</font>```Put```

 ![Image for post](https://miro.medium.com/max/60/1*c2nv0agkplmO_kP3MGN3oA.png?q=20)

![Image for post](https://miro.medium.com/max/1288/1*c2nv0agkplmO_kP3MGN3oA.png)

<noscript>![Image for post](https://miro.medium.com/max/2576/1*c2nv0agkplmO_kP3MGN3oA.png)</noscript>

<font _mstmutation="1" _msthash="28691" _msttexthash="1003500420">这是因为安全性在 Nexus 中的工作方式，即确定任何用户如何与 Nexus 交互的概念。应用的默认值称为本地身份验证和本地授权，其职责根据文档如下：</font>```realms``````realm``````realm```

> <font _mstmutation="1" _msthash="21944" _msttexthash="218668151">它们允许存储库管理器在没有其他外部系统的情况下管理安全设置。</font>

<font _mstmutation="1" _msthash="29003" _msttexthash="299029432">我们需要添加附加功能以启用功能。要启用其他领域，请转到"设置>安全>领域"。</font>```realms``````npm publish```

<font _mstmutation="1" _msthash="28744" _msttexthash="127973417">添加 并保存更改。有关领域的其他信息可在此[获得](https://zshipu.com/t?url=https://help.sonatype.com/repomanager3/security/realms)。</font>```npm Bearer Token Realm```

 ![Image for post](https://miro.medium.com/max/60/1*JJc2Gybcyrqpqaj-kojTaA.png?q=20)

![Image for post](https://miro.medium.com/max/1866/1*JJc2Gybcyrqpqaj-kojTaA.png)

<noscript>![Image for post](https://miro.medium.com/max/3732/1*JJc2Gybcyrqpqaj-kojTaA.png)</noscript>

<font _mstmutation="1" _msthash="40131" _msttexthash="152885096">现在，我们准备重试发布命令，并可以正常使用：</font>

 ![Image for post](https://miro.medium.com/max/60/1*cMuXGlu1yaOHSMXldZ56XQ.png?q=20)

![Image for post](https://miro.medium.com/max/1114/1*cMuXGlu1yaOHSMXldZ56XQ.png)

<noscript>![Image for post](https://miro.medium.com/max/2228/1*cMuXGlu1yaOHSMXldZ56XQ.png)</noscript>

<font _mstmutation="1" _msthash="34710" _msttexthash="777833615">为了验证，我们可以浏览我们的存储库，并按预期查看包。从顶部导航栏 > 浏览 > npm - 私人选择"浏览"选项，查看如下所示的套餐：</font>

 ![Image for post](https://miro.medium.com/max/60/1*VRRYl5ZiaPUJzY0lquknBw.png?q=20)

![Image for post](https://miro.medium.com/max/1490/1*VRRYl5ZiaPUJzY0lquknBw.png)

<noscript>![Image for post](https://miro.medium.com/max/2980/1*VRRYl5ZiaPUJzY0lquknBw.png)</noscript>

<font _mstmutation="1" _msthash="34697" _msttexthash="316921124">我们还可以验证要在 S3 中上载的文件夹称为 ，尽管它在存储时转换为 Blob 时无法清晰。</font>```content```

# <font _mstmutation="1" _msthash="27820" _msttexthash="42904511">从 Nexus 中拉出二进制文件</font>

<font _mstmutation="1" _msthash="29120" _msttexthash="326574469">现在，我们已经发布了二进制到Nexus，让我们创建另一个项目，我们将尝试使用。</font>```npm-app1```

mkdir npm-app2 && cd npm-app2npm init -y

<font _mstmutation="1" _msthash="33579" _msttexthash="1162359367">在尝试从存储库中检索之前，让我们删除之前添加的凭据。我们这样做是为了避免使用这些凭据来检索包。理想情况下，我们希望复制使用我们应用程序的新开发人员的经验。</font>```npm install``` ```npm-app1``````npm login```

<font _mstmutation="1" _msthash="35490" _msttexthash="106936752">要删除这些凭据，只需运行以下命令：</font>

npm logout --registry=[http://localhost:8081/repository/npm-private/](https://zshipu.com/t?url=http://localhost:8081/repository/npm-private/)

<font _mstmutation="1" _msthash="33930" _msttexthash="117701493">现在，让我们尝试从我们的新项目安装：</font>```npm-app1``````npm-app2```

npm i -S npm-app1

<font _mstmutation="1" _msthash="34307" _msttexthash="298518129">不出所料，我们看到 404 错误，因为默认情况下在公共注册表上找不到该错误。</font>```npm-app1``````npm```

 ![Image for post](https://miro.medium.com/max/60/1*1vNugMumuSwUf_huw_44Fw.png?q=20)

![Image for post](https://miro.medium.com/max/1244/1*1vNugMumuSwUf_huw_44Fw.png)

<noscript>![Image for post](https://miro.medium.com/max/2488/1*1vNugMumuSwUf_huw_44Fw.png)</noscript>

<font _mstmutation="1" _msthash="39741" _msttexthash="511458649">要解决此问题，我们需要在本地向项目添加一个文件。此文件包含我们需要指向的提取包和所需的任何其他凭据。</font>```.npmrc``````.npmrc``````registry```

touch .npmrc

<font _mstmutation="1" _msthash="32683" _msttexthash="257611926">我们首先添加注册表，我们需要指向该注册表，以便能够检索我们的包</font>

registry=[http://localhost:8081/repository/npm-group](https://zshipu.com/t?url=http://localhost:8081/repository/npm-group)/

<font _mstmutation="1" _msthash="39871" _msttexthash="906998885">请注意，我们指向 的 不是 存储库，因为我们想要同时访问私有和近在近的公共包。我们可以看到，该项目位于，但不能安装，因为我们没有授权。</font>```npm-group``````npm-private``````npm```

 ![Image for post](https://miro.medium.com/max/60/1*C4CXyxhHsmE3CPQSatXecA.png?q=20)

![Image for post](https://miro.medium.com/max/1212/1*C4CXyxhHsmE3CPQSatXecA.png)

<noscript>![Image for post](https://miro.medium.com/max/2424/1*C4CXyxhHsmE3CPQSatXecA.png)</noscript>

<font _mstmutation="1" _msthash="22087" _msttexthash="115304254">最简单的解决方案是添加使这项工作所需的。</font>```authToken```

> <font _mstmutation="1" _msthash="38221" _msttexthash="767994500">最佳做法是，我建议创建一个所有存储库都具有只读角色的新用户。我们这样做，因为不想将 Nexus 的管理员身份验证令牌添加到源代码中。</font>
> 
> <font _mstmutation="1" _msthash="37050" _msttexthash="368785755">为此，创建具有与读取和浏览相关的所有权限的角色，最简单的方法是提供角色 和 特权</font>```nx-repository-view-*-*-browse``````nx-repository-view-*-*-read```

 ![Image for post](https://miro.medium.com/max/60/1*2FJB8yDQpW12FyLF9qvOLA.png?q=20)

![Image for post](https://miro.medium.com/max/1754/1*2FJB8yDQpW12FyLF9qvOLA.png)

<noscript>![Image for post](https://miro.medium.com/max/3508/1*2FJB8yDQpW12FyLF9qvOLA.png)</noscript>

> <font _mstmutation="1" _msthash="27339" _msttexthash="75380916">然后创建具有以下角色的用户：</font>

 ![Image for post](https://miro.medium.com/max/60/1*lFfl_yxa2eC4wolc7XTbSw.png?q=20)

![Image for post](https://miro.medium.com/max/1728/1*lFfl_yxa2eC4wolc7XTbSw.png)

<noscript>![Image for post](https://miro.medium.com/max/3456/1*lFfl_yxa2eC4wolc7XTbSw.png)</noscript>

<font _mstmutation="1" _msthash="24349" _msttexthash="262222324">接下来，要获取此用户的身份验证令牌，请执行指向我们的存储库：</font>```npm login``````npm-group```

 ![Image for post](https://miro.medium.com/max/60/1*p97heVo71KDkGYYQ8rJhCQ.png?q=20)

![Image for post](https://miro.medium.com/max/1154/1*p97heVo71KDkGYYQ8rJhCQ.png)

<noscript>![Image for post](https://miro.medium.com/max/2308/1*p97heVo71KDkGYYQ8rJhCQ.png)</noscript>

<font _mstmutation="1" _msthash="35204" _msttexthash="348202907">执行登录将凭据添加到计算机根目录的文件。打开全局文件并找到类似于以下内容的行：</font>```.npmrc``````.npmrc```

//localhost:8081/repository/npm-group/:_authToken=NpmToken.bb495270–9831–3046–8c24-a2978853d3a1

<font _mstmutation="1" _msthash="34073" _msttexthash="665428920">是上面打印的行的最后一位。现在，我们可以将 添加到项目中的文件。我们这样做是为了避免登录到克隆此存储库的每台计算机。</font>```_authToken``````_authToken``````.npmrc``````npm-app2```

<font _mstmutation="1" _msthash="28223" _msttexthash="55868423">让我们在继续之前注销：</font>

npm logout --registry=[http://localhost:8081/repository/npm-group/](https://zshipu.com/t?url=http://localhost:8081/repository/npm-private/)

<font _mstmutation="1" _msthash="23101" _msttexthash="82097756">项目中文件的最终形式如下所示：</font>```.npmrc```

<font _mstmutation="1" _msthash="44161" _msttexthash="250043599">有了这个，我们现在应该能够安装和使用任何和所有包，如下所示：</font>

 ![Image for post](https://miro.medium.com/max/60/1*ashW3MiXiFVK8VMKJNmzow.png?q=20)

![Image for post](https://miro.medium.com/max/1436/1*ashW3MiXiFVK8VMKJNmzow.png)

<noscript>![Image for post](https://miro.medium.com/max/2872/1*ashW3MiXiFVK8VMKJNmzow.png)</noscript>

<font _mstmutation="1" _msthash="29666" _msttexthash="315420846">当我们浏览存储库时，我们可以看到代理包（本例中是 lodash）的缓存在行动：</font>

 ![Image for post](https://miro.medium.com/max/60/1*RvUKiIfxH5NQmZXnQxLOoQ.png?q=20)

![Image for post](https://miro.medium.com/max/1548/1*RvUKiIfxH5NQmZXnQxLOoQ.png)

<noscript>![Image for post](https://miro.medium.com/max/3096/1*RvUKiIfxH5NQmZXnQxLOoQ.png)</noscript>

# <font _mstmutation="1" _msthash="34957" _msttexthash="6674577">结论</font>

<font _mstmutation="1" _msthash="34671" _msttexthash="2210319553">本文仅介绍如何使用 Nexus 作为存储库管理器的一些基础知识。尽管我们运行容器并将卷装载到本地目录，但强烈建议您在您选择的云提供商上试用上述内容。请记住，对于云提供商（或自托管），您需要备份卷以进行灾难恢复。</font>
