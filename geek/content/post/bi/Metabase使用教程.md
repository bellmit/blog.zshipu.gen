---
title: Metabase使用教程
date: 2021-10-20 18:00:00
tags: [BI]
---

## **一、写在前面**

概述：Metabase可以帮助你把数据库中的数据更好的呈现给更多人，数据分析人员通过建立一个”查询“（Metabase中定义为Question）来提炼数据，再通过仪表盘（Dashboards）来组合展示给公司成员

优点：1.开源免费

2.工具轻量、安装依赖的环境简单、配置简单清楚

3.容易上手，操作门槛低，不会sql语句也能使用

4.支持对外共享，权限控制

5.Question可以便捷地创建图表，Dashboards界面整洁美观

缺点：1.Question每次只能对数据库中的一张表进行查询,切换数据表已有的查询选项会重置

2.填写了sql语句的sql查询（Native query）模式不能转到点选查询（Custom）模式

3.不能在Metabase中自由转换数据表中字段的属性

4.可创建的图表类型较单一

为什么选择Metabase：

- 免费 Metabase是一个免费的开源工具，并且只要你赋予权限的人都可以自由浏览你的Dashboards，Metabase虽然没有Tableau的功能多、支持的图表丰富，但Tableau使用客户端Desktop要付费，使用TableauServer发表到Tableau Online也要付费，添加可浏览的viewer也要付费(还是按人头收费，权限越高费用越高)， 而我们可能只是需要一个平台展示一些图表给同事看，为次每月要付上百美金的确得不偿失了。

## **二、安装**

```text
wget http://downloads.metabase.com/v0.30.0/metabase.jar
查看Java版本，Java版本要求在1.7以上
java -version
启动jar
java -jar metabase.jar
```

## **三、初始化配置**

1. metabase默认端口是3000，打开链接 http://your_host:3000

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650825.jpg)

2.点击Let't get started,创建一个初始化的admin账户

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650828.jpg)

3.配置邮箱，可以通过邮箱给用户发送通知，邀请新用户，重置密码等

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650829.jpg)


以126邮箱为例：
SMTP HOST:[smtp.126.com](https://link.zhihu.com/?target=http%3A//smtp.126.com/)
SMTP PORT:465
在邮箱个人中心设置选项中开通SMTP功能，设置密码
SMTP SECURITY:SSL

## **四、使用指南**

1. **连接数据库**：依次点击右上角齿轮——Admin——Databases——Add database ，
   选择Database type(我们使用mysql)，按照提示填入数据库信息再点保存即可连到数据库

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650830.jpg)

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650831.jpg)

**2.从建立一个Question-到展示在DashBoards**
好的，现在我有了一个需求，我想在我的DashBoard上看到我们游戏近七天每一天的收入，那么首先我要建立一个Question
点击Ask a question 我们来到如下界面
Custom模式下可以通过点击的方式对数据进行查询、计算和制图
Native query模式下为自定义sql语句查询

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650832.jpg)


（1） 这么简单的需求，Custom完全可以搞定！我们选择Custom，进入到这个界面，在DATA处， 我选择了我刚刚添加好的数据库，再选择了包含我的测试数据的每日收入的数据表;



![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650833.jpg)


（2） 数据表里我的收入是不同地区的不同天的收入，而我希望的是看近七天的分天收入，不同大区求和在一起就好了，所以现在我要用GROUP BY-对数据进行分组，GROUP BY Date

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650834.jpg)


（3） View 模块可以设置我想展示的数据，并且能对数据进行一些简单的计算（计数、求和、求平均、最大值、最小值等等）

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650835.jpg)



（4） Custom Expression 选项可以对一个或多个字段进行计算，并能在第二行命名

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650836.jpg)




（5）我的需求是看近七天的收入，所以我还可以对上面的数据限定下条件“最近七天”，使用FILTERD BY完成

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650837.jpg)


*对字段为数字的筛选条件有：等于、不等、 大于、小于、之间、大于等于、小于等于、空值、非空
对日期为数字的筛选条件有：最近n天、未来n天、今天、某天前、某天后、某天、某天和某天之间、空值、非空*

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650838.jpg)

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650839.jpg)


（6） 条件都选好后点 Get Answer就得到了我们的查询结果

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650840.jpg)


（7）点击右上角的Save,就可以保存我们的Question到DashBoards上啦，可以拖动、缩放你的Question模块，右边的Filter能添加筛选器 包括时间、地点、字段、ID等可筛选项，便于阅读仪表盘的人进行筛选，
保存好dashboard，所有有权限的人就都可以来到这个board里看到近七天收入了

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650841.jpg)


（8）对了，刚刚观察到Table有一个下拉的选项，我们回到Question，试着点下，哦！原来是在这里作图，我们选择条形图，把这个图也添加到我们刚刚的board里是不是能让我们的展示更丰富？
*Question 中可以把处理好的数据转换为图形（线性图、条形图、环形图、散点图、漏斗图、地图），点击右边的齿轮可以对图表的格式进行设置。*

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650842.jpg)

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650843.jpg)


也把它放入Dashboard （仪表盘）中~

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650844.jpg)



3.**举一反三** 现在我想得到一个内容更丰富的日报~ 重复上述操作，可以得到下图了

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650845.jpg)

4.Dashboard可以让更多的人能方便地看到更多的内容，其中的数据会随着数据库而自动更新，所以你日常要做的日报和一些需要重复性处理的实时的简单分析图表，都可以放进Dashboard给大家呈现

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650846.jpg)

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650847.jpg)

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650848.jpg)



5.**Pluses功能**

可以定时将选定的Question 发送至指定邮件，是不是很酷，不用打开电脑就能看今天的最新数据了

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110211650849.jpg)