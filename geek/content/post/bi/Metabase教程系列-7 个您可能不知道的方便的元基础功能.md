---
title: Metabase教程系列-7 个您可能不知道的方便的元基础功能
date: 2021-10-24 13:00:00
tags: [BI]
---

Metabase 的界面试图远离您的方式，以帮助将您的数据带到最前沿。这种悠闲的方法意味着有时功能可能需要时间来发现，因此我们整理了一些您可能尚未利用的功能列表。

## 1. 警报：当指标达到某个数字时，会收到通知

有些人错过了问题右下角的菜单（图1）：

![<>图1</他们>。单击问题右下角的铃来设置警报。](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902957.png)*图1。*单击问题右下角的铃来设置警报。

他们不点击铃声，所以他们从来没有发现，你可以设置一个问题，向您发送电子邮件或 Slack 消息的基础上：

- 当时间系列[越过球门线](../Metabase教程系列-获取有关问题的警报).
- 当 a[进度条达到（或低于）其目标](../Metabase教程系列-获取有关问题的警报).
- 当问题出现时[返回结果](../Metabase教程系列-获取有关问题的警报#results-alerts).

![<>图2</他们>。警报的广泛世界。](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902958.png)*图2。*警报的广泛世界。

您可以将问题安排为每小时、每天或每周运行一次。如果结果符合您的标准，Metabase 将向您发送电子邮件或 Slack 消息，告知您。

![<>图3</他们>。设置警报的选项。](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902959.png)*图3.*设置警报的选项。

设置警报后，您可以将注意力集中在别处，直到数据再次需要您的注意力。

要了解更多，请查看[获取有关问题的警报](https://www.metabase.com/docs/latest/users-guide/15-alerts.html).

## 2. 出口结果给CSV、Excel 或 JSON

虽然我们仍在问题的右下角菜单中，但另一个经常被忽视的功能是下载问题结果的能力。

![<em>Fig. 4</em>. Export results as CSV, XLSX, or JSON format.](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902961.png)*图4*。出口结果为 CSV、XLSX 或 JSON 格式。

如果您愿意在 Metabase 中将结果作为问题共享，请查看我们的[共享数据指南](https://www.metabase.com/learn/data-diet/analytics/guide-to-sharing-data.html).

## 3. 现场过滤器：创建智能滤芯小部件

字段筛选器是一种特殊的变量，您可以在 SQL 查询中包含，允许 Metabase 创建有关列中数据的"知道"的筛选器。这意味着在实践中，您可以使用日期拾取器创建筛选器，或者使用预填充选项的下拉菜单。他们需要一点时间才能掌握窍门， 这就是为什么我们写了一个[学习关于现场过滤器的文章](https://www.metabase.com/learn/building-analytics/sql-templates/field-filters.html)，但有经验的用户一直依赖他们。

![<em>Fig. 5</em>. A SQL question with a field filter powering a date picker.](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902962.gif)*图5.*带有现场过滤器的 SQL 问题，为日期拾取器供电。

## 4. 自定义当人们单击图表时会发生什么

![<em>Fig. 6</em>. When in editing a dashboard, select <strong>Click behavior</strong>.](../../../../../images/edit-dashboard-163512369633614.png)*图6.*在编辑仪表板时，选择**单击行为**。

当您将其添加到仪表板时，您可以自定义问题中的点击行为。以下是您的选择：

- [打开元基操作菜单](https://www.metabase.com/learn/basics/questions/drill-through.html).
- [自定义目的地：选择当人们单击图表时会发生什么](https://www.metabase.com/learn/building-analytics/dashboards/custom-destinations.html).
- [交叉筛选：使用图表更新过滤器](https://www.metabase.com/learn/building-analytics/dashboards/cross-filtering.html).

![<em>Fig. 7</em>. The dashboard editing interface when setting up custom click behavior.](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902963.png)*图7*。设置自定义单击行为时仪表板编辑界面。

您甚至可以使用图表中的值来参数化链接。要了解更多，请查看上面列出的文章，以及我们的文档[交互式仪表板](https://www.metabase.com/docs/latest/users-guide/interactive-dashboards.html).

## 5. 笔记本编辑器中的多步骤总结

使用笔记本编辑器时，大多数人会停止选择数据，2） 过滤数据，3） 总结数据。但是，您可以继续：添加过滤、加入和总结的附加阶段，以获得您需要的答案。

![<em>Fig. 8</em>. A question with two steps of summarization to find the average count of orders per month by product category.](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902964.png)*图8*。具有两个汇总步骤的问题，以按产品类别查找每月订单的平均计数。

这为使用笔记本编辑器提供了更多可能性。有关更多，请参阅我们的文章[多层次聚合](https://www.metabase.com/learn/building-analytics/notebook-editor/multi-aggregation.html).

## 6. 使用 SQL 片段共享和重用代码位

您可以将一些 SQL 代码保存为片段，并这样引用它：

```
SELECT 
    product_id
FROM 
    orders 
WHERE 
    total < {{snippet: average order total}}
```

您可以通过单击代码图标在 SQL 编辑器的右侧栏中找到现有的片段。从那里，您可以插入现有的片段，或创建自己的片段。

![<em>Fig. 9</em>. Select the items you want to move, then you can either archive or move them in bulk.](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902965.gif)*图9。*选择要移动的项目，然后您可以存档或批量移动它们。

您还可以突出显示代码的某些部分，以将其保存为片段。请参阅我们的[SQL 片段的完整文章](https://www.metabase.com/learn/building-analytics/sql-templates/sql-snippets.html).

## 7. 保持集合与拖动和下降和批量移动组织

您可以将物品从收集到收集进行拖放。

![<em>Fig. 10</em>. Simply drag and drop items to another collection.](../../../../../images/drag-and-drop-163512370855616.gif)*图10。*只需将项目拖放到其他集合。

您还可以单击项目的图标来选择它，当您想要同时移动或存档一堆问题和仪表板时，您很有用。

![<em>Fig. 11</em>. Select the items you want to move, then you can either archive or move them in bulk.](https://cdn.jsdelivr.net/gh/zshipu/images/202110250902966.gif)*图11。*选择要移动的项目，然后您可以存档或批量移动它们。