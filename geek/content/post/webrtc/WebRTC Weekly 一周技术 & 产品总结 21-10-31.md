---
title: WebRTC Weekly 一周技术 & 产品总结 21-10-31
date: 2021-10-30
tags: [WebRTC]
---

### 两年后 Skype Web 版本现在也能在 Firefox 上使用了

Skype 作为 VOIP 鼻祖级别的公司，被微软收购之后反而走向了下坡路， 很多人可能已经忘记了 Skype。微软的 Teams 推出之后， 由于跟 Office 套件的捆绑策略迅速抢占了大量的企业办公协同市场， 就在人们以为微软会放弃 Skype 之后， Skype 终于让他的 web 版本，支持了 firefox。前一段时间甚至传出微软会重新定位 Skype， 主打年轻人。说回为什么 Skype 要支持 web 端，跟苹果终于让 FaceTime 支持 web 端大概思路是一样， 虽然 Web 中 WebRTC 的体验没法跟 native 的体验相比， 但 Web 所具有的一大优势就是不用下载，人人往往低估了这一优势， 个人的看法是当 web 端的功能或者体验能达到 native 的 70% 的时候，人们会积极的拥抱 Web 的版本。

相关链接 https://www.cnbeta.com/articles/tech/1194519.htm [1]

### Edge 浏览器将支持 GeForce Now 服务

自动微软将 Edge 从其自制的 EdgeHTML 引擎切换到 Chromium 之后，对 WebRTC 的支持越来越好， 最近 Edge 浏览器将支持 GeForce Now 服务， XBox 玩家可以把他们的 PC 游戏通过 Edge 浏览器串流到主机游戏上玩， 看起来这个是基于 WebRTC 的局域网云游戏， 好奇他们在局域网下基于 WebRTC 的云游戏可以做到端到端多少毫秒的延迟。值得一提的是，今年 9 月的 Edge 浏览器更新，还添加了对另外一个云服务——谷歌 Stadia 的支持，允许玩家在 Xbox 主机上使用 Edge 浏览器在谷歌 Stadia 上玩游戏。持续关注云游戏的发展。

相关链接: https://hot.cnbeta.com/articles/game/1194311.htm [2]

### iOS 15.1 中的 SharePlay 终于来了

本周苹果推送了 iOS 15.1, 支持了在 WWDC 上重点讲的 SharePlay， SharePlay 可以让用户在进行 FaceTime 通话时，和对方同步观看视频，听音乐，共享屏幕。苹果又利用自己生态的优势 来提升自己产品的粘性， 目前已经看到一些小游戏在尝试使用 SharePlay， 相信后面基于 SharePlay 越来越多的创新玩法会涌现。问题来了，Android 平台会不会跟进类似的玩法， 个人的猜想应该不会，Android 系统没有这样的生态优势。但不妨碍第三方公司会推出类似玩法和体验的跨平台的方案， 但 SharePlay 利用了苹果特有的权限，第三方的实现可能很难达到类似的跨平台的体验。

我们看到体验共享方向的产品越来越多，比如 K 歌体验共享：线下 K 歌可以与朋友对唱，及时听到好友演唱， 在超低延迟的加持下 ，线上 K 歌可以连麦，获得无感知延迟的合唱体验。听歌体验共享：“一起听” 是在线听歌中的新的休闲娱乐模式，让听歌和社交互动完美结合。当两个陌生人配对成功并 “一起听”， 还可以进行实时的语音视频以及其他的互动玩法。观影体验共享：和一起观影的人讨论电影可以增加观影乐趣，新技术驱动下，在线上观影场景中，逐渐产生了更多的共享体验模式。

未来一起 XXX 的产品会越来越多，期待这个方向的创新。

相关链接 1： https://36kr.com/p/1452080810256521 [3]

相关链接 2： https://36kr.com/p/1457374160955264 [4]

### iOS 15.1 Safari 更新：我更强了，但 bug 也更多了

在 iOS 15.0 Safari 的更新中，增加了很多 WebRTC 相关的特性，比如 Insertable stream 的支持，可以用来端到端加密， 屏幕共享的支持， HTTP3.0 的支持， 甚至支持了在浏览器中跟 facetime 互通。但同步也带入了很多 bug，对 WebRTC 影响比较大的是，在 iOS15.1 中 在使用 WebRTC 推流的时候会导致 crash， iOS 15.0 的 safari 中 websocket 如果在服务端开启了压缩，会导致连不上。希望苹果早日修复这些 Bug。

### WebRTC 要实现 SVC 了

其实 WebRTC 很早就支持了 vp9 的 SVC, 但一直只能通过命令行开启，并不能默认打开。后来 SVC 成为 WebRTC 1.0 API 的扩展规范， 现在重要实现完备的 SVC 支持了， SVC 在视频会议场景中非常好用，但也带来了不少问题，比如在移动端你开启了 SVC 可能就要放弃硬件编码， 一个很美好的技术到真正落地的时候总会带着很多遗憾和取舍。

咨询了以为 Intel 给 Chrome 做硬件编解码支持的专家，这次 SVC 的实现也不是那么的完美：

```
“其实是给av1用的 vp9还不理睬这个api 264只会支持L1T2和L1T3。然而av1的硬件编码我只在windows上加了支持，且只会以后支持L1T2和L1T3。除非你只用软件编码”
```

现在让我们静静等待 SVC， 有总好过没有。

相关链接： https://groups.google.com/a/chromium.org/g/blink-dev/c/XzygOFuas2A/m/imTtbDqPBgAJ   [5] (链接在国外，需要梯—子)

### Zoom 给用户带来自动生成字幕等功能

Zoom 现在也面临很激励的竞争，动作很多， 前一段时间也开始下场做 RTC 的 PaaS 服务， 甚至要 147 亿美收购 five9， 但最后收购失败。Zoom 也在不断迭代提升其产品的粘性。最近自动生成字幕能力现在可用于所有免费的 Zoom 账号，目前只支持英文，后续会支持其他的语言， 后续我们跟老外开会再也不怕蹩脚的英文了。所以，腾讯会议啥时候支持上。

相关链接： https://www.cnbeta.com/articles/tech/1194821.htm [6]

PS: 我组建了一个 WebRTC 技术交流的群，基本涵盖了行业内做 RTC 相关的公司的研发伙伴，对于想做技术交流的伙伴可以加我微信 (leeoxiang)，备注 “名字 @公司名字 ” 我拉你进群，仅限技术产品交流。

### References

`[1]` https://www.cnbeta.com/articles/tech/1194519.htm   
`[2]` https://hot.cnbeta.com/articles/game/1194311.htm   
`[3]` https://36kr.com/p/1452080810256521   
`[4]` https://36kr.com/p/1457374160955264   
`[5]` https://groups.google.com/a/chromium.org/g/blink-dev/c/XzygOFuas2A/m/imTtbDqPBgAJ   
`[6]` https://www.cnbeta.com/articles/tech/1194821.htm    

  

