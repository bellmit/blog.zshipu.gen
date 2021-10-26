---
title: BI-ETL-在10分钟内掌握Apache Airflow
date: 2021-10-24 19:44:00
tags: [BI]
---

## 介绍

一个pache 气流是用于协调复杂工作流和数据处理管道的开源工具。它是一个平台，以编程方式安排和监控预定工作的工作流程。

Apache 气流使您的工作流程简单、井然有序、系统化，因此可以根据要求轻松编写和安排时间。

![img](../../../../../images/1FJsMPN5kPMI7JuqhsaP7rA.png)

**让我们从基础知识开始。**

**我们所说的工作流程是什么意思？
**工作流程可以是您的简单计算，创建基础架构，在数据库中执行一些查询，bash 命令，巨蛇脚本，MySQL 查询，蜂巢查询等。
工作流被分成一个或多个任务，相互关联并形成**DAG（**定向循环图）。

**什么是 DAG？
**简言之，DAG 是所有小任务的集合，这些小任务将协同在一起执行一项重大任务。

![img](../../../../../images/1l2rG8ILtIrQl-h9JMbq4Bg.png)

还是， 困惑？让我们举一个更好的例子。

**让我们通过编译器的阶段来理解这一点。**

对于那些不知道编译器的阶段的人 - 将其视为一个过程，然后由您的编译器将高级语言转换为低级语言（您的机器理解）

这就是编译代码后发生的情况。我们的代码被转换成字符流，词汇分析仪将其转换为令牌，然后语法分析仪将其转换为语法树，然后语义分析仪、中间代码生成器、代码优化、目标装配代码。在这里，每一步都非常关键，非常依赖于以前的步骤。
任何一个步骤中的错误都无法成功编译我们的代码。

这些步骤在 DAG 中会是什么样子？

下面是一些 DAG 的图表

![img](../../../../../images/1NCJL_QPs9eI9e8r9P1g3HQ-1635147516024116.png)

![img](../../../../../images/1NCJL_QPs9eI9e8r9P1g3HQ.png)

如果您的任务依赖于其他任务，您可以根据您的要求设置依赖项。我们将在开始与Apache Airflow时简短地讨论这个问题。

**预定的工作是什么？**

假设您的工作流程必须每周日运行，您可以安排它的方式，它只会在星期日触发。这有多酷？
简单地说，您可以自动实现工作流程。自动化最好的部分是您可以避免未来的人为错误。
您的 DAG 可以轻松监控、控制和触发。

**如果你的工作流程出现故障怎么办？如果成功完成怎么办？如果完成的时间超过预期，该怎么办？**

那么，记住所有这些事情，Apache Airflow已经给出了这样的功能，如如果你的工作流程失败，你可以设置它作为发送电子邮件警报，松弛通知所需的人/团队。
当 DAG 运行成功时，您也可以将其设置为发送电子邮件。
如果您的任务成功运行，但时间超过预期，该
怎么办？（在实际情况下，这是一个问题） - 为此，您可以设置您的 SLA。假设您的 SLA 时间为 600 秒。但是你的任务花了900秒是不是出问题了？如果发生这种情况，它会触发所需的团队

**Apache Airflow的优势**

Apache Airflow有相当多的优势，这使得它比市场上的其他工具更好工具。
首先，我们将讨论它的优势，然后使用气流在其他类似的工具的一些好处。

- **开源 / Python**气流是在 Python 中开发的，设计工作流非常容易。您可以在开源中贡献插件，还可以根据您的要求使用其他插件。
- **监控**- 一旦运行任务状态，您可以轻松地监控它。气流提供每个任务的所有必要细节，如执行时间、着陆时间、日志等。
- **可扩展**- 大多数数据驱动的公司都喜欢使用气流，因此工作流的复杂性将随着前进而增长。但气流比其他工具具有优势，因为它更具可扩展性。
- **智能调度**- 您可以根据需要安排任务。例如，如果您想安排您的任务，每周日下午 4：00 运行，您可以执行。
- **管理依赖性**- 使气流比所有其他工具更好的很酷的功能之一是适当管理依赖性。如果任务 t2 依赖于进一步依赖于任务 t0 的任务 t1，则可以设置整个任务的依赖性。
- **弹性**- 所有工作流程工具有时行为意外，可能是任何原因，如网络问题，人为错误，需要比预期更长的时间，等等。气流有几个功能，如重试。如果任何机会，您的任务未能执行，气流在一分钟后将其停用（如果由于其他原因（如网络问题）而失败，则重试可能会使该任务成功）。
  它甚至通过电子邮件/松弛向团队发出警报信息。
- **提醒**- 这是气流中最酷的功能之一，如果您想要您的团队收到通知，如果您的任何任务失败，它将通过邮件通知，松弛通知。
  即使您的任务成功，您可能也希望得到通知，气流也有此功能。
- **服务级别协议 （SLA） 超时**：这可能是气流提供的最关键功能之一（至少对于某些公司来说是如此）。如果你的任务通常需要500秒才能完成，但是有一天，你花了1500秒，你不觉得发生了意想不到的事情吗？
  你不想得到通知吗？您可能有自己的理由存储这些记录，也许是为了分析目的或任何其他研究工作。
  示例：假设您的公司在一天结束时收集用户注册数据，但您已经注意到，每个星期六您的任务需要很多时间，这意味着周六的人会更多地参与。
- **用户界面**- 它有一个很好的UI，这使得它更平易近人为用户。您可以在格式良好的树结构中查看任务，您可以在 UI 中查看日志详细信息、气流数据库、任务持续时间、提单时间、丰富的图形视图。

![img](../../../../../images/11mnjl5D-WphcmJvn7gxDIg-1635147516031119.png)

![img](../../../../../images/11mnjl5D-WphcmJvn7gxDIg.png)

![img](../../../../../images/11a_p_5vuuq27-HMv04L33Q.png)

![img](../../../../../images/11a_p_5vuuq27-HMv04L33Q-1635147516051126.png)

- **插件和挂钩**- 气流有各种预定义的插件，也用户定义的插件，这使得您的任务容易。
- **自定义插件，钩，传感器**- 我会回到你关于这些关键字，如插件钩传感器，等等。简言之，我们可以使我们自己的操作员在气流中操纵它工作，因为我们喜欢它的行为。
- **云服务**- 云平台，如谷歌云显示其支持气流。云作曲家 - 是一个谷歌服务， 在谷歌云中创建一个Apache Airflow的环境。您可以执行几乎所有内容，并使用云服务，如 Google BigQuery、数据程序、数据流等。

**动手怎么样？**

我将使用云作曲家（基于 GCP 的托管服务）创建气流环境。我们还可以创建本地环境。
一旦创建云作曲家，它就会自动在云存储中创建一个存储桶，最终与您的作曲家环境一起安装。同样，当您将安装到本地环境中时，您将具有相同的目录结构。

![image-20211025153953111](../../../../../images/image-20211025153953111.png)

在 DAG 文件夹中，您需要上传所有将呈现到气流服务器并在 UI 中显示的 Python 脚本或 DAG，然后您可以手动触发它，或者如果计划好，它会自动触发。

下面是示例代码！

```
from datetime import datetime
from airflow import models
from airflow.operators.bash_operator import BashOperator

yesterday = datetime.datetime.combine(
   datetime.datetime.today() - datetime.timedelta(1),
   datetime.datetime.min.time())

default_dag_args = {
    'start_date': yesterday,
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': datetime.timedelta(minutes=5),
    'project_id': models.Variable.get('gcp_project')
}

with models.DAG(
        ‘Bash_operations’,
        schedule_interval=datetime.timedelta(days=1),
        default_args=default_dag_args) as dag:


t1 = BashOperator(
	task_id=’Make directory’, bash_command=’mkdir folder_name’, dag=dag)


t2 = BashOperator(
	task_id=’delete directory’, bash_command=’rm -rf folder_name’, dag=dag)

t1 >> t2   # This is how we set dependency among two tasks
```



让我们逐行了解此代码。

```
from datetime import datetime
from airflow import models
from airflow.operators.bash_operator import BashOperator
```

这些是我们在 DAG 中使用的设施的进口报表。由于我们正在使用，我们需要从气流库导入巴舍拉。`BashOperator`

```
default_dag_args = {
 ‘start_date’: yesterday,
 ‘email_on_failure’: False,
 ‘email_on_retry’: False,
 ‘retries’: 1,
 ‘retry_delay’: datetime.timedelta(minutes=5),
 ‘project_id’: models.Variable.get(‘gcp_project’)
}
```

这些是默认参数，我们可以通过将参数设置为每个任务的构造器来为每个任务设置。我们可以定义一个默认参数字典，我们可以在创建任务时使用这些参数。

**Start_date，**因为昨天意味着一旦它加载到服务器就开始了。我们可以随时设置它。

**Email_on_failure**为"虚假"，如果是真的，如果任何特定任务失败，它会向指定人员/团队发送电子邮件。

**重述**为 1 表示任务失败后的重述数量。

**Retry_delay**被设定为 5 分钟意味着，在任何特定任务失败后，它应该等待整整 5 分钟才能开始重试。

**Email_on_retry**为假，如果这是真的，那么在任务失败后，每次重试后，它会发送电子邮件给指定的人/团队。

在 DAG 中，一切都以操作员的身份工作。
`Example t1=SomeOperator(arguments)`

我们在本示例中使用 Bash 操作员。

```
t1 = BashOperator(task_id=’Make directory’,bash_command=’mkdir folder_name’,dag=dag)
```

**t1**是一种值，它调用**BashOperator**类，并将所有所需的参数发送到该类。
每个任务都有**一个task_id**它根据您正在使用的操作员对任务进行唯一定义，并具有其他所需的参数。

在我们的 DAG 中，我们运行两个不同的任务，例如，一个是**创建**目录，另一个是**删除**目录。
因此，其明显的**t1**必须在**t2**之前运行，因此我们设置了依赖性，例如 t1 必须在任务 t2 之前运行。`t1 ``t2`

**有两种方法可以确定依赖性：**

- `t1 >> t2`（这意味着 t1 将在 t2 之前运行）
- `t1.upstream(t2)`（这也意味着与上述相同）

反之亦然，语法是这样的：

- `t1 << t2`
- `t1.downstream (t2)`

最后，我们需要将我们的.py文件放入 DAG 文件夹中，然后它会自动加载到服务器中。

![img](../../../../../images/1f3ZpmMlkewJoKRrrGTZ68g-1635147516031120.png)

![img](../../../../../images/1f3ZpmMlkewJoKRrrGTZ68g.png)

您可以将任务图视图视图为：

![img](../../../../../images/1X6EVEglrc4rxi-FfFrOheA-1635147516051124.png)

![img](../../../../../images/1X6EVEglrc4rxi-FfFrOheA.png)

箭头表示依赖于 。`make_directory ``delete_directory`

嗯，这是一个非常简单的例子，说明我们如何创建任务和运行工作流程。

# 工作流

当 DAG 描述如何运行工作流时，操作员会确定实际完成的操作。

操作员描述工作流程中的单个任务。操作员通常是（但并不总是）原子的，这意味着他们可以独立站立，不需要与任何其他操作员共享资源。

注意：如果两个操作员需要共享信息（如文件名或少量数据），您应该考虑将其合并为单个操作员。如果它绝对无法避免，气流确实有一个功能，为运营商交叉通信称为[XCom。](https://airflow.apache.org/docs/1.10.1/concepts.html?highlight=xcom)

气流为许多操作员提供其中的一些操作员，包括：

- `BashOperator `（我们刚才看到）
- `PythonOperator `- 用于调用 DAG 中的任何巨蛇功能
- `EmailOperator `发送电子邮件
- `SimpleHttpOperator `- 发送 HTTP 请求
- `MySqlOperator`， ， - 执行 SQL 查询。`SqliteOperator``PostgresOperator``OracleOperator``JdbcOperator`

# 传感器

传感器是一种特殊的操作员类型，一直运行在场景后面。传感器类是通过扩展创建的。`BaseSensorOperator`

它有一个戳法，它执行任务一遍又一遍后，每隔poke_interval秒，直到它返回真，如果它返回错误，它会再次调用。

**示例：**传感器，以检查文件是否存在于指定目录中。每次poke_interval后，传感器类的戳法将被执行，如果文件不存在，它会发送**假**，一旦文件出现在目录中，它将返回**真**。

# 触发规则

所有操作员都有一个trigger_rule论点，该参数定义了生成任务触发的规则。默认值是，并且可以定义为"当所有直接上游任务都成功时触发此任务"。此处描述的所有其他规则都基于直接父级任务，并且是创建任务时可以传递给任何操作员的值：`trigger_rule``all_success`

- `all_success`： （默认） 所有父母都成功了
- `all_failed`：所有父母都处于失败或upstream_failed状态
- `all_done`： 所有父母都完成了他们的处决
- `one_failed`： 火灾， 只要至少有一个父母失败， 它不等待所有的父母做
- `one_success`： 一旦至少有一个父母成功， 它不等待所有的父母都做
- `none_failed`：所有父母都没有失败（失败或upstream_failed），即所有父母都成功或被跳过
- `dummy`： 依赖只是为了显示， 触发立即
  查看有关[触发规则](https://airflow.apache.org/docs/stable/concepts.html#trigger-rules)的更多信息

## 您想知道两个操作员是如何相互沟通的吗？

Apache Airflow提供一种称为"气流"的功能`XCom`

# XCom （交叉 + 通信）：

两个操作员之间的通信。如果任何操作员返回某些值，它会存储在 xcom 中，气流提供了一种机制，用于拉取 xcom 值，并在其他操作中使用它，并推动价值使用。`xcom_pull()``xcom-push()`

**示例：**查看 GitHub [**Xcom_example.py**](https://github.com/iAshishHere/Apache-Airflow/blob/master/Xcom_example/Xcom_example.py)**中的**代码

让我们通过在市场上列出其他替代工具来结束本文。

- Cron
- Apache Oozie
- Luigi
- Azkaban

既然你已经了解了 DAG 是什么，这里有一个建议给你

![img](../../../../../images/1-mvQD87V7cNUW9SaDWbBRw-1635147516050123.png)

![img](../../../../../images/1-mvQD87V7cNUW9SaDWbBRw.png)

图片信用

[**Airflow Documentation**](https://airflow.apache.org/)
[**Apache-Airflow GitHub**](https://github.com/airflow-plugins)
[代码](https://github.com/iAshishHere/Apache-Airflow)

