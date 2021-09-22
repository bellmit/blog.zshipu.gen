
---
title: SSH - 配置
author: 知识铺
date: 2021-03-04 20:30:08+08:00
tags: []
---
# [](#ssh-commands)<font _mstmutation="1" _msthash="288184" _msttexthash="5724407">SSH命令</font>

<font _mstmutation="1" _msthash="275951" _msttexthash="850379426">生成 ssh-key 运行终端
中的命令，然后重命名您的密钥或键输入，以继续使用通用给定名称，该名称id_rsa用于私钥，id_rsa.pub 用于公共密钥</font>

```
ssh-keygen -t rsa
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1006096" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1006642" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="276523" _msttexthash="12529400">添加标识</font>

```
ssh-add /home/user/.ssh/id_rsa
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1006720" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1007266" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

## [](#add-the-identity-to-github)<font _mstmutation="1" _msthash="289952" _msttexthash="31448924">将标识添加到吉图布</font>

* * *

```
cat /home/user/.ssh/id_rsa.pub
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1007968" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1008514" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

如果 ssh 键是针对 GitHub 的，请转到设置查找 ssh 键和 gpg 键，并在此处运行 Cat 命令后粘贴复制的键。那你就完了现在，您可以使用密钥访问您的 GitHub。

## [](#server-key)<font _mstmutation="1" _msthash="303745" _msttexthash="15684422">服务器密钥</font>

* * *

<font _mstmutation="1" _msthash="291213" _msttexthash="279756893">如果密钥是服务器密钥，则使用根密码进入服务器，并在根中运行以下命令。</font>

```
mkdir /home/user/.ssh

touch /home/user/authorized_keys

sudo nano /home/user/authorized_keys
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042847" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043406" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291811" _msttexthash="73208590">在本地计算机上运行以下命令：</font>

```
cat /home/user/.ssh/id_rsa.pub
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043497" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044056" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="292409" _msttexthash="2117065314">这将给你的公众，你复制和粘贴到authorized_keys文件后，Sudo纳米命令打开文件。ctr +x，你会被提示，如果你想保存的文件类型'Y'为是，然后进入保存。现在通过键入退出退出服务器，然后按下文示向服务器显示：</font>

```
ssh user@134.565.56.31
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044147" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044706" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

用您的 IP 用用户名和 IP 地址替换用户，它应该在无需密码的情况下自动将您放入服务器。

## [](#disable-root-password-login-for-the-server)<font _mstmutation="1" _msthash="304044" _msttexthash="46160335">禁用服务器的根密码登录</font>

<font _mstmutation="1" _msthash="290901" _msttexthash="82282057">在bash终端中键入以下命令以打开文件</font>

```
sudo nano /etc/ssh/sshd_config
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042509" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043068" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291499" _msttexthash="136077409">之后导航到类似于下面的部分，并将"是"更改为"否"。</font>

```
#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxAuthSessions 10
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043159" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043718" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

将选项更改为无 CTR + x 后，将显示"Y"类型，然后输入以保存新文件的提示。

<font _mstmutation="1" _msthash="292396" _msttexthash="128147435">通过键入下面的命令重新加载已保存的文件，</font>

```
sudo systemctl reload sshd
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044134" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044693" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

然后你做没有人可以ssh使用根密码到您的服务器。这主要是为了防止蛮力攻击您的服务器。

# [](#adding-an-sshkey-into-your-server)<font _mstmutation="1" _msthash="303758" _msttexthash="21067189">在服务器中添加 SSH-KEY</font>

<font _mstmutation="1" _msthash="290888" _msttexthash="1168796798">当您希望能够访问其他命令（如 git 克隆或从 Github 或 GitLab 中提取）时，您将主要这样做，而不会每次都提示密码。
首先，确认在服务器中创建的用户拥有 ssh 文件。</font>

```
ls -la
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042496" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043055" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

然后查找ssh文件

_埃德温埃德温 807 九月 7 11：09 .配置文件
2 根根.ssh_

<font _mstmutation="1" _msthash="292084" _msttexthash="1501674811">正如你可以看到我的文件是拥有的根，因此，如果我尝试生成任何ssh键，我会得到一个权限拒绝错误。我必须将所有权从根部更改为创建的用户。我通过在终端中运行下面的命令来做到这一点。</font>

 ```
 sudo chown -R edwin:edwin /home/edwin
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1043796" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044355" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

如果您再次运行**ls-la，**您将注意到ssh文件将所有权从根切换到当前用户。即我的现在是_埃德温·埃德温。_

<font _mstmutation="1" _msthash="292981" _msttexthash="105957657">完成此任务后，您可以在终端中运行：</font>

```
ssh-keygen -t rsa
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044771" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045330" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

如果您不需要此文件类型，您将获得文件路径的提示，否则，键入相同的路径。即/家庭/_用户_/。ssh/id_rsa_github。
然后键入输入并输入一个密码，这只是为了一些额外的安全性，或者你可以跳过这一步，只需再次按下输入，直到你看到下面的怪异数字。
密钥的随机图图像是：

```

+---[RSA 3072]----+|。
+ |
|._。o.|
|奥埃|
|o_[B]*|
|•斯博*|
|o*+哦|
|o+。o|
|.o=。.|
|.+o |
[----[SHA256]-----]

```

<font _mstmutation="1" _msthash="292669" _msttexthash="14619826">运行：</font>

```
eval `ssh-agent -s`
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1044433" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1044992" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="293267" _msttexthash="12516036">然后：</font>

 ```
 ssh-add /home/*user*/.ssh/id_rsa_github
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1045083" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1045642" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>

<font _mstmutation="1" _msthash="291161" _msttexthash="335454834">这将添加身份猫id_rsa_github. pub 或任何你命名你的公共钥匙通过运行下面的命令。</font>

```
cat /home/*user*/.ssh/id_rsa_github.pub
```

 <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on" _msthidden="1"><title _msthash="1042795" _msttexthash="419224" _msthidden="1">Enter fullscreen mode</title></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off" _msthidden="1"><title _msthash="1043354" _msttexthash="385177" _msthidden="1">Exit fullscreen mode</title></svg>


