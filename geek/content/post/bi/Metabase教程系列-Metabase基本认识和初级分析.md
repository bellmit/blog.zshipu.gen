---
title: Metabase教程系列-Metabase基本认识和初级分析
date: 2021-10-25 10:12:00
tags: [BI]
---

# Metabase介绍及基础使用

## Metabase概述

> Metabase是基于一个java语言开发的一款开源的数据分析工具，主要通过给公司人员提问题的方式（ps:相对于Metabase中的Question）对数据进行根据自己的需求进行提炼。帮助你把数据库中的数据更好的,多样化的呈现给更多的人。

## Metabase特性

- 基于java语言开发，是一款开源的工具
- 支持多套主流环境，安装运行简单，界面简洁，操作容易上手
- 支持对外共享：镶嵌到APP，iframe框，超链接 数据
- 支持下载：支持json,csv，xlsx格
- 支持简单的预警操作和邮件发送
- 支持数据权限管理和成员添加 支持集合（collection），仪表板（dashboard），question的各种互响组织形式
- 缓存机制，减少对数据库服务器的频繁访问的压力，对于大数据库表可支持自定义时间同步数据

## Metabase基础使用

### Metabase的安装及运行

> - 支持Docker Image，Amazon Web Services，Heroku下安装
> - 支持Mac,Windows,CentOs等所有主流系统下安装
> - 安装依赖程度低，因为基于java语言，所以Metabase的运行需要依赖 jdk编译环境，且jdk版本必须要大于等于1.8版本

#### 在windows下安装启动

> 只需要在官网中下载对应的metabase.jar包，并在windows下运行：java -jar meatbase.jar 服务就会启动起来

```
#输入命令
$：java -jar meatbase.jar
```

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110877.png)

#### 在docker下安装启动

```powershell
#直接输入以下命令即可
`docker run -d -p 3000:3000 -v /mnt/docker_data/metabase:/tmp -e "MB_DB_FILE=/tmp/metabase.db" --name metabase metabase/metabase
```

`

#### 在Metabase运行

Metabase服务器启动成功，打开浏览器，输入对应的地址，例如：192.168.0.1:3000，红色部分是本机的IP，后半部分是Metabase默认的端口：3000.

> ps：初次进入是注册页面，根据步骤完成注册
> ![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110879.png)

### Metabase基本功能

> Metabase整体功能较为简单，主要分为数据源，客户，权限，question,analytics,日志记录等模块做成。就因为功能简单，所以上手容易，是对于初次进行简单数据分析和编程能力弱的不二选择。
> ![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110880.png)

### Metabase支持数据源及图标类型

> Metabase对于数据源的支持也是比较丰富的，例如mysql,mongoDB，Oracle等，基本满足当前较多的公司
> Metabase系统自带提供了比较丰富的图表类型，对于初级数据分析，可以基本适用
> ![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110881.png)

### Metabase数据组织形式

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110882.png)

> 1.Metabase结果组织结构主要基于collection,dashboard,question三个模块构成，所有模块都是基于Our analytics里面
> 2.任何一个question也可以集成到dashboard，也可以归属到collection里面，也可以直接存在于Our analytics中
> 3.任何一个dashboard可以集合到collection里面，也可以存在于Our analytics中
> 4.任何一个collection可以移动到另一个collection里面（ps:形成父子层级），也可以直接独立于Our analytics中
> ![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110883.png)

### Metabase基本流程操作

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110884.png)

#### 1.添加Databases

(1)点击右边setting按钮，Admin
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110885.png)
(2)点击Databases，进入数据源列表，点击Add Database,进行添加数据源
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110886.png)

#### 2.创建Question

> Metabase数据分析，采用的是提问的方式进行对不同类型的数据进行提炼和抽取。目前系统提供了两种Question方式:系统自带（Custom）,客户自定义（Native query）,使用者可以根据自己的要求进行选择，扩展能力比较强![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110887.png)

（1）Custom模式

Custom模式，使用者无需掌握太多的sql能力，系统自带过滤条件方式和函数,分组等，基本能满足简易的数据分析工作，这对于不熟悉sql的人，但又想做数据分析的人员来说，真的是太“卧槽”了。
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110888.png)

（2）Native query模式
相对于Custom模式来说，Native query模式更加的灵活和可扩展性，用户可以通过编写自己的sql，根据自己需求进行展示，而且支持参数化的形式。
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110889.png)
(3)数据展示
目前Metabase图表支持，相对来说还是比较完善的，对于简易的数据分析来说也是比较够用的
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110890.png)

#### 3.加入到集合中

创建完成，我们可以点击右上角的save模块加到对应的集合/仪表盘
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110891.png)

#### 4.集成到仪表盘

dashboard可以集成各种创建的question。图表类型支持拖动，放大缩小，和颜色，字体，中间线，高亮等一些基础设置，非常灵活且方便上手
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110892.png)

#### 5.分享

对于数据分析来说，有时候别人并不需要登陆系统查看对应的数据，客户可能需要将某一个数据进行镶嵌到某个应用上，或者通过一个链接进行，或者集成到iframe中等操作，这些Metabase都可以简单实现
目前Metabase支持3种方式进行分析，可以通过镶嵌到应用，iframe，链接形式进行分析，有没有一种全方位的既视感

(1)点击仪表盘上的Sharing,则可进入分享的选择项
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110893.png)
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110894.png)

#### 6.数据推送

Metabase还可以支持简单的数据推送，通过邮件方式的形式，定时将数据结果传到到对应的人员中
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110895.png)

## 基于Metabase的个人思考

### 什么场景下适合使用Metabase

- 功能测试中，大家有可能涉及各种sql,不同的人接触的模块不一致，当涉及跨个人不熟悉模块，又要了解相关sql,没有一个系统化的方案进行整合，传统的记录到共享文档，又无法实时查看数据，可以通过Metabase的数据组织形式，将所有的sql语句统一整合，划分模块，使用时点击即可运行
- 功能测试人员或者其他客服人员等不熟悉sql，但要快速知道数据的准确消息，则可以通过Metabase的Custom模式，快速上手
- 对应人员需要快速进行简易的数据分析，但是人力资源不足，编程能力欠缺。Metabase作为一款轻量级的数据分析工具，只要一上手，所有功能走一遍，熟练度即可上升到60%左右，作者尝尽人间百态，很难遇见一款如此上手速度快的数据分析系统
- 部署环境，运行简单，依赖第三方程度低，对于环境部署不熟悉的人员来说，Metabase可是你的不二选择
- 如果你的英语水平不高，那么metabase也可以支持汉化版

### Metabase不足

- 自定义不支持钉钉推送（ps:不过可以二次开发，该系统只对数据进行获取，其他功能需要自定义开发
- 数据预警设计不足，如果实际情况可能需要运用到算法进行预警，目前暂时无法支持
- 采用推送模式不支持仪表盘和集合推送，只支持多个question模式
- 图表展示效果基本基于系统自带的效果，不支持某些特定形式的动态交互
- 目前暂不支持组合条件，以及字段和字段的比较
- 不支持跨实例进行操作，对于有时候不同数据存在不同数据库的实例中，metabse不支持这种操作

## 小试牛刀

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zshipu/images/202110261110896.png)



转摘：https://www.icode9.com/content-4-1063587.html

