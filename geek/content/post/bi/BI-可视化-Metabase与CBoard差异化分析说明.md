---
title: BI-可视化-Metabase与CBoard差异化分析说明
date: 2021-10-25 10:11:00
tags: [BI]
---

这里的CBoard是在原生态CBoard基础上进行二次开发之后的BI工具，以下内容将其称为Mydata。

## 相似点

1.可以下载查询出的数据。

2.底层均采用java开发。

3.可视化拖拉拽查询方式。

4.均支持二次开发。

5.支持在图表上方进行数值筛选。

6.均支持自定义表达式，Metabase的自定义表达式实现方式可参考本文Metabase使用介绍的自定义表达式部分。

7.界面简洁明了。

8.可视化拖拉拽方式都可以解析为对应的SQL，Metabase的解析说明参考本文Metabase使用介绍部分的可视化操作解析为SQL。

9.支持分享图表。Mydata支持分享看板到不同角色，角色下设用户，Metabase支持分享图表到不同仪表盘，也可以以公共链接的方式分享仪表盘（需要在管理员设置中开启公共分享）。

10.对数据源、数据集、图表及字段均具有权限控制功能，Metabase的权限控制详情可参考本文Metabase使用介绍的权限控制部分。
 11.均支持SQL方式查询，Mydata通过创建数据集的方式实现SQL方式查询，Metabase的查询方式共分为三种，第一种为可视化简单查询，功能单一，第二种为可视化自定义查询，功能相对第一种丰富，第三种为SQL方式查询，可实现可视化无法实现的复杂问题查询，同时其可以设置问题作为子查询，可以保存代码片段反复使用，详细可查看本文Metabase使用介绍的SQL查询部分。

## 不同点

1.图表的层级表达不同，Mydata的一级为看板，下设文件夹或看板，其中文件夹下方又可设置子文件夹或看板，而Metabase的一级为集合，下设集合或仪表盘，其中集合下面又可设置子集合和仪表盘，仪表盘中设置问题（也就是图表）。

2.字段中文描述在可视化查询中的作用不同，Mydata可以实现批量导入中文字段名称，在可视化时使用中文字段查询，而Metabase的中文字段需要一个一个手输，且可视化查询过程中也没有显示中文名称，依旧是英文字段，不便于业务人员的操作。

3.告警方式不同，Mydata有企业微信告警功能，Metabase为邮件告警，可以将看板数据定时发送到邮箱，也可以设置阈值，当看板查询值达到阈值，发送邮件，但标准版版本没有阈值告警功能，企业版本中有，详细可参看本文Metabase使用介绍的告警部分。

4.可接入数据源不同，Mydata现有支持的常用数据源Mysql、ElasticSearch，Clickhouse中，Metabase不支持ElasticSearch，其支持数据源参考本文Metabase使用介绍的数据源部分。

5.是否支持可视化关联查询，Mydata暂时不支持可视化关联查询，可通过在数据集中设置表的关联关系进行关联查询，Metabase支持可视化关联查询，二者均不支持跨库的关联查询。

6.是否具有数据集数据的全面快速分析功能，Mydata只能手动查询查看各表的数据情况，而Metabase有X-rays透视功能，可一键查看该数据集的各维度统计数据，详细参考本文Metabase使用介绍的X-rays透视部分。

7.是否可设置图表的点击行为，Mydata对图表的点击无功能设置，而Metabase可设置图表的点击行为，详细查看本文Metabase使用介绍的仪表盘问题的点击行为部分。

8.子查询的使用方式不同，Mydata可以设置子查询为一个数据集，在此数据集基础上进行查询，而Metabase可以在问题（图表）查询结果基础上直接编辑新问题，详细查看本文Metabase使用介绍的查询结果作为子查询部分。

9.刷新机制不同，Mydata可设置定时，或按某频率（每小时等）更新，而Metabase没有定时更新，只能按照某频率（每几分钟或每小时）更新。

10.是否为本土化框架，Mydata为国内CBoard框架发展而来，Metabase为美国某公司开发框架

# Metabase使用介绍

## Metabase的安装与启动

### 安装

Metabase默认没有配置ClickHouse数据库，需要加载第三方驱动配置，配置方式参考：

[https://github.com/enqueue/metabase-clickhouse-driver](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fenqueue%2Fmetabase-clickhouse-driver)

[https://www.metabase.com](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.metabase.com)/

这里采用jar包方式安装，也可以采用Docker方式安装。

### 启动

启动metabase方式，进入目录/data/work/metadase，执行以下命令，参数DMB_JETTY_PORT表示指定浏览器访问端口为3300，默认为3000，参数DMB_PLUGINS_DIR表示指定插件路径，主要用于加载Clickhouse的驱动：java -DMB_JETTY_PORT=3300 -DMB_PLUGINS_DIR=./plugins -jar metabase.jar

浏览器打开访问链接[http://ipAddress:3300/](https://links.jianshu.com/go?to=http%3A%2F%2FipAddress%3A3300%2F).

## Metabase特性说明

### 1.支持的数据源

- Amazon Redshift
- Druid
- Google Analytics
- Google BigQuery
- H2
- MongoDB
- MySQL
- Oracle
- PostgreSQL
- Presto
- Snowflake
- SparkSQL
- SQL Server
- SQLite
- Vertica

### 2.X-rays透视

X-rays透视图，可以实现对表数据的全面快速分析。

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031025.png)





### 3.自定义表达式

自定义表达式，包括简单的加减乘除，条件判断等，可使用的表达式查看如下链接，其中对时间相关字段值的限定，如[create_date] > "2021-01-01"，这里的字段create_date使用中括号表示变量。

[https://www.metabase.com/docs/latest/users-guide/expressions.html](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.metabase.com%2Fdocs%2Flatest%2Fusers-guide%2Fexpressions.html)

### 4.权限管理

- 权限设置单一，只有访问权限
- 实现对数据源、数据表、集合、仪表盘、问题（图表）、字段等权限控制，
- 使用角色权限管理方式，管理权限。

### 5.仪表盘中问题（图表）的点击行为

仪表盘编辑时每个问题都有点击行为设置，可以设置到链接到一个url，仪表盘或问题，或更新仪表盘过滤器.如下点击第二个问题，就可转到对应设置的另外一个问题。

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031026.png)



![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031027.png)





### 6.查询结果作为子查询

这里操作的前提是该问题的点击行为设置为打开操作菜单，在问题的某维度数据上直接点击就会弹出不同维度数据统计选项，其中查看这个New Total……表示该维度的全部数据（这里表示商品分类为3的底层全部数据），分类表示选择该表的其他维度字段进行分类聚合统计，时间表示选择该表的时间字段进行分类统计，透视表示对商品分类为3的全部数据全面快速分析，和其余的比较表示和其他商品分类的数据以各种不同维度统计对比数据，编辑完成需要的话可以保存为新的问题。

![image-20211026093909581](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031029.png)





### 7.可视化操作解析为SQL

查看可视化拖拉拽制作后对应的SQL

![image-20211026093932438](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031030.png)



### 8.SQL查询

#### 8.1 引入变量

允许引入变量，在筛选框中输入变量值查询。

![image-20211026093949990](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031031.png)







```sql
#如下变量设置方式表示month变量值不可缺少，必须指定，
select * from user_active_month_model where month = {{month}}

#如下方式表示month变量值可不填写，或设置为默认;
select * from user_active_month_model [[where month = {{month}}]]
#如下方式可以实现多重变量查询，同时变量值可填写可不填写，或设置为默认。
select * from user_active_month_model where 1 [[and month = {{month}}]] [[and pc_active = {{pc_active}}]] 
#同时，变量名可以随意命名，不一定为筛选字段名
```

#### 8.2 问题作为自查询

以一个问题作为子查询。

![image-20211026094009619](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031032.png)



```sql
# #之后会弹出侧栏问题选项，选择问题作为查询数据表
select * from {{#}}
```

#### 8.3 sql代码片段

![](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031033.gif)







![](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031034.gif)

### 9.告警功能

可以设置将图表查询数据发送到邮箱，需要在每个查询图表设置告警。按照官网文档，企业版本可以设置阈值/目标值，当达到阈值时进行告警。

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031035.png)



![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031036.png)





或者在这里设置：

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031037.png)



![image-20211026103111169](https://cdn.jsdelivr.net/gh/zshipu/images/202110261031038.png)





注意时区要设置为本地时区，这里采用Asia/HONG_KONG的时区，该时区与北京时间保持一致。



作者：大数据faner
链接：https://www.jianshu.com/p/f3536e408180