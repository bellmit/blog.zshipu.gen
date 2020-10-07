
title: Docker实战：从 Web 应用程序到 Docker 映像，到使用 Kubernetes 部署
author: 知识铺
date: 2020-10-07 18:43:59
tags: 
---
 # [](#from-a-java-application-to-a-kubernetes-deployment)<font _mstmutation="1" _msthash="288483" _msttexthash="50704368">从 Java 应用程序到 Kubernetes 部署</font>

在本教程中，我们将从**Java Web 应用程序开始**，创建**包含应用程序**内部的 Docker 映像，然后在本地**Kubernetes**群集上部署映像。本指南显示从编译 Web 应用程序到在 Kubernetes 上运行它的所有必要步骤。虽然有很棒的开源工具可以执行所有这些步骤，但我们将手动执行命令行**上的每一步**。

[![Pipeline for typical cloud deployment](https://res.cloudinary.com/practicaldev/image/fetch/s--DrcM3_41--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/5qlfmbeebcjuc8jji3t2.PNG)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--DrcM3_41--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/5qlfmbeebcjuc8jji3t2.PNG)

[Kubernetes](https://zshipu.com/t?url=https://kubernetes.io/)是一个用于在群集上部署容器化应用程序的系统。它允许将创建 Web 应用程序的问题与在服务器上运行它的问题分开。在 Kubernetes 群集上运行的实体通常是容器化应用程序，如[Docker](https://zshipu.com/t?url=https://www.docker.com/)映像。

<font _mstmutation="1" _msthash="277095" _msttexthash="2977320866">对于本教程，您将使用 和 （Kubernetes） 命令行工具。这两个工具都可以通过[Dock桌面工具安装](//docs.docker.com/install)。作为本教程的一部分，您将安装 Docker 工具，这样您就可以在计算机上发出与本教程中所述相同的命令。在本教程结束时，您将在您自己的 Kubernetes 群集上部署一个 Web 应用。😊</font>```docker``````kubectl```

# [](#running-the-web-application-on-your-os)<font _mstmutation="1" _msthash="289978" _msttexthash="59448701">在操作系统上运行 Web 应用程序</font>

我们要使用的 Web 应用程序是 Java Spring Boot启动 Web 应用程序。为简单起见，我们将使用官方[春靴](https://zshipu.com/t?url=https://spring.io/guides/gs/rest-service/)教程中的简单现有应用程序。此 Web 应用是一个 REST 服务，公开一个 HTTP GET 终结点。

<font _mstmutation="1" _msthash="277953" _msttexthash="687720657">作为本节的先决条件，您需要[Git](https://zshipu.com/t?url=https://git-scm.com/) [、JDK（Java](https://zshipu.com/t?url=https://www.oracle.com/java/technologies/javase-downloads.html) 8 或更新版本）和[Maven](https://zshipu.com/t?url=https://maven.apache.org/download.cgi)。首先，首先下载 Java 项目，然后使用 Maven 编译它：</font>

 <code>$ git clone https://github.com/spring-guides/gs-rest-service.git
$ cd gs-rest-service\complete
$ mvn clean package
$ cp target/rest-service-0.0.1-SNAPSHOT.jar ../..
$ cd ../..</code> 

<font _mstmutation="1" _msthash="290316" _msttexthash="363031760">第三个命令编译 Java 应用程序，并在 JAR 文件中打包 Web 应用程序。您可以在文件夹中找到 JAR 文件。</font>```target```

<font _mstmutation="1" _msthash="290615" _msttexthash="114617815">接下来，您可以使用以下命令运行 Web 应用：</font>```java```

 <code>$ java -jar rest-service-0.0.1-SNAPSHOT.jar</code> 

<font _mstmutation="1" _msthash="291213" _msttexthash="530476830">您将在终端上看到大量线路飞过，告诉您 Spring-应用程序上下文将初始化，您的应用程序在端口 8080 上公开：</font>

  <code>.   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.2.RELEASE)

2020-03-26 20:56:13.857  INFO 18504 --- [           main] c.e.restservice.RestServiceApplication   : Starting RestServiceApplication v0.0.1-SNAPSHOT on Philipp-PC with PID 18504 [...]
[...]
2020-03-26 20:56:17.477  INFO 18504 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-03-26 20:56:17.481  INFO 18504 --- [           main] c.e.restservice.RestServiceApplication   : Started RestServiceApplication in 4.834 seconds (JVM running for 5.736)</code> 

<font _mstmutation="1" _msthash="291811" _msttexthash="964247427">您可以通过使用 GET 方法调用 REST 服务来验证 Web 应用程序是否正常运行。在您最喜爱的 Web 浏览器中，导航到[URL：http://localhost:8080/greeting](https://zshipu.com/t?url=http://localhost:8080/greeting)。您可以看到以下消息：</font>

 <code>{"id":1,"content":"Hello, World!"}</code> 

# [](#introduction-to-docker-images)<font _mstmutation="1" _msthash="305656" _msttexthash="18133219">码头图像简介</font>

确保安装了 Docker 桌面工具。你可以在这里找到所有的安装[说明](//docs.docker.com/install)。

Docker 属于 PaaS 类别（平台即服务），它是开源的。简单地说，Docker 在容器中运行应用程序（如我们的 Web 应用程序）。容器与外部世界隔离，包含**操作系统、****要运行**的应用程序及其所有**依赖项**。Docker 工作流如下所示：

*   从包含操作系统和常用依赖项（如 JDK 或 Python）的基本映像开始。
*   将您自己的应用程序添加到基本映像。还要添加不是基本映像一部分的所有依赖项。
*   输出是一个自定义图像，我们的应用程序里面。
*   在映像内运行应用程序。

# [](#build-and-run-a-docker-application)<font _mstmutation="1" _msthash="304083" _msttexthash="45863974">生成并运行 Docker 应用程序</font>

<font _mstmutation="1" _msthash="291200" _msttexthash="1654580772">Docker 图像是分层的：每个图像都通过添加更多实体构建在另一个映像上。为了使图像创建过程更加透明，我们使用 Docker 文件。此 Docker 文件包含有关如何创建 Docker 映像的所有信息。创建具有以下内容命名的文件：</font>```Dockerfile```

 <code>FROM openjdk:8-jre-alpine
COPY rest-service-0.0.1-SNAPSHOT.jar /my-app.jar
CMD java -jar /my-app.jar</code> 

在第一行中，我们指定包含 Java 8 运行时环境的基本映像。下一行，我们将 Web 应用程序复制到映像中。最后一行，我们描述当映像作为 Docker 容器运行时会发生什么：我们的 Web 应用程序被执行。

<font _mstmutation="1" _msthash="292097" _msttexthash="152381476">现在，让我们使用 Docker 文件创建我们自己的映像：</font>

 <code>$ docker build -t my-app:0.0.1 .</code> 

<font _mstmutation="1" _msthash="292695" _msttexthash="125531679">我们可以使用以下命令列出所有已知的 Docker 映像：</font>

 <code>$ docker images
REPOSITORY  TAG           IMAGE ID      CREATED         SIZE
my-app      0.0.1         32b488088806  25 minutes ago  103MB
openjdk     8-jre-alpine  f7a292bbb70c  10 minutes ago  84.9MB</code> 

<font _mstmutation="1" _msthash="290589" _msttexthash="955375707">上面的命令应该显示我们的自定义图像称为 。现在，我们已准备好运行 Docker 映像。请注意，此时我们不使用 Kubernetes，而是直接通过命令运行映像：</font>```my-app``````docker```

 <code>$ docker run -p 8080:8080 -d my-app:0.0.1
c5a91de6d0d6ffe692434548ff2ce6fdcc2c89fa02f7bc621c0c132ddfe2589a</code> 

<font _mstmutation="1" _msthash="291187" _msttexthash="1729062309">恭喜，您刚刚在 Docker 容器中启动了 Web 服务😊 通过导航到 URL 或 http://localhost:8080/greeting 运行 Web[应用](https://zshipu.com/t?url=http://localhost:8080/greeting)。Docker 提供各种命令来创建、运行和监视 Docker 映像。要列出正在运行的 Docker 映像，只需键入：</font>

 <code>$ docker ps
CONTAINER ID  IMAGE          COMMAND                  CREATED        STATUS         PORTS                    NAMES
c5a91de6d0d6  my-app:0.0.1   "/bin/sh -c 'java -j…"   2 minutes ago  Up 21 seconds  0.0.0.0:8080->8080/tcp   funny_dhawan</code> 

<font _mstmutation="1" _msthash="291785" _msttexthash="117793676">最后，可以通过键入 来停止正在运行的容器。</font>```docker stop```

有关 Docker 文件的更详尽文档，请参阅此处的官方[文档](https://zshipu.com/t?url=https://docs.docker.com/engine/reference/builder)。

# [](#introduction-to-kubernetes)<font _mstmutation="1" _msthash="305630" _msttexthash="18511077">Kubernetes介绍</font>

[Kubernetes](https://zshipu.com/t?url=https://kubernetes.io/)是一个用于在云中部署、监视和扩展应用程序的系统。它最初由谷歌开发，是开源的。Kubernetes 负责运行容器化应用程序。

在 Kubernetes 中，映像的单个运行实例称为**pod**，使用 RESTful Web 服务时，通常有多个同一应用的 Pod 并行运行。Kubernetes 可轻松将计算资源分配给您的窗格，在工作负载繁重时启动更多窗格，或检测不正常的窗格。

Docker 桌面工具的安装包含本地 Kubernetes 服务器。您可以像在云中一样在 Kubernetes 上部署工作负载，但请注意，这只是为了测试目的。在现实生活中，您将使用 Kubernetes 将应用程序部署到真正的云基础架构，如亚马逊云或 Google 云。

# [](#run-your-application-on-kubernetes-cluster)<font _mstmutation="1" _msthash="304057" _msttexthash="69819633">在Kubernetes集群上运行应用程序</font>

<font _mstmutation="1" _msthash="291174" _msttexthash="537431921">在本节中，您将使用 Kubernetes 部署 Docker 映像。更具体地说，您将使用命令行工具以及 Kubernetes 文件来运行应用。</font>```kubectl```

首先，请确保您的计算机上激活并运行 Kubernetes（请参阅此处[的说明](https://zshipu.com/t?url=http://docs.docker.com/docker-for-windows/#kubernetes)）。

第二，我们要启动一个吊舱。为此，我们通常使用[部署文件](https://zshipu.com/t?url=https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)。Kubernetes 将确保必要的吊舱开始，甚至会根据需要替换一个不健康的吊舱。

<font _mstmutation="1" _msthash="292071" _msttexthash="40602185">创建以下部署文件：</font>```deployment.yml```

 <code>apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:0.0.1
        ports:
        - containerPort: 8080</code> 

<font _mstmutation="1" _msthash="292669" _msttexthash="923034957">部署文件指定要运行的 Docker 映像 （）、要启动的 pod 数 （） 以及公开的端口 （）。或者，我们可以添加资源约束，如最大 CPU 和内存使用率。</font>```containers: name``````replicas``````containerPort```

 <code>$ kubectl apply -f deployment.yml
deployment.apps/my-app-deploy created

$ kubectl get deployments
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
my-app-deploy   1/1     1            1           1min

$ kubectl describe deployment my-app-deploy</code> 

<font _mstmutation="1" _msthash="293267" _msttexthash="2780692967">在第一行中，我们创建Kubernetes部署。这会自动启动关联的窗格，因为您可以使用 进行检查。在第二行，您可以获取所有部署的列表;在第三行，您可以查询我们的部署的所有详细信息。请注意，我们的部署配置为仅启动一个窗格。我们可以将此配置更改为两个副本：</font>```kubectl get pods```

 <code>$ kubectl scale --replicas=2 deployment/my-app-deploy
deployment.extensions/my-app-deploy scaled

$ kubectl describe deployments my-app-deploy</code> 

您可以看到，我们有两个正在运行的 pod，这两个窗格的状态都处于"可用"状态。

<font _mstmutation="1" _msthash="291460" _msttexthash="4640292553">此时，我们的群集上运行 Web 应用，但无法直接访问 Web 应用。我们的吊舱的 IP 地址只能从 Kubernetes 群集内访问。所以现在的问题是：我们如何从群集外部测试我们的 Web 应用程序？当您考虑我们的一个吊舱将来可能会被替换，因此 IP 地址将发生变化时，这个问题就变得更加棘手了。好消息是，Kubernetes提供了一个简单的解决方案，称为 。</font>```Services```

<font _mstmutation="1" _msthash="291759" _msttexthash="439430498">[Kubernetes 服务是](https://zshipu.com/t?url=https://kubernetes.io/docs/concepts/services-networking/service/)一种仅一个 IP 地址上公开多个 Pod 的抽象方法。您可以通过以下文件创建服务：</font>```service.yml```

 <code>apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  ports:
    - port: 80
      targetPort: 8080
  selector:
    app: my-app</code> 

 <code>$ kubectl create -f service.yml
service/my-app-service created

$ kubectl get services
NAME             TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes       ClusterIP   10.96.0.1       <none>        443/TCP   5d1h
my-app-service   ClusterIP   10.104.130.56   <none>        80/TCP    24s</code> 

<font _mstmutation="1" _msthash="292656" _msttexthash="1069918135">我们的服务的 IP 地址仍然只能从群集内访问。我们可以使用端口转发来解决此问题。请注意，对于生产就绪环境，您将使用另一个解决方案，如类型的服务或 。</font>```my-app-service``````NodePort``````LoadBalancer```

 <code>$ kubectl port-forward service/my-app-service 8081:80</code> 

<font _mstmutation="1" _msthash="293254" _msttexthash="1220902046">我们的网络应用程序现在可以在网址上访问[http://localhost:8081/greeting。](https://zshipu.com/t?url=http://localhost:8081/greeting)恭喜，您的 Kubernetes 群集现在托管您的 Web 应用程序，您可以通过 Web 浏览器访问它😊</font>```localhost```

<font _mstmutation="1" _msthash="293553" _msttexthash="89885965">要关闭服务和窗格，您可以键入：</font>

 <code>$ kubectl delete deployment my-app-deploy
deployment.extensions "my-app-deploy" deleted

$ kubectl delete service my-app-service
service "my-app-service" deleted</code> 

# [](#summary)<font _mstmutation="1" _msthash="304655" _msttexthash="5618353">总结</font>

让我们总结一下云部署管道中最重要的步骤：

*   将 Web 应用程序打包为 JAR
*   使用内部 JAR 文件创建 Docker 映像
*   创建Kubernetes部署
*   Kubernetes将自动启动吊舱， 里面有我们的 Docker 图像
*   创建Kubernetes服务，作为所有正在运行的窗格的入口点

