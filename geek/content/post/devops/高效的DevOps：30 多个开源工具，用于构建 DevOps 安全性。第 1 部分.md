
---
title: 高效的DevOps：30 多个开源工具，用于构建 DevOps 安全性。第 1 部分
author: 知识铺
date: 2020-10-13 22:50:06+08:00

tags: [DevOps]
---
<font _mstmutation="1" _msthash="26988" _msttexthash="432076398">新的安全工具没有时间成为快速增长的实践集的一部分，这使我想将某个检查点设置为工具列表。</font>

<font _mstmutation="1" _msthash="28808" _msttexthash="574300584">实践意味着一组措施可以内置到 SDLC/DevOps 的阶段之一（威胁建模、SAST、DAST、SCA、Docker 图像扫描、Kubernetes 扫描、AWS 审核等）。</font>

 

![image-20210930085918331](https://cdn.jsdelivr.net/gh/zshipu/images/202109300859663.png)





# <font _mstmutation="1" _msthash="23465" _msttexthash="14705236">1.威胁建模</font>

<font _mstmutation="1" _msthash="27872" _msttexthash="4596282067">因此，安全开发生命周期环境中的威胁建模是分析软件体系结构是否存在潜在软件漏洞和不安全技术的过程。为了降低从安全角度添加附加功能的成本，解决方案可能是在体系结构设计阶段实现已处于安全检查过程。在同一阶段，AppSec 专家的要求已经形成，并将进入积压工作。此方法实际上用于所有 DevSecOps 实践，并已收到稳定的表达式"向左移动安全性"。</font>

<font _mstmutation="1" _msthash="32370" _msttexthash="834232789">为了使此过程在现代开发中以高发行率在大型 IT 公司中找到位置，还必须自动化对威胁进行建模的过程。下面是一些可以提供帮助的开源工具库。</font>

<font _mstmutation="1" _msthash="37375" _msttexthash="20454694">**1.1** [**OWASP 威胁龙**](https://zshipu.com/t?url=https://owasp.org/www-project-threat-dragon/)</font>

 ![Image for post](https://miro.medium.com/max/60/0*cGawBPFx3IWWFzvJ.png?q=20)![image-20210930085959579](https://cdn.jsdelivr.net/gh/zshipu/images/202109300900642.png)



<font _mstmutation="1" _msthash="23036" _msttexthash="1781540280">一个非常简单的工具，用于自我建模的威胁。用户绘制软件体系结构，指示可以遵循 STRIDE 方法的威胁。没有自动化，但在经典版本中，当进程被调试时，可能很有用。此工具特别用于对 GitHub 中的威胁进行建模。</font>

<font _mstmutation="1" _msthash="27014" _msttexthash="922683060">使用 pytm 框架中描述的元素和属性在 Python 中定义系统。根据您的定义，pytm 可以生成数据流图 （DFD）、序列图，最重要的是对系统的威胁。</font>

[**1.2 皮特姆**](https://zshipu.com/t?url=https://github.com/izar/pytm)



<font _mstmutation="1" _msthash="34762" _msttexthash="1438373105">Pytm 是 Python 上的一个框架，用于创建数据流图和系统威胁列表。Pytm 用户以代码形式在体系结构中定义组件交互模型，然后该工具生成组件交互图本身。它可用于协作和版本跟踪系统。</font>

# <font _mstmutation="1" _msthash="33540" _msttexthash="84448390">2\. 漏洞静态应用程序分析 （SAST）</font>

<font _mstmutation="1" _msthash="32981" _msttexthash="1048401666">让我们进入测试阶段，即静态代码分析。有很多代码分析器。反过来，开源工具之所以突出，是因为它们是为特定语言编写的。在以下集合中可以找到大量工具：</font>

> [OWASP 源代码分析工具](https://zshipu.com/t?url=https://owasp.org/www-community/Source_Code_Analysis_Tools)
>
> [静态分析工具](https://zshipu.com/t?url=https://github.com/analysis-tools-dev/static-analysis)

<font _mstmutation="1" _msthash="27456" _msttexthash="112854482">但也有一些相当奇怪的工具，可以普遍使用。</font>



<noscript>![Image for post](https://miro.medium.com/max/1464/1*vCJGywggCRyihTp41CsvsQ.png)</noscript>

<font _mstmutation="1" _msthash="27599" _msttexthash="2996178835">Salus（安全自动化作为轻量级通用扫描仪），[以罗马保护女神](https://zshipu.com/t?url=https://en.wikipedia.org/wiki/Salus)的名字命名，是协调安全扫描仪执行的工具。您可以通过 Docker 守护进程在存储库上运行 Salus，它将确定哪些扫描仪是相关的，运行它们并提供输出。大多数扫描仪是其他成熟的开源项目，我们直接包括在容器中。</font>

<font _mstmutation="1" _msthash="29263" _msttexthash="2808325676">Salus 对 CI/CD 管道特别有用，因为它成为跨大型存储库队列协调扫描的集中位置。通常，每个项目的扫描程序在存储库级别进行配置。这意味着，在组织范围更改扫描仪的运行方式时，必须更新每个存储库。相反，您可以更新 Salus，所有生成将立即继承更改。</font>

<font _mstmutation="1" _msthash="28665" _msttexthash="1331799027">容器的图像，其中放置了多个静态分析器（如强盗、Gosec、布雷克曼和开源组件（Ruby、Node.js、Python、Go）。在输出中，我们获取 JSON/YAML 报告。在 GitHub 上，您还可以找到 CircleCI 中嵌入的说明。</font>

[**2.2 移位式扫描**](https://zshipu.com/t?url=https://github.com/ShiftLeftSecurity/sast-scan)



![image-20210930090100695](../../../../../../../images/image-20210930090100695.png)



<font _mstmutation="1" _msthash="28860" _msttexthash="1735539221">该工具的工作方式与 Salus 类似，但支持更多静态分析器。在存储库中，您可以看到放置在 Docker 映像中的静态分析器（gosec、find-sec 错误、诗篇、土匪、...）。甚至地形、bash、库伯内特清单分析器也被放置在 Docker 映像中。</font>

[**2.3 GitLab Sast**](https://zshipu.com/t?url=https://docs.gitlab.com/ee/user/application_security/sast/)

 ![Image for post](https://miro.medium.com/max/60/0*zPKAaBb7Z3yzHPc-.png?q=20)

![Image for post](https://miro.medium.com/max/1088/0*zPKAaBb7Z3yzHPc-.png)

<noscript>![Image for post](https://miro.medium.com/max/2176/0*zPKAaBb7Z3yzHPc-.png)</noscript>

<font _mstmutation="1" _msthash="34489" _msttexthash="1625349362">Gitlab 是一个相当受欢迎的 DevOps 平台，但它还有一组免费的不同开源 SSTS，可以从框连接到绘画。Gitlab 还能够嵌入 SCA、秘密搜索、模糊和其他 DevSecOps 实践，但所有工具的集中管理仅在 Gold 版本中可用。</font>

# <font _mstmutation="1" _msthash="27015" _msttexthash="23716693">3\. 检查开源组件 + SCA</font>

<font _mstmutation="1" _msthash="30615" _msttexthash="1798445896">除了在命令内开发的代码外，还应检查连接到项目的开源。缺乏对漏洞的第三方组件分析过程可能会严重影响产品的安全性。工作原理，比较流行的SCA工具，我在一个单独的文章，在这里我们将讨论什么工具存在。</font>

[**3.1 依赖项检查**](https://zshipu.com/t?url=https://github.com/jeremylong/DependencyCheck)

 ![Image for post](https://miro.medium.com/max/60/0*uwlHM4-Uham44M1V.png?q=20)

![Image for post](https://miro.medium.com/max/1920/0*uwlHM4-Uham44M1V.png)

<noscript>![Image for post](https://miro.medium.com/max/3840/0*uwlHM4-Uham44M1V.png)</noscript>

<font _mstmutation="1" _msthash="29861" _msttexthash="4549760371">依赖项检查是 OWASP 中用于检查第三方组件的最流行的开源解决方案之一。有许多现成的集成，嵌入管道的方法，但该工具有很多发展到质量。建议对安全 SDLC 流程处于初始阶段的公司实施，网络安全专家有时间分析误报。依赖项检查没有一个平台可以回顾跟踪结果，因此，如果组织中的漏洞管理过程未构建，则应注意依赖关系跟踪。</font>

[**3.2 依赖关系轨道**](https://zshipu.com/t?url=https://dependencytrack.org/)

 ![Image for post](https://miro.medium.com/max/60/0*Lymjsncya8uvvOLm.png?q=20)

![Image for post](https://miro.medium.com/max/2000/0*Lymjsncya8uvvOLm.png)

<noscript>![Image for post](https://miro.medium.com/max/4000/0*Lymjsncya8uvvOLm.png)</noscript>

<font _mstmutation="1" _msthash="29862" _msttexthash="3311663381">依赖性跟踪是 OWASP 中第二受欢迎的解决方案，它是一个 Web 平台，它接受来自另一个 CycloneDx 工具的软件物料清单 （SBOM） 输入。依赖关系跟踪探索 BOM，然后访问公开可用的漏洞数据库（如 NVD）。该工具还能够与 Slack、Microsoft 团队集成、扫描工件存储库和检查第三方组件的许可证纯度。</font>

**3.3 Sonatype 开源**

 ![Image for post](https://miro.medium.com/max/60/0*a5NHfpYtyHTHhNxr.png?q=20)

![Image for post](https://miro.medium.com/max/2000/0*a5NHfpYtyHTHhNxr.png)

<noscript>![Image for post](https://miro.medium.com/max/4000/0*a5NHfpYtyHTHhNxr.png)</noscript>

<font _mstmutation="1" _msthash="34502" _msttexthash="4770786189">除了 NVD（大多数解决方案的漏洞信息的主要来源）之外，Sonatype OSS 数据库还由 Sonatype 支持，该数据库还具有商业 Nexus IQ 解决方案。反过来，我们采用了NexusIQ作为我们的客户的主要SCA工具。Sonatype OSS 是一个漏洞数据库，可连接到依赖项检查和依赖跟踪工具。此外，Sonatype 支持以下开源 SCA 工具，这些工具可用于扫描依赖项和从 Sonatype OSS 中收集数据。</font>

*   <font _mstmutation="1" _msthash="23361" _msttexthash="141717914">AuditJS = JS 扫描仪（NPM、角、纱线、弓箭手）</font>
*   <font _mstmutation="1" _msthash="21801" _msttexthash="23412116">南希 + Golang扫描仪</font>
*   <font _mstmutation="1" _msthash="22399" _msttexthash="25875993">杰克 • 康达扫描仪</font>
*   <font _mstmutation="1" _msthash="28756" _msttexthash="35740146">切尔西 + 红宝石扫描仪</font>
*   <font _mstmutation="1" _msthash="38194" _msttexthash="54331069">支票 + C/C++扫描仪 （GCC）</font>
*   <font _mstmutation="1" _msthash="38675" _msttexthash="85169344">Ahab = 扫描仪贴切， apk， yum， dnf 包</font>
*   <font _mstmutation="1" _msthash="22776" _msttexthash="61603204">裤子 + 扫描仪锈 （货物）</font>
*   <font _mstmutation="1" _msthash="23738" _msttexthash="59821281">索纳型 Depshield + GitHub 项目扫描仪</font>

# <font _mstmutation="1" _msthash="23010" _msttexthash="15297932">4\. 搜索秘密</font>

<font _mstmutation="1" _msthash="28158" _msttexthash="2999186957">项目可能不仅包含其自己的代码和开源组件中允许的漏洞，还包含密码、令牌、私钥等机密。等。当然，如果代码包含来自关键数据库的开放密码，则不需要在存储库中允许它。为此，有许多工具可以帮助您查找公开的秘密。我们不会在这里停留太久，因为各地的操作原则都是一样的。</font>

[**4.1 git 机密**](https://zshipu.com/t?url=https://github.com/awslabs/git-secrets)

<font _mstmutation="1" _msthash="23985" _msttexthash="100483955">防止您将密码和其他敏感信息提交到 git 存储库。</font>

 ![Image for post](https://miro.medium.com/max/60/0*ZphKNCIkfbwIqQe2.png?q=20)

![Image for post](https://miro.medium.com/max/620/0*ZphKNCIkfbwIqQe2.png)

<noscript>![Image for post](https://miro.medium.com/max/1240/0*ZphKNCIkfbwIqQe2.png)</noscript>

[**4.2 吉特罗布**](https://zshipu.com/t?url=https://github.com/michenriksen/gitrob)

<font _mstmutation="1" _msthash="33423" _msttexthash="2244027123">Gitrob 是一个工具，可帮助查找推送到 Github 上公共存储库的潜在敏感文件。Gitrob 将克隆属于用户或组织的存储库，并迭代提交历史记录和标记与潜在敏感文件签名匹配的文件。研究结果将通过网络界面呈现，以便于浏览和分析。</font>

 ![Image for post](https://miro.medium.com/max/60/0*pQd-WZNPB9kx0k-4.PNG?q=20)

![Image for post](https://miro.medium.com/max/726/0*pQd-WZNPB9kx0k-4.PNG)

<noscript>![Image for post](https://miro.medium.com/max/1452/0*pQd-WZNPB9kx0k-4.PNG)</noscript>

[**4.3 Gitleaks**](https://zshipu.com/t?url=https://github.com/zricethezav/gitleaks)

<font _mstmutation="1" _msthash="43953" _msttexthash="1174555915">Gitleaks 是一个 SAST 工具，用于检测密码、api 密钥和 git 存储库中的令牌等硬编码机密。Gitleaks 的目标是在代码中查找过去或现在的秘密的易于使用的一切解决方案。</font>

 ![Image for post](https://miro.medium.com/max/60/0*uuyLdq8z-uH4jsyP.png?q=20)

![Image for post](https://miro.medium.com/max/1773/0*uuyLdq8z-uH4jsyP.png)

<noscript>![Image for post](https://miro.medium.com/max/3546/0*uuyLdq8z-uH4jsyP.png)</noscript>

[**4.4 特鲁弗勒霍格**](https://zshipu.com/t?url=https://github.com/dxa4481/truffleHog)

<font _mstmutation="1" _msthash="32721" _msttexthash="406177434">通过 git 存储库搜索机密，深入了解提交历史记录和分支。这对于查找意外提交的秘密是有效的。</font>

 ![Image for post](https://miro.medium.com/max/60/0*P7Kw9kGuspcOuh0A.png?q=20)

![Image for post](https://miro.medium.com/max/1876/0*P7Kw9kGuspcOuh0A.png)

<noscript>![Image for post](https://miro.medium.com/max/3752/0*P7Kw9kGuspcOuh0A.png)</noscript>

[**4.5 GitGuardian**](https://zshipu.com/t?url=https://www.gitguardian.com/community)

<font _mstmutation="1" _msthash="33241" _msttexthash="92613924">用于应用程序安全性的自动机密检测工具</font>

 ![Image for post](https://miro.medium.com/max/60/0*Hg6BixBAEQXh0rat.png?q=20)

