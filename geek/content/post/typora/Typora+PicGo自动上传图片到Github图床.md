---
title: Typora+PicGo自动上传图片到Github图床
author: 知识铺
date: 2021-09-23 15:02:42+08:00

tags: [Typora]
---



以前用Typora写东西，要插入图片url需要手动用PicGo将图片上传到图床，然后把链接粘贴到Typora中。之前重装系统以后也重装了Typora，虽然用PicGo上传图片的流程已经很简单了，但是今天打开发现插入图片可以直接调用PicGo上传到图床，立马就开始折腾了起来。



![image-20210924154451125](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154451125.png)



Typora偏好设置

发现Typora已经给出了很详细的说明了：[Typora上传图片说明](https://links.jianshu.com/go?to=https%3A%2F%2Fsupport.typora.io%2FUpload-Image%2F%23image-uploaders)

## 1. Github 图床

已使用其他图床的可以跳过这一节。

我之前使用的是微博的图床，结果现在挂掉了，因此决定找个比较靠谱的，以前没使用github当图床是觉得不太好，免费存代码已经很厚道了，再占用资源存图片有点过分。不过现在微软收购了github，可以心安理得的吃大户了23333

不过也仅仅适合普通的用户，平时上传的图片不多，对访问速度的要求也不高，要建站的还是用其他的图床吧。

1. 新建一个repositoryepository，名字随便填，记得选 public，否则外链不能访问。

   

   ![image-20210924154510159](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154510159.png)

   new repository

   ![image-20210924154522924](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154522924.png)

   

   new repository

2. 生成token以便PicGo访问，Select scopes时，勾选红框中的就好了，然后点击生成。记得马上将其复制下来，否则等你再次打开时就看不到了。

   

   ![image-20210924154537724](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154537724.png)

   settings



![image-20210924154548973](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154548973.png)

Developer settings



![image-20210924154558555](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154558555.png)

Person access tokens



![image-20210924154608203](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154608203.png)

Generate new token



![image-20210924154616796](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154616796.png)

Generate new token

## 2. PicGo

Typora给出了使用PicGo的两种方式：

- **PicGo-Core (Command line)**
- **PicGo.app (Chinese Language Only)**

并且总结了两者的不同点：

- PicGo应用程序目前仅支持中文。（哈哈哈，听到这个感觉好爽，以前的应用都是只支持英文的）
- PicGo.app提供了一个GUI，因此与CLI版本相比更易于设置。
- 命令行方式更节省计算资源。
- PicGo.app和PicGo-Core使用不同的配置文件，但是可以将PicGo.app的配置文件中picBed键下的json对象复制到PicGo的配置文件中。
- PicGo.app提供其他功能，例如上传历史记录，自动重命名等。

那我就两个都试一下，看看效果如何。先试一下比较简单的应用程序方式。

### 2.1 PicGo.app 方式

到 [PicGo下载](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FMolunerfinn%2FPicGo%2Freleases) 下载 exe 安装包，下载速度有点慢，我是把链接发送到手机用流量下载的。

安装完成后打开，右边图床设置中找到GitHub图床，填写图床信息。其中的仓库名的格式是：`你的用户名/仓库名`



![image-20210924154627949](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154627949.png)

GitHub图床设置



可以选择上传一张图片试一下，一般没啥问题。

然后打开Typora的偏好设置，填写PicGo的路径：



![image-20210924154637965](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154637965.png)

PicGo路径设置

然后重启一下Typora，插入一张图片试试，搞定。





上传测试

### 2.2 PicGo-Core命令行方式



![image-20210924154659325](https://cdn.jsdelivr.net/gh/zshipu/images/image-20210924154659325.png)





