
title: NodeJS 初级：管理多个 NodeJS 版本
author: 知识铺
date: 2020-09-15 18:04:02
tags: nodejs
---
 我们都切换不同的项目，有时甚至是每天。每个项目在依赖关系和运行时方面都有自己的要求。幸运的是，NPM 会处理依赖项，但我们仍然需要管理运行时。某些项目可能使用 LTS 版本，而其他项目可能位于边缘，并使用最新版本的节点。

# [](#meet-nvm)<font _mstmutation="1" _msthash="288483" _msttexthash="6386952">满足 NVM</font>

nvm（节点版本管理器）管理多个节点版本，并在它们之间即时切换。
即使您使用单个节点版本，通过 nvm 安装和更新它也容易得多。

# [](#installing)<font _mstmutation="1" _msthash="289081" _msttexthash="5773755">安装</font>

<font _mstmutation="1" _msthash="276809" _msttexthash="37408956">使用此单行安装：</font>

 <code>curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash</code> 

或者查看[GitHub 存储库上的完整说明](https://zshipu.com/t?url=https://github.com/nvm-sh/nvm)

# [](#getting-started)<font _mstmutation="1" _msthash="290277" _msttexthash="4603768">开始</font>

<font _mstmutation="1" _msthash="277953" _msttexthash="134524481">假设我们要安装节点 v14.3.0，这很容易做到：</font>

 <code>nvm install 14.3.0</code> 

只需将 14.3.0 更改为所需的版本。

<font _mstmutation="1" _msthash="290615" _msttexthash="93004444">如果要安装最新的 LTS，请运行：</font>

 <code>nvm install --lts</code> 

<font _mstmutation="1" _msthash="291213" _msttexthash="192989914">安装了几个节点版本后，可以使用 使用命令激活特定版本：</font>

 <code>nvm use 14.3.0</code> 

# [](#global-modules)<font _mstmutation="1" _msthash="305032" _msttexthash="11070579">全球模块</font>

全局模块不在不同的节点版本之间共享。您必须安装每个节点版本的全局依赖项。它可以很烦人， 但它是有道理的。某些依赖项可能与某些节点版本不兼容。

# [](#nvmrc)<font _mstmutation="1" _msthash="305656" _msttexthash="75348">. nvmrc</font>

<font _mstmutation="1" _msthash="292708" _msttexthash="644598253">这是最好的部分！您可以向项目添加 .nvmrc 文件，以准确指定节点版本。
回到我们之前的示例，让我们将节点版本保存到 .nvmrc。</font>

 <code>echo "14.3.0" > .nvmrc</code> 

<font _mstmutation="1" _msthash="290602" _msttexthash="496478736">现在，每次我进入这个目录或它的子目录，我可以运行来激活我的项目的版本。在我们的案例中，它是 14.3.0。</font>```cd``````nvm use```

我甚至可以将此文件提交到 git 存储库，以便其他开发人员也可以使用它。

就是这样！现在，您可以轻松地在项目之间切换，而无需考虑所需的节点版本。👾

