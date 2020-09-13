
title: 从零开始 - 第 6 部分 - 建立一个 ios 应用程序， 没有 Mac 或 iphone 使用 Flutter
author: 知识铺
date: 2020-09-13 19:16:19
tags: flutter
---
  

* * *

## 内容

*   [开始](#getting-started)
    *   [您需要什么](#what-youll-need)
    *   [设置开发帐户](#setting-up-the-dev-account)
*   [构建应用](#building-the-app)
    *   [如果你还在开发](#if-youre-still-developing)
    *   [如果您已经构建了应用](#if-youve-built-your-app)
    *   [你需要_一_个 mac](#you-will-need-a-mac)
        *   [为什么？因为包。](#why-because-packages)
        *   [为什么？因为测试。](#why-because-testing)
    *   [Mac 和 XCode](#mac-and-xcode)
        *   [设置您的环境](#setup-your-environment)
        *   [Mac 提示](#mac-tips)
        *   [使用 XCode](#using-xcode)
        *   [Firebase + Podfile](#firebase--podfile)
        *   [应用程序权限](#app-permissions)
    *   [其他内容](#other-stuff)
        *   [版本和生成 ID](#versions-and-build-ids)
        *   [图标](#icon)
        *   [应用内购买](#in-app-purchases)
*   [部署](#deployment)
    *   [存储资产](#store-assets)
        *   [图像](#images)
        *   [视频（可选）](#videos-optional)
    *   [生成和上传](#build-and-upload)
    *   [发布新版本](#publishing-new-releases)
*   [最终想法](#final-thoughts)

* * *

所以你正在使用 Windows / Linux， 想构建一个 ios 应用程序， 嗯？

我现在告诉你， 这并不容易， 但希望你能从我的痛苦中吸取教训。在本指南中，我将向您展示如何在无需访问 mac 或 iPhone 的情况下在应用商店中构建、测试和启动。

破坏者： 你实际上需要一个 iDevice， 但有可能这样做， 而无需触摸一个自己。我会告诉你怎么做的。

如果你是新到 Flutter， 然后看看下面的系列的第一个帖子！

  [![Project photo](https://d33wubrfki0l68.cloudfront.net/897a33b25c9053e1df6fbefa8f54bc8f90a07203/e15ca/images/posts/2020-05-15/banner.jpg) 
 零到英雄 - 第 1 部分 - 我如何建立我的游戏与 Flutter 在 1 个月。](/2020/05/15/zero-to-hero-1) [![Project photo](https://d33wubrfki0l68.cloudfront.net/f06e33fce84bdb5bb27eb2017be560b2f1043487/12aa5/images/projects/icing-addict.jpg) 
 结冰成瘾](https://zshipu.com/t?url=https://icing-addict.kangabru.xyz/) 



* * *

## 开始

Flutter 承诺在 Android、iOS 甚至其他平台上构建应用程序-所有这些都在单个代码库内。

这不辜负炒作吗？绝对。但挑战不是Flutter，而是苹果。

### 您需要什么

*   您的 Flutter 应用程序
*   苹果开发者帐户 $99 USD
*   在云中租用 Mac 的 20 美元（可能是可选的）
*   拥有 iDevice 的朋友（即 iPhone 或 iPad）
*   电话号码
*   很多耐心， 也许一些酒精

### 设置开发帐户

首先你需要一个苹果帐户。[在这里做一个](https://zshipu.com/t?url=https://appleid.apple.com/)。

接下来，您需要设置 2 因素身份验证。苹果的措辞在这里很奇怪， 但他们有 2 个概念：

*   2_步_验证 - 使用代码登录（如通过短信）
*   2_因素_身份验证 - 通过确认关联 iDevice 上的登录登录

你需要同时做到这两点。您需要身份验证_才能_创建 apple 开发人员帐户，但将使用_验证_登录。

首先设置 2 因子验证并使用您的电话号码接收文本。这是开发帐户设置后登录的配置。

其次，您需要设置 2 因素身份验证来创建 Apple 开发人员帐户并发布应用程序。这是您的物理设备的来源 - 您需要将其关联到帐户。问朋友或家庭成员， 如果你能使用他们的 （btw 谢谢妈妈！

[按照此页](https://zshipu.com/t?url=https://developer.apple.com/support/authentication/)在 iDevice 上设置 2 个因素身份验证。请注意：

*   您必须在整个开发过程中保持关联。如果没有设备链接到您的帐户， 苹果将拒绝上传到应用商店...
*   如果您更改帐户密码，您将断开链接。您应该信任拥有设备的人，并安全地向他们发送密码。

从现在开始，系统将提示您使用 2 因子身份验证通过 iDevice 确认登录。您只需选择"未获取验证码"选项即可绕过此选项来使用您的电话号码。

![](https://d33wubrfki0l68.cloudfront.net/f88f30e86fb9ef422f6dd3779e995436869643c1/e00cc/images/posts/2020-07-18/login.jpg)

一旦你设置，你可以在这里注册[苹果开发者帐户](https://zshipu.com/t?url=https://developer.apple.com/programs/enroll/)。只需支付 $99 （！） 费用，您就可以出发了！

* * *

## 构建应用

Flutter 本身在 ios 上工作得很好， 没有太多的问题。它是第三方包，经常需要 iOS 特定的代码或额外的安装_步骤（尤其是_Firebase）。

### 如果你还在开发

如果您目前正在开发应用，那么在安装新包时需要做大量的笔记。

*   保留涵盖需要 iOS 特定安装步骤的软件包的文档。
*   在需要 iOS 特定代码的地方添加明显的代码注释。

在 Android 上构建应用程序后，您可以在尝试在 iOS 上部署之前重新浏览笔记，以确保一切外观良好。

我没有_做笔记_， 把一切都留到最后 - 这是一个痛苦， 因为我必须找到我的应用程序的一部分， 我需要 ios 特定的代码...节省自己的精力， 并在需要 iOS 之前记录您的 ios 需求。

### 如果您已经构建了应用

如果您已经构建了应用，请浏览_您添加的每个_包并阅读 iOS 安装说明。还要仔细检查您的代码，以确保您根据需要添加了 iOS 特定代码。

许多软件包（尤其是 Firebase）具有需要在 iOS 上使用的特定配置。请仔细执行他们的指示。我必须更新我的 Flutter 代码， 如下所示：

*   为 Firebase 添加 ios 配置
*   添加用于应用内购买的 iOS ID
*   使用 Firebase 动态链接时添加 iOS 参数

某些包可能不需要更改代码 - 是的，您可能需要使用 XCode。我将解释如何在以下部分。


* * *

### 你需要_一_个 mac

我真的很想避免使用 mac， 但不幸的是， 这是必要的。有 90% 的机会， 你也需要。您需要使用 mac 有 2 个原因 - 通过 XCode 和测试安装某些软件包。

#### 为什么？因为包。

不幸的是，有些软件包需要的不仅仅是一个酒吧包安装才能工作。有时您可能需要 XCode 来正确配置应用。我不得不使用 XCode 安装这些软件包：

*   Firebase本身 » 分析 » 动态链接
*   应用程序权限
*   应用内购买

如果您不使用特殊权限或更复杂的软件包，那么如果没有_Mac，_您可能没问题。如果你这样做， 那么你需要租一台 Mac 进行小开发。

#### 为什么？因为测试。

我强烈建议你租一个 mac 反正只是为了测试你的应用程序。在没有设备或模拟器的情况下测试和调试应用是一个严重的 PITA。我希望我能部署， 应用程序只会工作 - 我有多天真啊？

省去麻烦，租个 mac 。在 Mac 上运行 VSCode 和 iOS 模拟器感觉就像在 Windows 上开发一样。

### Mac 和 XCode

如果你决定你需要租一台Mac，那么我建议[macincloud。](https://zshipu.com/t?url=https://www.macincloud.com/)我以 20 美元获得 1 个月的访问权限。

以这个价格，你每天得到3小时的访问，比我每天可以忍受的时间😅

#### 设置您的环境

设置通常是无痛的。该实例附带安装了 VSCode + XCode，我使用 Github 快速访问代码。下[一次安装 Flutter，](https://zshipu.com/t?url=https://flutter.dev/docs/get-started/install/macos)你几乎设置。

如果您使用 Windows，则我发现此命令在安装后可将 Flutter 添加到我的路径中：

```export PATH="$PATH:/Users/<user>/<install_path>/flutter/bin"```

如果使用 VSCode，那么您应该准备好出发。运行应用程序，就像你在 Windows/Linux 和 iOS 模拟器应该弹出。

#### Mac 提示

<font _mstmutation="1" _msthash="429962" _msttexthash="434858658">如果使用 Windows 键盘，键盘快捷键大多将"控制"替换为"Win"键，即使用 Windows 键盘在 Mac 上的"复制"是 。</font>```Win + C```

使用右上右侧的搜索栏搜索应用。

Finder[应用](https://zshipu.com/t?url=https://support.apple.com/en-us/HT201732)与 Windows 资源管理器一样。

通过右键单击文件、单击"文件信息"，然后突出显示路径并复制该路径，将文件路径复制到剪贴板。

[Xcode](https://zshipu.com/t?url=https://developer.apple.com/xcode/)是 ios Ide 和[模拟器](https://zshipu.com/t?url=https://developer.apple.com/library/archive/documentation/IDEs/Conceptual/iOS_Simulator_Guide/GettingStartedwithiOSSimulator/GettingStartedwithiOSSimulator.html)就像 Android 模拟器， 但对于 ios 。

#### 使用 XCode

您只需使用 XCode 为某些第三方包设置额外的配置 - 使用 VSCode 执行所有 Flutter 代码。

您还可能会发现，在更新选项时，XCode 会更新一吨配置文件。这就是为什么目前无法真正安装一些没有 XCode 的软件包的原因。

#### Firebase + Podfile

<font _mstmutation="1" _msthash="429949" _msttexthash="69121078">通过在文件中启用，确保启用 Firebase。</font>```AppDelegate.swift```

 ```
 import UIKit
import Flutter
import Firebase

@UIApplicationMain
@objc class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    FirebaseApp.configure()
    GeneratedPluginRegistrant.register(with: self)
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
}
``` 

我的 Firebase 包还需要一个不是由 Flutter 生成的 Podfile。我的应用仅在 XCode 自动为我生成一个后才能工作，我根据他们的说明为 Firebase 分析和动态链接包添加了配置。

#### 应用程序权限

iOS 要求您在需要使用权限时包括说明。

如果使用像["permission_handler包](https://zshipu.com/t?url=https://pub.dev/packages/permission_handler)，则需要为"所有"权限添加这些说明，即使您不使用它们。这是因为苹果的静态分析器将看到API调用，并假设他们正在被使用。

<font _mstmutation="1" _msthash="428805" _msttexthash="77730484">将它们像这样添加到您的文件中：</font>```Info.plist```

 ```
 <key>NSAppleMusicUsageDescription</key>
<string>Music access not used but required by permissions API.</string>

<key>NSCalendarsUsageDescription</key>
<string>Calendar access not used but required by permissions API.</string>
``` 

[在此处查找所有键和进一步说明](https://zshipu.com/t?url=https://pub.dev/packages/permission_handler)。

### 其他内容

#### 版本和生成 ID

如果在某些情况下已使用生成 ID 或版本号，Apple 将拒绝您的应用。

<font _mstmutation="1" _msthash="427661" _msttexthash="232220690">一个示例版本代码（如文件中定义）是 - 部件是版本号，是生成号。</font>```pubspec.yaml``````1.1.1+12``````1.1.1``````+12```

如果将新的应用存档上载到 Apple（即添加新的测试版本），请确保更新生成 ID。

如果将版本公开发布到应用商店，请确保更新版本号。

#### 图标

我强烈建议您[使用flutter_launcher_icons生成](https://zshipu.com/t?url=https://pub.dev/packages/flutter_launcher_icons)应用图标。

iOS 的一件事是，您不能在应用图标中使用透明度。如果使用 PNG，您甚至不能具有透明度图层，因此在 Photoshop 等**程序中关闭透明度设置**时导出 PNG。

#### 应用内购买

测试应用内购买糟透了。我按照[T](https://zshipu.com/t?url=https://pub.dev/packages/in_app_purchase)的指示， 但我不能让他们在 ios 上工作

由于[这个线程](https://zshipu.com/t?url=https://developer.apple.com/forums/thread/100356?page=2)[和这个](https://zshipu.com/t?url=https://stackoverflow.com/questions/36660280/not-showing-amendments-or-request-button-to-accept-the-updated-apple-develop)线程，我能够解决这个问题。事实证明，您必须：

*   [设置银行详细信息](https://zshipu.com/t?url=https://appstoreconnect.apple.com/agreements/#/banking)
*   [同意此处的协议](https://zshipu.com/t?url=https://developer.apple.com/account/#/membership)

我甚至不能测试应用程序内购买， 直到这些完成。

* * *

## 部署

### 存储资产

商店具有非常具体的资产大小和内容规则。确保您遵循要求，否则您的应用在提交时将被拒绝。

#### 图像

您将需要制作至少 2 套资产（用于 5.5" 和 6.5" iPhone），如果支持 iPad，则需要制作一套额外的资产。图像必须是他们在这里指定[的确切大小](https://zshipu.com/t?url=https://help.apple.com/app-store-connect/#/devd274dd925)。

我使用了一个简单的图像格式，可以调整大小到两个设置大小，如下所示。

![](https://d33wubrfki0l68.cloudfront.net/1f68031a196b8e4414b5fb50f66868174f5598bc/1220f/images/posts/2020-07-18/images.jpg)

还要确保您的屏幕截图不包含 Android UI 元素或镶边，否则您的应用将被拒绝。

#### 视频（可选）

就像与图像一样，视频大小和持续时间是非常严格的[，因为这里指定](https://zshipu.com/t?url=https://help.apple.com/app-store-connect/#/dev4e413fcb8)。

如果支持 iPad， 您将需要一个视频的两个 iphone 尺寸加上一个额外的大小。视频必须小于 30s 长。

与图像一样，我使用相同的视频，但添加了较高的后栏，以适应两个设置的大小。同样，确保您的视频不包含 Android UI 元素或镶边。

![](https://d33wubrfki0l68.cloudfront.net/63c61c9c99d06eee2132fd783ff33d53176adbe4/b2ea4/images/posts/2020-07-18/wtf.jpg)

另一个额外的事情是， 苹果要求你使用 Safari 和 Osx 10 + 上传视频...说真的， wtf？

只需通过浏览器扩展切换用户代理来[绕过这一点](https://zshipu.com/t?url=https://addons.mozilla.org/en-US/firefox/addon/uaswitcher/)。

### 生成和上传

如果使用 macincloud， 那么你可以手动上传你的内置应用程序到苹果。请按照[此处的 Flutter 部署](https://zshipu.com/t?url=https://flutter.dev/docs/deployment/ios)指南操作，您应该是好。

请注意，在最便宜的 macincloud 实例上构建需要数年（约 20 分钟）。

如果你想自动化你的部署，那么我可以建议[代码魔术](https://zshipu.com/t?url=https://codemagic.io/start/)自动部署你的 iOS 应用程序。他们有一个很好的博客[与有用的指南](https://zshipu.com/t?url=https://blog.codemagic.io/how-to-develop-and-distribute-ios-apps-without-mac-with-flutter-codemagic/)，以帮助您。

我建议您仅在部署自己之后才设置此设置。尝试通过 CodeMagic 生成日志调试问题将让你发疯。另请注意，您每月可获得 500 个免费构建分钟数，但每个生成在免费实例上需要 30-75 分钟。

### 发布新版本

我发现[App Store 连接](https://zshipu.com/t?url=https://appstoreconnect.apple.com/)网站超级不直观， 有时使用。以下是需要注意的一些方面：

*   在可以使用"试飞"屏幕之前，我必须手动更新"试飞"屏幕中的新版本。新版本不适用于测试人员，直到我勾选了每个新版本的一些框。
*   提交新的公共版本时，必须指定生成编号。其 UI 位于"App Store"屏幕的半路上，该屏幕不是最值得发现的地方。

一旦提交您的应用程序将由 Apple 审核。谢天谢地， 他们的审查过程相当不错， 只需要一天左右对我来说。

## 最终想法

尝试在应用商店中部署是迄今为止制作应用最令人沮丧的部分。花了 99 美元， 我得到了一个错综复杂， 记录不好， 设计不好的开发人员经验。此外， 他们强迫你使用 mac 和 idevice 对我来说是疯狂的。

谷歌Play商店也不完美，但苹果认真对待蛋糕痛苦的开发者经验。

