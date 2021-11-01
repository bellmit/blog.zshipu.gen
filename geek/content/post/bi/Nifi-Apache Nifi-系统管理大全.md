---
title: Nifi-Apache Nifi-系统管理大全
date: 2021-10-30 12:01:00
tags: [nifi]

---


## 系统要求

Apache NiFi 可以在笔记本电脑这样简单的东西上运行，但它也可以聚类到许多企业级服务器上。因此，所需的硬件和内存数量将取决于所涉及的数据流的规模和性质。数据存储在磁盘上，而 NiFi 正在处理它。因此，NiFi 需要为其各种存储库分配足够的磁盘空间，特别是内容存储库、流文件存储库和出处存储库（请参阅[系统属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#system_properties)部分，了解有关这些存储库的更多信息）。NiFi 具有以下最低系统要求：

- 需要 Java 8 或Java 11
- 支持操作系统：
  - Linux
  - Unix
  - Windows
  - macOS
- 支持的 Web 浏览器：
  - 微软边缘： 电流 + （当前 - 1）
  - 莫齐拉火狐： 电流 + （当前 - 1）
  - 谷歌浏览器： 当前 + （当前 - 1）
  - 野生动物园： 电流 + （当前 - 1）

|      | 在持续和极高的吞吐量下，可能需要调整 CodeCache 设置以避免突然的性能损失。有关更多信息，请参阅[引导属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#bootstrap_properties)部分。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

## 如何安装和启动 NiFi

- Linux/Unix/macOS
  - 减压和未塔到所需的安装目录
  - 在下面找到的文件中进行任何所需的编辑`<installdir>/conf`
    - 至少，我们建议编辑*nifi.属性*文件并输入密码（参见下面[的系统属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#system_properties)）`nifi.sensitive.props.key`
  - 从目录中，通过键入执行以下命令：`<installdir>/bin``./nifi.sh <command>`
    - `start`： 在后台启动 NiFi
    - `stop`： 停止在后台运行的 Nifi
    - `status`： 提供 NiFi 的当前状态
    - `run`： 在前景中运行 Nifi， 并等待 Ctrl - c 启动 Nifi 的关闭
    - `install`： 安装 NiFi 作为一项服务， 然后可以通过
      - `service nifi start`
      - `service nifi stop`
      - `service nifi status`
- Windows
  - 减压到所需的安装目录中
  - 在下面找到的文件中进行任何所需的编辑`<installdir>/conf`
    - 至少，我们建议编辑*nifi.属性*文件并输入密码（参见下面[的系统属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#system_properties)）`nifi.sensitive.props.key`
  - 导航到目录`<installdir>/bin`
  - 双击。这运行 NiFi 的前景， 并等待 Ctrl - c 启动关闭 Nifi`run-nifi.bat`
  - 要查看 NiFi 的当前状态，请双击`status-nifi.bat`

当 NiFi 首次启动时，创建以下文件和目录：

- `content_repository`
- `database_repository`
- `flowfile_repository`
- `provenance_repository`
- `work`目录
- `logs`目录
- 在目录内，*创建流.xml.gz*文件`conf`

|      | 出于安全目的，当没有提供安全配置时，NiFi 现在默认情况下将绑定到 127.0.0.1，并且仅通过此回路接口访问 UI。应配置 HTTPS 属性，以便从其他接口访问 NiFi。请参阅[安全配置](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#security_configuration)，了解如何做到这一点的指导。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

有关配置 NiFi 存储库和配置文件的更多信息，请参阅本指南的[系统属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#system_properties)部分。

## 端口配置

### NIFI

下表列出了 NiFi 使用的默认端口和*nifi.属性*文件中的相应属性。

| 功能                             | 财产                                  | 默认值  |
| :------------------------------- | :------------------------------------ | :------ |
| HTTPS Port                       | `nifi.web.https.port`                 | `8443`  |
| Remote Input Socket Port*        | `nifi.remote.input.socket.port`       | `10443` |
| Cluster Node Protocol Port*      | `nifi.cluster.node.protocol.port`     | `11443` |
| Cluster Node Load Balancing Port | `nifi.cluster.node.load.balance.port` | `6342`  |
| Web HTTP Forwarding Port         | `nifi.web.http.port.forwarding`       | *none*  |

|      | 标有星号 （*） 的端口的属性值在*nifi.属性*中默认为空白。表中显示的值是这些端口的默认值，当[TLS 工具包](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#tls_toolkit)用于生成*nifi.属性*用于安全的 NiFi 实例时。[TLS 工具包](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#tls_toolkit)使用的默认证书管理局端口是 。`9443` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 嵌入式ZooKeeper

下表列出[了嵌入式ZooKeeper服务器](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#embedded_zookeeper)使用的默认端口和*ZooKeeper*的相应属性。

| 功能                                                         | 财产         | 默认值 |
| :----------------------------------------------------------- | :----------- | :----- |
| ZooKeeper服务器报价和领导者选举端口                          | `server.1`   | *没有* |
| ZooKeeper客户端口（已弃用：截至 NiFi 1.10.x，客户端端口不再在单独的线路上指定） | `clientPort` | `2181` |

|      | ZooKeeper服务器端口的评论示例包含在*ZooKeeper。属性*文件的形式。`server.N=nifi-nodeN-hostname:2888:3888;2181` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

## 配置最佳实践

如果您在 Linux 上跑步，请考虑这些最佳实践。典型的 Linux 默认值不一定适合像 NiFi 这样的 IO 密集应用的需求。对于所有这些领域，您的分销要求可能有所不同。使用这些部分作为建议，但请咨询您的特定分布文档，了解如何最好地实现这些建议。

- 最大文件手柄

  NiFi 会在任何时候都可能打开大量文件手柄。通过编辑*/等/安全/限制.conf*添加类似的东西来增加限制

```
*  hard  nofile  50000
*  soft  nofile  50000
```

- 最大叉过程

  NiFi 可能会被配置为生成大量线程。要增加允许的数量，请编辑*/等/安全/限制。*

```
*  hard  nproc  10000
*  soft  nproc  10000
```

您的分发可能需要通过添加来编辑到*/etc/安全/限制。*

```
*  soft  nproc  10000
```

- 增加可用的 TCP 插座端口数量

  如果您的流量将在一小段时间内设置并拆下大量插座，这一点尤其重要。

```
sudo sysctl -w net.ipv4.ip_local_port_range="10000 65000"
```

- 设置插座关闭时在TIMED_WAIT状态下停留多长时间

  你不希望你的插座坐得太久，因为你想能够快速设置和拆解新的插座。这是一个好主意，阅读更多关于它，并适应类似的东西

内核 2.6

```
sudo sysctl -w net.ipv4.netfilter.ip_conntrack_tcp_timeout_time_wait="1"
```

内核 3.0

```
sudo sysctl -w net.netfilter.nf_conntrack_tcp_timeout_time_wait="1"
```

- 告诉Linux你从来不想让NIFI交换

  对于某些应用程序来说，交换是很棒的。对于像 Nifi 这样总是想跑步的东西来说， 这不好。要告诉 Linux 您想换掉，您可以编辑*/等/sysctl.conf*以添加以下行

```
vm.swappiness = 0
```

对于处理各种 NiFi 重新存回的分区，请关闭诸如 。这样做会导致吞吐量的惊人颠簸。编辑文件和感兴趣的分区，添加选项。`atime``/etc/fstab``noatime`

## 推荐的防病毒排除

防病毒软件可能需要很长时间才能扫描大目录及其内的众多文件。此外，如果防病毒软件在扫描期间锁定文件或目录，则这些资源无法访问 NiFi 过程，导致 NiFi 实例/集群中这些资源出现延迟或不可用。为了防止这些性能和可靠性问题发生，强烈建议配置您的防病毒软件以跳过以下 NiFi 目录上的扫描：

- `content_repository`
- `flowfile_repository`
- `logs`
- `provenance_repository`
- `state`

## 安全配置

NiFi 为安全目的提供了多种不同的配置选项。最重要的属性是 nifi.属性文件中标题下的"安全*属性"下的属性*。为了安全运行，必须设置以下属性：

| 属性名称                         | 描述                                                         |
| :------------------------------- | :----------------------------------------------------------- |
| `nifi.security.truststorePasswd` | 信托商店的密码。                                             |
| `nifi.security.keystore`         | 包含服务器私钥的钥匙店文件名。                               |
| `nifi.security.keystoreType`     | 钥匙店的类型。必须是或或。JKS 是首选类型，BCFKS 和 PKCS12 文件将加载弹力城堡提供商。`PKCS12``JKS``BCFKS` |
| `nifi.security.keystorePasswd`   | 钥匙店的密码。                                               |
| `nifi.security.keyPasswd`        | 钥匙店中证书的密码。如果不设置，将使用其值。`nifi.security.keystorePasswd` |
| `nifi.security.truststore`       | 信托商店的档案名，将用于授权那些连接到 NiFi。没有信托商店的安全实例将拒绝所有传入的连接。 |
| `nifi.security.truststoreType`   | 信托商店的类型。必须是或或。JKS 是首选类型，BCFKS 和 PKCS12 文件将加载弹力城堡提供商。`PKCS12``JKS``BCFKS` |

配置上述属性后，我们可以通过 HTTPS 而不是 HTTP 访问用户界面。这是通过设置和属性来实现的。该属性指示服务器应运行哪个主机名。如果需要从所有网络接口访问 HTTPS 接口，则应使用 HTTPS 接口的价值。允许管理员配置应用程序仅在特定的网络接口上运行，或者可以指定属性。`nifi.web.https.host``nifi.web.https.port``nifi.web.https.host``0.0.0.0``nifi.web.http.network.interface*``nifi.web.https.network.interface*`

|      | 启用 HTTPS 时，必须解置属性。NiFi 仅支持在 HTTP**或**HTTPS 上运行，而不是同时运行。`nifi.web.http.port` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

NiFi 的 Web 服务器将要求访问用户界面的用户进行基于证书的客户身份验证，而该验证机制不需要单向 SSL（例如 LDAP、OpenId 连接等）。启用替代身份验证机制将配置 Web 服务器以进行 WAND 证书基础客户端身份验证。这将允许它支持用户与证书和那些没有可能登录凭据。有关详细信息，请参阅[用户身份验证](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#user_authentication)。

现在，用户界面已得到保护，我们也可以轻松地保护站点到站点的连接和内部集群通信。这是通过设置和属性，分别，以。这些通信始终需要双向 SSL，因为节点将使用其配置的钥匙店/信托商店进行身份验证。`nifi.remote.input.secure``nifi.cluster.protocol.is.secure``true`

NiFi 的 Web SSL 上下文工厂的自动刷新可使用以下属性启用：

| 属性名称                            | 描述                                                         |
| :---------------------------------- | :----------------------------------------------------------- |
| `nifi.security.autoreload.interval` | 指定检查钥匙店和信托商店以获取更新的间隔。仅适用于设置为 。默认值是 。`nifi.security.autoreload.enabled``true``10 secs` |
| `nifi.security.autoreload.enabled`  | 具体说明如果检测到钥匙店和信托商店的更新，是否应自动重新加载 SSL 上下文工厂。默认情况下，它被设置为 。`false` |

一旦该属性被设置为，对配置的钥匙店和信托商店的任何有效更改将导致 NiFi 的 SSL 上下文工厂重新加载，使客户能够拾取更改。这是为了允许过期的证书在钥匙店更新和新的受信任证书添加到信托商店，所有无需重新启动 NiFi 服务器。`nifi.security.autoreload.enabled``true`

|      | 自动刷新逻辑不会拾取对任何或属性的更改，该逻辑假定密码和存储路径将保持不变。`nifi.security.keystore*``nifi.security.truststore*` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### TLS 生成工具包

为了方便 NiFi 的安全设置，您可以使用命令线实用程序自动生成所需的密钥商店、托管店和相关配置文件。这对于保护多个 NiFi 节点特别有用，这可能是一个繁琐且容易出错的过程。有关更多信息，请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)中的[TLS](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#tls_toolkit)工具包部分。相关主题包括：`tls-toolkit`

- [通配符证书](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#wildcard_certificates)
- [操作模式：独立和客户/服务器](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#tls_operation_modes)
- [使用现有的中间证书管理局](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#tls_intermediate_ca)
- [附加证书命令](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#additional_certificate_commands)

### TLS 密码套件

Java 运行时间环境提供指定自定义 TLS 密码套件的功能，以便服务器在接受客户端连接时使用。有关更多信息，请参阅[此处](https://java.com/en/configure_crypto.html)。要将此功能用于 NiFi 网络服务，可以设置以下 NiFi 属性：

| 属性名称                              | 描述                                                         |
| :------------------------------------ | :----------------------------------------------------------- |
| `nifi.web.https.ciphersuites.exclude` | 一组密码，不得用于传入的客户端连接。设置后可过滤可用密码。   |
| `nifi.web.https.ciphersuites.include` | 一组密码可供传入的客户端连接使用。如果设置，将替换系统默认值。 |

每个属性应采取逗号分离列表的形式，共同密码名称[在这里](https://docs.oracle.com/javase/8/docs/technotes/guides/security/StandardNames.html#ciphersuites)指定。也可以指定常规表达式（例如）。`^.*GCM_SHA256$`

语义与以下码头 API 的使用相匹配：

- [斯尔康特文工厂. 集包括密码套件 （）](https://www.eclipse.org/jetty/javadoc/jetty-9/org/eclipse/jetty/util/ssl/SslContextFactory.html#setIncludeCipherSuites(java.lang.String...))
- [斯尔康特克斯工厂. 设置不包括密码西装 （）](https://www.eclipse.org/jetty/javadoc/jetty-9/org/eclipse/jetty/util/ssl/SslContextFactory.html#setExcludeCipherSuites(java.lang.String...))

## 用户身份验证

NiFi 通过客户端证书、用户名/密码、阿帕奇旋钮或[OpenId 连接](http://openid.net/connect)支持用户身份验证。

用户名/密码身份验证由"登录身份提供商"执行。登录身份提供商是一种可插入的机制，可通过用户名/密码对用户进行身份验证。要使用的登录身份提供商配置在*nifi.属性*文件中。目前，NiFi提供用户名/密码与登录身份提供商选项的[单用户](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#single_user_identity_provider)，[轻量级目录访问协议（LDAP）](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#ldap_login_identity_provider)和[Kerberos。](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#kerberos_login_identity_provider)

该属性指定登录身份提供商的配置文件。默认情况下，此属性设置为 。`nifi.login.identity.provider.configuration.file``./conf/login-identity-providers.xml`

该属性指示应使用配置的登录身份提供商中的哪一个。此属性的默认值是使用生成的用户名和密码支持身份验证。`nifi.security.user.login.identity.provider``single-user-provider`

在 OpenId 连接身份验证期间，NiFi 将重定向用户在返回到 NiFi 之前与提供商登录。然后，NiFi 将致电提供商以获取用户身份。

在阿帕奇诺克斯认证期间，NiFi 将重定向用户在返回 NiFi 之前与阿帕奇诺克斯登录。NiFi 将在认证过程中验证阿帕奇诺克斯令牌。

|      | NiFi 只能在给定时间配置用户名/密码、OpenId 连接或阿帕奇诺克斯。它不支持同时运行其中的每一个。NiFi 将要求客户端证书通过 HTTPS 对用户进行身份验证，如果这些证书没有配置的话。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

用户不能匿名验证与 NiFi 的安全实例，除非设置为 。如果是这样的话，NiFi 还必须配置一个授权机构，该授权人支持授权匿名用户。目前，NiFi 不附带任何支持此的授权商。这里有一个功能请求，以帮助支持它[（NIFI-2730）。](https://issues.apache.org/jira/browse/NIFI-2730)`nifi.security.allow.anonymous.authentication``true`

设置时需要考虑三种情况。当用户直接呼叫端点而没有尝试身份验证时，将控制请求是经过身份验证还是被拒绝。其他两种情况是代理请求时。这可以通过 NiFi 节点（例如 NiFi 集群中的节点）代理，也可以由代理匿名用户请求的单独代理代理。在这些代理方案中，将控制请求是经过验证还是被拒绝。在所有这些情况下，如果请求经过认证，则随后将根据请求的资源获得正常授权。`nifi.security.allow.anonymous.authentication``nifi.security.allow.anonymous.authentication``nifi.security.allow.anonymous.authentication`

|      | NiFi 不会通过 HTTP 执行用户身份验证。使用 HTTP，所有用户将被授予所有角色。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 单个用户

默认单用户登录身份提供商支持自动生成用户名和密码凭据。

生成的用户名将是一个由 36 个字符组成的随机 UUID。生成的密码将是一个由 32 个字符组成的随机字符串，并使用 bcrypt 哈希进行存储。

*nifi.属性*中的默认配置启用了单个用户身份验证：

```
nifi.security.user.login.identity.provider=single-user-provider
```

默认*登录身份提供商.xml*包括空白提供商定义：

```
<provider>
   <identifier>single-user-provider</identifier>
   <class>org.apache.nifi.authentication.single.user.SingleUserLoginIdentityProvider</class>
   <property name="Username"/>
   <property name="Password"/>
</provider>
```

以下命令可用于更改用户名和密码：

```
$ ./bin/nifi.sh set-single-user-credentials <username> <password>
```

### 轻量级目录访问协议 （LDAP）

下面是配置与目录服务器集成以验证用户的登录身份提供商的示例和描述。

在*nifi.属性*中设置以下设置为 LDAP 用户名/密码身份验证：

```
nifi.security.user.login.identity.provider=ldap-provider
```

修改*登录身份提供商.xml*启用 。以下是文件中提供的示例：`ldap-provider`

```
<provider>
    <identifier>ldap-provider</identifier>
    <class>org.apache.nifi.ldap.LdapProvider</class>
    <property name="Authentication Strategy">START_TLS</property>

    <property name="Manager DN"></property>
    <property name="Manager Password"></property>

    <property name="TLS - Keystore"></property>
    <property name="TLS - Keystore Password"></property>
    <property name="TLS - Keystore Type"></property>
    <property name="TLS - Truststore"></property>
    <property name="TLS - Truststore Password"></property>
    <property name="TLS - Truststore Type"></property>
    <property name="TLS - Client Auth"></property>
    <property name="TLS - Protocol"></property>
    <property name="TLS - Shutdown Gracefully"></property>

    <property name="Referral Strategy">FOLLOW</property>
    <property name="Connect Timeout">10 secs</property>
    <property name="Read Timeout">10 secs</property>

    <property name="Url"></property>
    <property name="User Search Base"></property>
    <property name="User Search Filter"></property>

    <property name="Identity Strategy">USE_DN</property>
    <property name="Authentication Expiration">12 hours</property>
</provider>
```

具有以下属性：`ldap-provider`

| 属性名称                    | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `Authentication Expiration` | 用户身份验证有效期。如果用户从未注销，则需要他们在此持续时间后登录。 |
| `Authentication Strategy`   | 如何验证与 LDAP 服务器的连接。可能的值是，或。`ANONYMOUS``SIMPLE``LDAPS``START_TLS` |
| `Manager DN`                | 用于绑定到 LDAP 服务器以搜索用户的管理器的 DN。              |
| `Manager Password`          | 用于绑定到 LDAP 服务器以搜索用户的管理器密码。               |
| `TLS - Keystore`            | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的钥匙店路径。       |
| `TLS - Keystore Password`   | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的钥匙店密码。       |
| `TLS - Keystore Type`       | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的钥匙店类型（即。 或））`JKS``PKCS12` |
| `TLS - Truststore`          | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的信托商店路径。     |
| `TLS - Truststore Password` | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的信托商店密码。     |
| `TLS - Truststore Type`     | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的信托商店类型（即。 或））`JKS``PKCS12` |
| `TLS - Client Auth`         | 使用 LDAPS 或START_TLS连接到 LDAP 时的客户身份验证策略。可能的值是， . .`REQUIRED``WANT``NONE` |
| `TLS - Protocol`            | 使用 LDAPS 或START_TLS连接到 LDAP 时要使用的协议。（例如，等等）。`TLS``TLSv1.1``TLSv1.2` |
| `TLS - Shutdown Gracefully` | 指定在目标上下文关闭之前是否应优雅地关闭 TLS。默认为假。     |
| `Referral Strategy`         | 处理转介的策略。可能的值是， . .`FOLLOW``IGNORE``THROW`      |
| `Connect Timeout`           | 连接超时的持续时间。（即）。`10 secs`                        |
| `Read Timeout`              | 读取超时时间的持续时间。（即）。`10 secs`                    |
| `Url`                       | LDAP 服务器的隔空网蛋白列表（即）。`ldap://<hostname>:<port>` |
| `User Search Base`          | 用于搜索用户的底座 DN（即）。`CN=Users,DC=example,DC=com`    |
| `User Search Filter`        | 过滤器，以搜索用户对。（即）。用户指定的名称插入"{0}"。`User Search Base``sAMAccountName={0}` |
| `Identity Strategy`         | 识别用户的策略。可能的值是和 。缺少此属性的默认功能是USE_DN以保留向后兼容性。 如果可能，将使用用户条目的完整 DN。 将使用用户登录的用户名。`USE_DN``USE_USERNAME``USE_DN``USE_USERNAME` |

|      | 要更改*nifi.属性*和*登录身份提供商.xml*才能生效，需要重新启动 NiFi。如果 NiFi 是聚类的，则所有节点上的配置文件必须相同。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 克贝罗斯

以下是配置与 Kerberos 密钥分发中心 （KDC） 集成以验证用户的登录身份提供商的示例和描述。

在*nifi.属性*中设置以下设置为启用 Kerberos 用户名/密码身份验证：

```
nifi.security.user.login.identity.provider=kerberos-provider
```

修改*登录身份提供商.xml*启用 。以下是文件中提供的示例：`kerberos-provider`

```
<provider>
    <identifier>kerberos-provider</identifier>
    <class>org.apache.nifi.kerberos.KerberosProvider</class>
    <property name="Default Realm">NIFI.APACHE.ORG</property>
    <property name="Authentication Expiration">12 hours</property>
</provider>
```

具有以下属性：`kerberos-provider`

| 属性名称                    | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `Default Realm`             | 当用户输入不完整的用户委托（即）时，提供默认领域。`NIFI.APACHE.ORG` |
| `Authentication Expiration` | 用户身份验证有效期。如果用户从未注销，则需要他们在此持续时间后登录。 |

另请参阅[Kerberos 服务](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#kerberos_service)，允许通过客户 Kerberos 门票进行单次登录访问。

|      | 要更改*nifi.属性*和*登录身份提供商.xml*才能生效，需要重新启动 NiFi。如果 NiFi 是聚类的，则所有节点上的配置文件必须相同。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 开放式连接

要通过 OpenId 连接实现身份验证，以下属性必须在*nifi. 属性*中配置。

| 属性名称                                                   | 描述                                                         |
| :--------------------------------------------------------- | :----------------------------------------------------------- |
| `nifi.security.user.oidc.discovery.url`                    | 所需的 OpenId 连接提供商[（http://openid.net/specs/openid-connect-discovery-1_0.html）](http://openid.net/specs/openid-connect-discovery-1_0.html)的发现 URL。 |
| `nifi.security.user.oidc.connect.timeout`                  | 与 OpenId 连接提供商通信时连接超时。                         |
| `nifi.security.user.oidc.read.timeout`                     | 与 OpenId 连接提供商通信时阅读超时。                         |
| `nifi.security.user.oidc.client.id`                        | 在 OpenId 连接提供商注册后，NiFi 的客户 ID。                 |
| `nifi.security.user.oidc.client.secret`                    | 在 OpenId 连接提供商注册后，NiFi 的客户秘密。                |
| `nifi.security.user.oidc.preferred.jwsalgorithm`           | 验证身份令牌的首选算法。如果此值为空白，它将默认到 OpenId 连接提供商需要根据规范支持该值。如果此值是，或者，NiFi 将尝试使用指定的客户端秘密验证 HMAC 受保护的令牌。如果这个值是，NiFi将尝试验证不安全/纯代币。此算法的其他值将尝试解析为 RSA 或 EC 算法，以便与通过发现 URL 中发现的元数据中的元数据中的jwks_uri提供的 JSON Web 密钥 （JWK） 一起使用。`RS256``HS256``HS384``HS512``none` |
| `nifi.security.user.oidc.additional.scopes`                | Comma 分离示波器，除和 。`openid``email`                     |
| `nifi.security.user.oidc.claim.identifying.user`           | 标识要登录的用户的索赔;默认是 。可能需要通过使用前请求。`email``nifi.security.user.oidc.additional.scopes` |
| `nifi.security.user.oidc.fallback.claims.identifying.user` | Comma 分离了用于识别用户的可能回退声明，以防登录用户不存在索赔。`nifi.security.user.oidc.claim.identifying.user` |

### 萨姆尔

要通过 SAML 实现身份验证，以下属性必须在*nifi. 属性*中配置。

| 属性名称                                                  | 描述                                                         |
| :-------------------------------------------------------- | :----------------------------------------------------------- |
| `nifi.security.user.saml.idp.metadata.url`                | 获取身份提供者元数据的 URL。元数据可以通过或，或可以引用本地文件从身份提供者检索。`http://``https://``file://` |
| `nifi.security.user.saml.sp.entity.id`                    | 服务提供商的实体 ID（即 NiFi）。此值将用作 SAML 身份验证请求，并且应为有效的 URI。在某些情况下，服务提供商实体 ID 必须提前向身份提供商注册。`Issuer` |
| `nifi.security.user.saml.identity.attribute.name`         | 包含用户身份的 SAML 断言属性的名称。此属性是可选的，如果没有指定，或者未找到属性，则将使用主题的 NameID。 |
| `nifi.security.user.saml.group.attribute.name`            | 包含用户所属群名的 SAML 断言属性的名称。此属性是可选的，但如果填充，这些组将传递到授权过程。 |
| `nifi.security.user.saml.metadata.signing.enabled`        | 启用生成的服务提供商元数据的签名。                           |
| `nifi.security.user.saml.request.signing.enabled`         | 控制生成的服务提供商元数据的价值。这表明服务提供商（即 NiFi） 不应签署发送给身份提供商的身份验证请求，但如果身份提供商表示，则请求仍可能需要签名。`AuthnRequestsSigned``nifi-api/access/saml/metadata``WantAuthnRequestSigned=true` |
| `nifi.security.user.saml.want.assertions.signed`          | 控制生成的服务提供商元数据的价值。这表明身份提供者应签署断言，但某些身份提供商可能会提供自己的配置来控制断言是否已签名。`WantAssertionsSigned``nifi-api/access/saml/metadata` |
| `nifi.security.user.saml.signature.algorithm`             | 签署 SAML 消息时要使用的算法。引用[打开 SAML 签名常数](https://git.shibboleth.net/view/?p=java-xmltooling.git;a=blob;f=src/main/java/org/opensaml/xml/signature/SignatureConstants.java)以获得有效值列表。如果不具体说明，将使用 SHA-256 的默认值。 |
| `nifi.security.user.saml.signature.digest.algorithm`      | 签署 SAML 消息时要使用的消化算法。引用[打开 SAML 签名常数](https://git.shibboleth.net/view/?p=java-xmltooling.git;a=blob;f=src/main/java/org/opensaml/xml/signature/SignatureConstants.java)以获得有效值列表。如果不具体说明，将使用 SHA-256 的默认值。 |
| `nifi.security.user.saml.message.logging.enabled`         | 启用用于调试目的的 SAML 消息的记录。                         |
| `nifi.security.user.saml.authentication.expiration`       | NiFi JWT 的到期，该产品将由成功的 SAML 认证响应生成。        |
| `nifi.security.user.saml.single.logout.enabled`           | 启用 SAML 单Log，从而导致 NiFi 的注销注销到身份提供商的注销。默认情况下，NiFi 的注销只会删除 NiFi JWT。 |
| `nifi.security.user.saml.http.client.truststore.strategy` | 当 Idp 元数据 URL 以 https 开始时， 信托商店策略。使用 JDK 默认信托商店的指示值。"NIFI"值表示使用指定的信托商店。`JDK``nifi.security.truststore` |
| `nifi.security.user.saml.http.client.connect.timeout`     | 与 SAML IDP 通信时的连接超时。                               |
| `nifi.security.user.saml.http.client.read.timeout`        | 与 SAML IDP 通信时的读取超时。                               |

### 阿帕奇·诺克斯

要通过阿帕奇诺克斯启用身份验证，以下属性必须在*nifi. 属性*中配置。

| 属性名称                             | 描述                                                         |
| :----------------------------------- | :----------------------------------------------------------- |
| `nifi.security.user.knox.url`        | 阿帕奇诺克斯登录页面的 URL。                                 |
| `nifi.security.user.knox.publicKey`  | 通往阿帕奇诺克斯公钥的路径，用于验证 HTTP Cookie 中身份验证令牌的签名。 |
| `nifi.security.user.knox.cookieName` | 阿帕奇·诺克斯在成功登录后将生成的 HTTP 曲奇的名称。          |
| `nifi.security.user.knox.audiences`  | 自选。允许受众的逗号单独列出。如果设置，代币中的观众必须出现在此列表中。代币中填充的受众可以配置在诺克斯。 |

## 多租户授权

配置 NiFi 以安全运行并具有身份验证机制后，您必须配置谁有权访问系统，以及他们的访问级别。您可以使用"多租户授权"来做到这一点。多租户授权使多个用户组（租户）能够命令、控制和观察数据流的不同部分，并具有不同级别的授权。当经过验证的用户尝试查看或修改 NiFi 资源时，系统会检查用户是否具有执行该操作的特权。这些特权由您可以在全系统范围内应用或应用于各个组件的政策定义。

### 授权配置

"授权人"通过在启动时创建初步授权，授予用户管理用户和策略的特权。

授权人使用*nifi. 属性*文件中的两个属性进行配置。

- 该属性指定了定义授权人的位置配置文件。默认情况下，选择位于根安装会议目录中的*授权人.xml*文件。`nifi.authorizer.configuration.file`
- 该属性指示授权人文件中配置的*授权人中的哪一个.xml*文件要使用。`nifi.security.user.authorizer`

### 授权人.xml设置

*授权人.xml*文件用于定义和配置可用的授权人。默认授权人是标准管理授权人。托管授权人由用户群提供者和访问政策提供者组成。用户、组和访问策略将通过这些提供商进行加载和可选配置。托管授权人将根据这些提供的用户、组和访问策略做出所有访问决策。

在启动过程中，需要检查以确保没有两个具有相同身份/名称的用户/组。无论配置的实现情况如何，此检查都会执行。这是必要的，因为这是用户/组在访问决策过程中的身份识别和授权方式。

#### 文件使用者组提供者

默认用户群提供者是文件用户群提供者，但是，您可以开发额外的用户群提供者作为扩展。文件使用者组提供者具有以下属性：

- 用户文件 - 文件用户群提供者存储用户和组的文件。默认情况下，选择目录中的*用户.xml。*`conf`
- 传统授权用户文件 - 进入现有*授权用户的*完整路径.xml该路径将自动用于将用户和组加载到用户文件中。
- 初始用户身份 - 用户和系统的身份，以种子用户文件。每个属性的名称必须是唯一的，例如："初始用户标识 A"、"初始用户标识 B"、"初始用户标识 C"或"初始用户标识 1"、"初始用户标识 2"、"初始用户标识 3"

#### 拉达普瑟集团提供器

用户群提供者的另一个选项是 LdapUser 组提供者。默认情况下，此选项会被注释，但可以配置以取代文件使用者群提供者。这将同步来自目录服务器的用户和组，并将它们以仅读形式以 NiFi UI 形式呈现。

LdapUser 群提供者具有以下属性：

| 属性名称                                                 | 描述                                                         |
| :------------------------------------------------------- | :----------------------------------------------------------- |
| `Group Member Attribute - Referenced User Attribute`     | 如果空白，定义中的属性值预计将是用户的完整 dn。如果不是空白，此属性将定义用户 ldap 条目的属性，其中定义的属性值是引用 （即） 。使用此属性也需要配置。（即 与。`Group Member Attribute``Group Member Attribute``uid``User Search Base``member: cn=User 1,ou=users,o=nifi``memberUid: user1`) |
| `Authentication Strategy`                                | 如何验证与 LDAP 服务器的连接。可能的值是，或。`ANONYMOUS``SIMPLE``LDAPS``START_TLS` |
| `Manager DN`                                             | 用于绑定到 LDAP 服务器以搜索用户的管理器的 DN。              |
| `Manager Password`                                       | 用于绑定到 LDAP 服务器以搜索用户的管理器密码。               |
| `TLS - Keystore`                                         | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的钥匙店路径。       |
| `TLS - Keystore Password`                                | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的钥匙店密码。       |
| `TLS - Keystore Type`                                    | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的钥匙店类型（即。 或））`JKS``PKCS12` |
| `TLS - Truststore`                                       | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的信托商店路径。     |
| `TLS - Truststore Password`                              | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的信托商店密码。     |
| `TLS - Truststore Type`                                  | 使用 LDAPS 或START_TLS连接到 LDAP 时使用的信托商店类型（即。 或））`JKS``PKCS12` |
| `TLS - Client Auth`                                      | 使用 LDAPS 或START_TLS连接到 LDAP 时的客户身份验证策略。可能的值是， . .`REQUIRED``WANT``NONE` |
| `TLS - Protocol`                                         | 使用 LDAPS 或START_TLS连接到 LDAP 时要使用的协议。（例如，等等）。`TLS``TLSv1.1``TLSv1.2` |
| `TLS - Shutdown Gracefully`                              | 指定在目标上下文关闭之前是否应优雅地关闭 TLS。默认为假。     |
| `Referral Strategy`                                      | 处理转介的策略。可能的值是， . .`FOLLOW``IGNORE``THROW`      |
| `Connect Timeout`                                        | 连接超时的持续时间。（即）。`10 secs`                        |
| `Read Timeout`                                           | 读取超时时间的持续时间。（即）。`10 secs`                    |
| `Url`                                                    | LDAP 服务器的隔空网蛋白列表（即）。`ldap://<hostname>:<port>` |
| `Page Size`                                              | 在检索用户和组时设置页面大小。如果没有指定，则不执行传呼。   |
| `Group Membership - Enforce Case Sensitivity`            | 确定组成员资格决策是否对案例敏感。当推断出用户或组（不指定或用户或组搜索基数或用户身份属性或群名属性）时，将强制执行案例敏感性，因为用于用户身份或群名的值将模棱两可。默认为假。 |
| `Sync Interval`                                          | 同步用户和组之间的时间。（即）。最低允许值是 。`30 mins``10 secs` |
| `User Search Base`                                       | 用于搜索用户的底座 DN（即）。需要搜索用户。`ou=users,o=nifi` |
| `User Object Class`                                      | 用于识别用户的对象类（即）。如果搜索用户，则需要。`person`   |
| `User Search Scope`                                      | 搜索用户的搜索范围（或）。如果搜索用户，则需要。`ONE_LEVEL``OBJECT``SUBTREE` |
| `User Search Filter`                                     | 过滤器，用于搜索用户对（即）。自选。`User Search Base``(memberof=cn=team1,ou=groups,o=nifi)` |
| `User Identity Attribute`                                | 用于提取用户身份的属性（即）。自选。如果不设置，则使用整个 DN。`cn` |
| `User Group Name Attribute`                              | 用于定义组成员资格的属性（即）。自选。如果不设置组成员资格，则不会通过用户计算。将依赖于通过设置来定义组成员资格。此属性的价值是用户 ldap 条目中的属性名称，该属性将其与组关联。例如，该用户属性的价值可能是 dn 或组名。预期值在 。`memberof``Group Member Attribute``User Group Name Attribute - Referenced Group Attribute` |
| `User Group Name Attribute - Referenced Group Attribute` | 如果为空白，则所定义的属性值应为组的完整 dn。如果不是空白，此属性将定义所定义的属性值为引用的组 ldap 条目的属性（即）。使用此属性也需要配置。`User Group Name Attribute``User Group Name Attribute``name``Group Search Base` |
| `Group Search Base`                                      | 用于搜索组（即）的基础 DN。需要搜索组。`ou=groups,o=nifi`    |
| `Group Object Class`                                     | 识别组的对象类（即）。需要搜索组。`groupOfNames`             |
| `Group Search Scope`                                     | 搜索组的搜索范围（或）。需要搜索组。`ONE_LEVEL``OBJECT``SUBTREE` |
| `Group Search Filter`                                    | 过滤器搜索组对。自选。`Group Search Base`                    |
| `Group Name Attribute`                                   | 用于提取组名（即）的属性。自选。如果不设置，则使用整个 DN。`cn` |
| `Group Member Attribute`                                 | 用于定义组成员资格的属性（即）。自选。如果不设置组成员资格，则不会通过组计算。将依赖于通过设置来定义组成员资格。此属性的价值是将属性与用户关联的组 ldap 条目中的属性名称。例如，该组属性的价值可能是 dn 或成员Uid。预期值在 。（即 与。`member``User Group Name Attribute``Group Member Attribute - Referenced User Attribute``member: cn=User 1,ou=users,o=nifi``memberUid: user1`) |

|      | *nifi.属性*中指定的任何身份映射规则也将应用于用户身份。未映射组名。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 壳牌使用者集团提供

ShellUserGroup 提供者使用外壳命令从类似 Unix 的系统获取用户和组详细信息。

此提供商执行各种外壳管道，并带有诸如 Linux 和 macOS 等命令。`getent``dscl`

支持的系统可以配置为从外部来源（如 LDAP 或 NIS）检索用户和组。在这些情况下，外壳命令将返回这些外部用户和组。这为管理员提供了集成用户和组目录服务的另一种机制。

壳牌使用者集团提供者具有以下属性：

| 属性名称                | 描述                                                         |
| :---------------------- | :----------------------------------------------------------- |
| `Exclude Users`         | 用于排除用户的常规表达方式。默认值是""，这意味着没有用户被排除在外。 |
| `Initial Refresh Delay` | 第一次用户和组刷新之前初始延迟的持续时间。（即）。默认是 。`10 secs``5 mins` |
| `Refresh Delay`         | 每个用户和组刷新之间的延迟持续时间。（即）。默认是 。`10 secs``5 mins` |
| `Exclude Groups`        | 用于排除组的常规表达。默认值为""，这意味着不包括任何组。     |

与 LdapUser 群提供者一样，壳牌使用者集团提供者也在*授权人的文件中进行了评论.xml。*请参阅该评论以提供使用示例。

#### 蔚蓝图使用者组提供者

AzureGraph 用户群提供者使用微软图形 API 从 Azure 活动目录 （AAD） 获取用户和组。

根据 Azure AD 组的*显示名*属性对下的筛选条件（、和）进行分组获取。然后从这些组加载成员用户。应至少指定一个筛选条件。`Group Filter Prefix``Group Filter Suffix``Group Filter Substring``Group Filter List Inclusion`

此提供商需要 Azure 应用程序注册：

- 微软图形组. 阅读. 全部和用户. 阅读. 所有 API 权限，并经管理员同意
- 客户端秘密或应用程序密码
- UPN 和/或电子邮件的 ID 令牌声明

有关如何创建有效的应用注册的更多信息，请参阅[此处](https://docs.microsoft.com/en-us/graph/auth-v2-service)和[此处](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-daemon-app-registration)。

AzureGraphUser群提供器具有以下属性：

| 属性名称                      | 描述                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| `Claim for Username`          | 用户目录对象的属性映射到 NiFi 用户名字段。默认值是"上"。"电子邮件"是设置为"upn"的另一种选择。`nifi.security.user.oidc.fallback.claims.identifying.user` |
| `Refresh Delay`               | 每个用户和组刷新之间的延迟持续时间。默认是 。`5 mins`        |
| `Authority Endpoint`          | Azure AD 登录的终点。这可以在 Azure 活动目录下的 Azure 门户中找到，→应用程序注册→ [应用程序名称] →端点。例如，全球权威端点[是 https://login.microsoftonline.com。](https://login.microsoftonline.com/) |
| `Directory ID`                | Azure AD 租户的租户 ID 或目录 ID。这可以在 Azure 活动目录下的 Azure 门户中找到，→应用程序注册→ [应用程序名称] →目录 （租户） ID。 |
| `Application ID`              | Azure 应用程序注册的客户 ID 或应用程序 ID。这可以在 Azure 活动目录下的 Azure 门户中找到，→应用程序注册→ [应用程序名称] →概述→应用程序 （客户端） ID。 |
| `Client Secret`               | Azure 应用程序注册的客户端秘密。根据 Azure 活动目录，您可以在 Azure 门户中创建秘密→应用程序注册→ [应用程序名称] →证书→客户机密→ []新客户秘密。 |
| `Group Filter Prefix`         | Azure AD 组的前缀过滤器。与组显示名匹配，仅检索以提供前缀开头的名称的组。 |
| `Group Filter Suffix`         | Azure AD 组的后缀过滤器。与组显示名匹配，仅检索以所提供的后缀结尾的名称的组。 |
| `Group Filter Substring`      | Azure AD 组的子弦过滤器。与组显示名称匹配，仅检索包含所提供子弦的名称的组。 |
| `Group Filter List Inclusion` | Azure AD 组的通信分离列表。如果没有指定基于字符串的匹配过滤器（即前缀、后缀和子弦），则设置此属性以避免取取 Azure AD 租户中的所有组和用户。 |
| `Page Size`                   | 与微软图形 API 一起使用的页面大小。设置为 0 以禁用寻呼 API 呼叫。默认值： 50， 最大： 999. |

与 LdapUser 群提供器和壳牌使用者组提供器一样，AzureGraphUserGroup 提供者配置也在*授权人.xml*文件中进行了评论。请参阅入门配置的评论。

#### 综合实施

用户群提供者的另一个选项是复合实现。这意味着可以配置和组合多个源/实现。例如，管理员可以配置用户/组从文件和目录服务器加载。有两个复合实现，一个支持多个用户群提供者，一个支持多个用户群提供者和一个可配置的用户组提供器。

复合用户群提供器将为从多个来源检索用户和组提供支持。复合使用者集团提供者具有以下属性：

| 属性名称                           | 描述                                                         |
| :--------------------------------- | :----------------------------------------------------------- |
| `User Group Provider [unique key]` | 用户组提供商要加载的标识符。每个属性的名称必须是唯一的，例如："用户组提供商 A"、"用户组提供商 B"、"用户组提供商 C"或"用户组提供商 1"、"用户组提供商 2"、"用户组提供商 3" |

|      | *nifi. 属性*中指定的任何身份映射规则均不在此实施中应用。此行为需要由基础实现应用。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

复合可配置用户群提供器将为从多个来源检索用户和组提供支持。此外，还需要一个可配置的用户组提供商。可配置用户组提供商的用户是可配置的，但从用户组提供商之一（唯一密钥）加载的用户将无法配置。复合可配置使用者组提供器具有以下属性：

| 属性名称                           | 描述                                                         |
| :--------------------------------- | :----------------------------------------------------------- |
| `User Group Provider [unique key]` | 用户组提供商要加载的标识符。每个属性的名称必须是唯一的，例如："用户组提供商 A"、"用户组提供商 B"、"用户组提供商 C"或"用户组提供商 1"、"用户组提供商 2"、"用户组提供商 3" |
| `Configurable User Group Provider` | 可配置的用户群提供商。                                       |

#### 文件处理政策提供者

默认的访问政策提供者是文件访问政策提供者，但是，您可以开发额外的访问政策提供者作为扩展。文件处理政策提供者具有以下属性：

| 属性名称                       | 描述                                                         |
| :----------------------------- | :----------------------------------------------------------- |
| `Node Group`                   | 包含 NiFi 聚类节点的组的名称。这通常用于动态添加节点/从组集中删除节点。 |
| `User Group Provider`          | 上面定义的用户组提供商的标识符将用于访问用户和组，以便在托管访问策略中使用。 |
| `Authorizations File`          | 文件获得政策提供者将存储策略的文件。                         |
| `Initial Admin Identity`       | 初始管理员用户的身份，该用户将被授予对 UI 的访问权限，并具有创建更多用户、组和策略的能力。使用证书或 LDAP 或 Kerberos 本金时，此属性的价值可能是 DN。此属性仅在未定义其他策略时使用。如果指定此属性，则无法指定"遗产授权用户文件"。 |
| `Legacy Authorized Users File` | 通往现有*授权用户的*完整路径.xml将自动转换为新的授权模式。如果指定了此属性，则无法指定初始管理员身份，并且此属性仅在未定义其他用户、组和策略时使用。 |
| `Node Identity`                | NIFI聚类节点的身份。当聚类时，应定义每个节点的属性，以便每个节点了解所有其他节点。如果不对这些属性进行聚类，则可以忽略这些属性。每个属性的名称必须是唯一的，例如三个节点组："节点标识 A"、"节点标识 B"、"节点标识 C"或"节点标识 1"、"节点标识 2"、"节点标识 3" |

|      | 在初始管理员身份、节点身份属性中配置或在旧版授权用户文件中发现的身份必须在配置的用户群提供商中提供。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

|      | 传统用户文件中的任何用户都必须在配置的用户群提供商中找到。 |
| ---- | ---------------------------------------------------------- |
|      |                                                            |

|      | *nifi.属性*中指定的任何身份映射规则也将应用于节点标识，因此值应是未映射的身份（即证书中的完整 DN）。此标识必须在配置的用户群提供商中找到。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 标准管理授权人

默认授权人是标准管理授权人，但是，您可以开发额外的授权人作为扩展。标准管理授权人具有以下属性：

| 属性名称                 | 描述                               |
| :----------------------- | :--------------------------------- |
| `Access Policy Provider` | 上面定义的访问策略提供商的标识符。 |

#### 文件授权人

文件授权已替换为上文所述更精细的标准管理授权方法。但是，由于向后兼容性原因，它仍然可用。文件授权人具有以下属性：

| 属性名称                       | 描述                                                         |
| :----------------------------- | :----------------------------------------------------------- |
| `Node Identity`                | NIFI聚类节点的身份。当聚类时，应定义每个节点的属性，以便每个节点了解所有其他节点。如果不进行聚类，这些属性可能会被忽略。 |
| `Authorizations File`          | 文件授权人存储策略的文件。默认情况下，选择目录中的*授权.xml。*`conf` |
| `Users File`                   | 文件授权人存储用户和组的文件。默认情况下，选择目录中的*用户.xml。*`conf` |
| `Initial Admin Identity`       | 初始管理员用户的身份，该用户被授予对 UI 的访问权限，并具有创建额外用户、组和策略的能力。此属性仅在未定义其他用户、组和策略时使用。 |
| `Legacy Authorized Users File` | 通往现有*授权用户的*完整路径.xml自动转换为多租户授权模式。此属性仅在未定义其他用户、组和策略时使用。 |

|      | *nifi.属性*中指定的任何身份映射规则也将应用于初始管理员身份，因此该值应为未映射标识。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

|      | *nifi.属性*中指定的任何身份映射规则也将应用于节点标识，因此值应是未映射的身份（即证书中的完整 DN）。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 初始管理员身份（新NIFI实例）

如果您是首次设置安全的 NiFi 实例，则必须在*授权人文件*中手动指定"初始管理员身份".xml文件。此初始管理员用户被授予对 UI 的访问权限，并具有创建更多用户、组和策略的能力。此属性的价值可能是 DN（使用证书或 LDAP 时）或 Kerberos 本金。如果您是 NiFi 管理员，请将自己添加为"初始管理员身份"。

编辑并保存*授权文件后.xml*重新启动 NiFi。在重新启动期间，用户和管理员身份和管理员策略*.xml*和*授权.xml*文件中添加了"初始管理员标识"用户和管理策略。一旦 NiFi 启动，"初始管理员身份"用户将能够访问 UI 并开始管理用户、组和策略。

|      | 对于全新的安全流，提供"初始管理员身份"使用户能够进入 UI 并管理用户、组和策略。但是，如果该用户想要开始修改流，他们需要为根过程组授予自己的策略。系统无法自动做到这一点，因为在新的流中，根过程组的 UUID 在流生成之前不会是永久性的*.xml.gz。*如果 NiFi 实例是从现有*流中升级.xml.gz*或从不安全到安全的 1.x 实例升级，则"初始管理员身份"用户将自动获得修改流的权限。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

下面描述了一些常用案例。

##### 基于文件（LDAP 认证）

下面是一个使用约翰·史密斯这个名字的LDAP条目示例：

```
<authorizers>
    <userGroupProvider>
        <identifier>file-user-group-provider</identifier>
        <class>org.apache.nifi.authorization.FileUserGroupProvider</class>
        <property name="Users File">./conf/users.xml</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Initial User Identity 1">cn=John Smith,ou=people,dc=example,dc=com</property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">file-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity">cn=John Smith,ou=people,dc=example,dc=com</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Node Identity 1"></property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

##### 基于文件（克贝罗斯身份验证）

下面是一个示例 Kerberos 条目使用名称约翰史密斯和领域：`NIFI.APACHE.ORG`

```
<authorizers>
    <userGroupProvider>
        <identifier>file-user-group-provider</identifier>
        <class>org.apache.nifi.authorization.FileUserGroupProvider</class>
        <property name="Users File">./conf/users.xml</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Initial User Identity 1">johnsmith@NIFI.APACHE.ORG</property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">file-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity">johnsmith@NIFI.APACHE.ORG</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Node Identity 1"></property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

##### 基于 LDAP 的用户/组引用用户 DN

下面是一个从 LDAP 加载用户和组的示例。集团成员身份将通过每个组的成员属性进行驱动。授权仍将使用基于文件的访问策略：

```
dn: cn=User 1,ou=users,o=nifi
objectClass: organizationalPerson
objectClass: person
objectClass: inetOrgPerson
objectClass: top
cn: User 1
sn: User1
uid: user1

dn: cn=User 2,ou=users,o=nifi
objectClass: organizationalPerson
objectClass: person
objectClass: inetOrgPerson
objectClass: top
cn: User 2
sn: User2
uid: user2

dn: cn=admins,ou=groups,o=nifi
objectClass: groupOfNames
objectClass: top
cn: admins
member: cn=User 1,ou=users,o=nifi
member: cn=User 2,ou=users,o=nifi

<authorizers>
    <userGroupProvider>
        <identifier>ldap-user-group-provider</identifier>
        <class>org.apache.nifi.ldap.tenants.LdapUserGroupProvider</class>
        <property name="Authentication Strategy">ANONYMOUS</property>

        <property name="Manager DN"></property>
        <property name="Manager Password"></property>

        <property name="TLS - Keystore"></property>
        <property name="TLS - Keystore Password"></property>
        <property name="TLS - Keystore Type"></property>
        <property name="TLS - Truststore"></property>
        <property name="TLS - Truststore Password"></property>
        <property name="TLS - Truststore Type"></property>
        <property name="TLS - Client Auth"></property>
        <property name="TLS - Protocol"></property>
        <property name="TLS - Shutdown Gracefully"></property>

        <property name="Referral Strategy">FOLLOW</property>
        <property name="Connect Timeout">10 secs</property>
        <property name="Read Timeout">10 secs</property>

        <property name="Url">ldap://localhost:10389</property>
        <property name="Page Size"></property>
        <property name="Sync Interval">30 mins</property>
        <property name="Group Membership - Enforce Case Sensitivity">false</property>

        <property name="User Search Base">ou=users,o=nifi</property>
        <property name="User Object Class">person</property>
        <property name="User Search Scope">ONE_LEVEL</property>
        <property name="User Search Filter"></property>
        <property name="User Identity Attribute">cn</property>
        <property name="User Group Name Attribute"></property>
        <property name="User Group Name Attribute - Referenced Group Attribute"></property>

        <property name="Group Search Base">ou=groups,o=nifi</property>
        <property name="Group Object Class">groupOfNames</property>
        <property name="Group Search Scope">ONE_LEVEL</property>
        <property name="Group Search Filter"></property>
        <property name="Group Name Attribute">cn</property>
        <property name="Group Member Attribute">member</property>
        <property name="Group Member Attribute - Referenced User Attribute"></property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">ldap-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity">John Smith</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Node Identity 1"></property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

根据值，从约翰·史密斯条目中加载的 cn 中会加载该值。`Initial Admin Identity``User Identity Attribute`

##### 基于 LDAP 的用户/组引用用户属性

下面是一个从 LDAP 加载用户和组的示例。组成员身份将通过每个组的成员 uid 属性进行驱动。授权仍将使用基于文件的访问策略：

```
dn: uid=User 1,ou=Users,dc=local
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: user1
cn: User 1

dn: uid=User 2,ou=Users,dc=local
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: user2
cn: User 2

dn: cn=Managers,ou=Groups,dc=local
objectClass: posixGroup
cn: Managers
memberUid: user1
memberUid: user2

<authorizers>
    <userGroupProvider>
        <identifier>ldap-user-group-provider</identifier>
        <class>org.apache.nifi.ldap.tenants.LdapUserGroupProvider</class>
        <property name="Authentication Strategy">ANONYMOUS</property>

        <property name="Manager DN"></property>
        <property name="Manager Password"></property>

        <property name="TLS - Keystore"></property>
        <property name="TLS - Keystore Password"></property>
        <property name="TLS - Keystore Type"></property>
        <property name="TLS - Truststore"></property>
        <property name="TLS - Truststore Password"></property>
        <property name="TLS - Truststore Type"></property>
        <property name="TLS - Client Auth"></property>
        <property name="TLS - Protocol"></property>
        <property name="TLS - Shutdown Gracefully"></property>

        <property name="Referral Strategy">FOLLOW</property>
        <property name="Connect Timeout">10 secs</property>
        <property name="Read Timeout">10 secs</property>

        <property name="Url">ldap://localhost:10389</property>
        <property name="Page Size"></property>
        <property name="Sync Interval">30 mins</property>
        <property name="Group Membership - Enforce Case Sensitivity">false</property>

        <property name="User Search Base">ou=Users,dc=local</property>
        <property name="User Object Class">posixAccount</property>
        <property name="User Search Scope">ONE_LEVEL</property>
        <property name="User Search Filter"></property>
        <property name="User Identity Attribute">cn</property>
        <property name="User Group Name Attribute"></property>
        <property name="User Group Name Attribute - Referenced Group Attribute"></property>

        <property name="Group Search Base">ou=Groups,dc=local</property>
        <property name="Group Object Class">posixGroup</property>
        <property name="Group Search Scope">ONE_LEVEL</property>
        <property name="Group Search Filter"></property>
        <property name="Group Name Attribute">cn</property>
        <property name="Group Member Attribute">memberUid</property>
        <property name="Group Member Attribute - Referenced User Attribute">uid</property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">ldap-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity">John Smith</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Node Identity 1"></property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

##### 复合材料 - 基于文件和LDAP的用户/组

下面是一个示例，综合实现加载用户和组从 LDAP 和本地文件。集团成员身份将通过每个组的成员属性进行驱动。只有当从文件中加载的用户在 UI 中可配置时，才会读取来自 LDAP 的用户。

```
dn: cn=User 1,ou=users,o=nifi
objectClass: organizationalPerson
objectClass: person
objectClass: inetOrgPerson
objectClass: top
cn: User 1
sn: User1
uid: user1

dn: cn=User 2,ou=users,o=nifi
objectClass: organizationalPerson
objectClass: person
objectClass: inetOrgPerson
objectClass: top
cn: User 2
sn: User2
uid: user2

dn: cn=admins,ou=groups,o=nifi
objectClass: groupOfNames
objectClass: top
cn: admins
member: cn=User 1,ou=users,o=nifi
member: cn=User 2,ou=users,o=nifi

<authorizers>
    <userGroupProvider>
        <identifier>file-user-group-provider</identifier>
        <class>org.apache.nifi.authorization.FileUserGroupProvider</class>
        <property name="Users File">./conf/users.xml</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Initial User Identity 1">cn=nifi-node1,ou=servers,dc=example,dc=com</property>
        <property name="Initial User Identity 2">cn=nifi-node2,ou=servers,dc=example,dc=com</property>
    </userGroupProvider>
    <userGroupProvider>
        <identifier>ldap-user-group-provider</identifier>
        <class>org.apache.nifi.ldap.tenants.LdapUserGroupProvider</class>
        <property name="Authentication Strategy">ANONYMOUS</property>

        <property name="Manager DN"></property>
        <property name="Manager Password"></property>

        <property name="TLS - Keystore"></property>
        <property name="TLS - Keystore Password"></property>
        <property name="TLS - Keystore Type"></property>
        <property name="TLS - Truststore"></property>
        <property name="TLS - Truststore Password"></property>
        <property name="TLS - Truststore Type"></property>
        <property name="TLS - Client Auth"></property>
        <property name="TLS - Protocol"></property>
        <property name="TLS - Shutdown Gracefully"></property>

        <property name="Referral Strategy">FOLLOW</property>
        <property name="Connect Timeout">10 secs</property>
        <property name="Read Timeout">10 secs</property>

        <property name="Url">ldap://localhost:10389</property>
        <property name="Page Size"></property>
        <property name="Sync Interval">30 mins</property>
        <property name="Group Membership - Enforce Case Sensitivity">false</property>

        <property name="User Search Base">ou=users,o=nifi</property>
        <property name="User Object Class">person</property>
        <property name="User Search Scope">ONE_LEVEL</property>
        <property name="User Search Filter"></property>
        <property name="User Identity Attribute">cn</property>
        <property name="User Group Name Attribute"></property>
        <property name="User Group Name Attribute - Referenced Group Attribute"></property>

        <property name="Group Search Base">ou=groups,o=nifi</property>
        <property name="Group Object Class">groupOfNames</property>
        <property name="Group Search Scope">ONE_LEVEL</property>
        <property name="Group Search Filter"></property>
        <property name="Group Name Attribute">cn</property>
        <property name="Group Member Attribute">member</property>
        <property name="Group Member Attribute - Referenced User Attribute"></property>
    </userGroupProvider>
    <userGroupProvider>
        <identifier>composite-user-group-provider</identifier>
        <class>org.apache.nifi.authorization.CompositeConfigurableUserGroupProvider</class>
        <property name="Configurable User Group Provider">file-user-group-provider</property>
        <property name="User Group Provider 1">ldap-user-group-provider</property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">composite-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity">John Smith</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Node Identity 1">cn=nifi-node1,ou=servers,dc=example,dc=com</property>
        <property name="Node Identity 2">cn=nifi-node2,ou=servers,dc=example,dc=com</property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

在此示例中，用户和组从 LDAP 加载，但服务器在本地文件中进行管理。该值来自基于 "" 的 LDAP 条目中的属性。值使用属性在本地文件中建立。`Initial Admin Identity``User Identity Attribute``Node Identity``Initial User Identity`

#### 传统授权用户（NiFi 实例升级）

如果您正在从 0.x NiFi 实例升级，您可以将以前配置的用户和角色转换为多租户授权模式。在*授权文件.xml*文件中，指定您现有*授权用户的位置.xml*文件在属性中的位置。`Legacy Authorized Users File`

下面是示例条目：

```
<authorizers>
    <userGroupProvider>
        <identifier>file-user-group-provider</identifier>
        <class>org.apache.nifi.authorization.FileUserGroupProvider</class>
        <property name="Users File">./conf/users.xml</property>
        <property name="Legacy Authorized Users File">/Users/johnsmith/config_files/authorized-users.xml</property>

        <property name="Initial User Identity 1"></property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">file-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity"></property>
        <property name="Legacy Authorized Users File">/Users/johnsmith/config_files/authorized-users.xml</property>

        <property name="Node Identity 1"></property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

编辑并保存*授权文件后.xml*重新启动 NiFi。*授权用户.xml文件中的用户*和角色被转换并添加为*用户.xml*和*授权*.xml文件中的身份和策略。一旦应用程序开始，以前具有传统管理员角色的用户可以访问 UI 并开始管理用户、组和策略。

下表总结了如果 NiFi 实例具有现有流程，则分配给每个旧角色的全球和组件策略*.xml.gz：*

##### 全球访问政策

|                              | 管理  | 德夫姆 | 监控  | 种源  | NIFI  | 代理  |
| ---------------------------: | :---: | :----: | :---: | :---: | :---: | :---: |
|                  **查看 UI** | ***** | *****  | ***** |       |       |       |
|        **访问控制器 - 视图** | ***** | *****  | ***** |       | ***** |       |
|        **访问控制器 - 修改** |       | *****  |       |       |       |       |
|    **访问参数上下文 - 查看** |       |        |       |       |       |       |
|    **访问参数上下文 - 修改** |       |        |       |       |       |       |
|                 **查询来源** |       |        |       | ***** |       |       |
|         **访问受限制的组件** |       | *****  |       |       |       |       |
|      **访问所有策略 - 查看** | ***** |        |       |       |       |       |
|      **访问所有策略 - 修改** | ***** |        |       |       |       |       |
|   **访问用户/用户组 - 查看** | ***** |        |       |       |       |       |
|   **访问用户/用户组 - 修改** | ***** |        |       |       |       |       |
| **检索站点到站点的详细信息** |       |        |       |       | ***** |       |
|             **查看系统诊断** |       | *****  | ***** |       |       |       |
|             **代理用户请求** |       |        |       |       |       | ***** |
|               **访问计数器** |       |        |       |       |       |       |

##### 根过程组的组件访问策略

|              | 管理  | 德夫姆 | 监控  | 种源  | NIFI | 代理  |
| -----------: | :---: | :----: | :---: | :---: | :--: | :---: |
| **查看组件** | ***** | *****  | ***** |       |      |       |
| **修改组件** |       | *****  |       |       |      |       |
| **查看数据** |       | *****  |       | ***** |      | ***** |
| **修改数据** |       | *****  |       |       |      | ***** |
| **查看来源** |       |        |       | ***** |      |       |

有关表中单个策略的详细信息，请参阅[访问策略](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#access-policies)。

|      | 如果存在该属性和属性的值，NiFi 将无法重新启动。您只能指定其中一个值来初始化授权。`Initial Admin Identity``Legacy Authorized Users File` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

|      | 不要手动编辑*授权.xml*文件。仅在初始设置期间和之后使用 NiFi UI 创建授权。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 集群节点身份

如果您在聚类环境中运行 NiFi，则必须指定每个节点的身份。节点通信所需的授权策略是在启动期间创建的。

例如，如果您正在为每个节点设置一个带有以下 DN 的 2 节点聚类：

```
cn=nifi-1,ou=people,dc=example,dc=com
cn=nifi-2,ou=people,dc=example,dc=com
<authorizers>
    <userGroupProvider>
        <identifier>file-user-group-provider</identifier>
        <class>org.apache.nifi.authorization.FileUserGroupProvider</class>
        <property name="Users File">./conf/users.xml</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Initial User Identity 1">johnsmith@NIFI.APACHE.ORG</property>
        <property name="Initial User Identity 2">cn=nifi-1,ou=people,dc=example,dc=com</property>
        <property name="Initial User Identity 3">cn=nifi-2,ou=people,dc=example,dc=com</property>
    </userGroupProvider>
    <accessPolicyProvider>
        <identifier>file-access-policy-provider</identifier>
        <class>org.apache.nifi.authorization.FileAccessPolicyProvider</class>
        <property name="User Group Provider">file-user-group-provider</property>
        <property name="Authorizations File">./conf/authorizations.xml</property>
        <property name="Initial Admin Identity">johnsmith@NIFI.APACHE.ORG</property>
        <property name="Legacy Authorized Users File"></property>

        <property name="Node Identity 1">cn=nifi-1,ou=people,dc=example,dc=com</property>
        <property name="Node Identity 2">cn=nifi-2,ou=people,dc=example,dc=com</property>
    </accessPolicyProvider>
    <authorizer>
        <identifier>managed-authorizer</identifier>
        <class>org.apache.nifi.authorization.StandardManagedAuthorizer</class>
        <property name="Access Policy Provider">file-access-policy-provider</property>
    </authorizer>
</authorizers>
```

|      | 在群集中，所有节点必须具有相同的*授权.xml*和*用户.xml。*唯一的例外是，如果节点在加入组之前具有空*授权.xml*和*用户.xml*文件。在此方案中，节点在启动期间从组中继承它们。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

现在，已创建初始授权，可以在 NiFi UI 中创建和管理其他用户、组和授权。

### 配置用户和访问策略

根据配置的用户群提供者和 Access 政策提供者的功能，用户、组和策略将在 UI 中进行配置。如果扩展不可配置，则用户、组和策略将仅在 UI 中读取。如果配置的授权人不使用用户群提供器和 Access 政策提供者，则用户和策略可能根据基本实现在 UI 中可见且可配置。

本节假设用户、组和策略在 UI 中可配置，并描述：

- 如何创建用户和组
- 如何使用访问策略来定义授权
- 如何查看设置在用户身上的策略
- 如何通过浏览特定示例来配置访问策略

|      | 需要与 UI 交互的说明假定应用正被用户 1 访问，用户具有管理员特权，如"初始管理员身份"用户或已转换的旧管理员用户（参见[授权人.xml设置](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#authorizers-setup)）。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 创建用户和组

从 UI 中，从全球菜单中选择"用户"。这将打开对话以创建和管理用户和组。

![NIFI用户对话](https://cdn.jsdelivr.net/gh/zshipu/images/202111011330904.png)

单击"添加"图标 （![添加用户图标](https://cdn.jsdelivr.net/gh/zshipu/images/202111011337434.png)).要创建用户，请输入与为保护您的 NiFi 实例而选择的身份验证方法相关的"身份"信息。单击"确定"。

![User Creation Dialog](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331100.png)

要创建组，请选择"组"无线电按钮，输入组的名称并选择要包含在组中的用户。单击"确定"。

![Group Creation Dialog](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331860.png)

#### 访问策略

您可以管理用户和组使用"访问策略"查看或修改 NiFi 资源的能力。有两种类型的访问策略可以应用于资源：

- 查看 - 如果为资源创建了查看策略，则只有添加到该策略中的用户或组才能查看该资源的详细信息。
- 修改 • 如果资源具有修改策略，则只有添加到该策略中的用户或组才能更改该资源的配置。

您可以在全球和组件级别创建和应用访问策略。

##### 全球访问政策

全球访问政策管辖以下系统级别授权：

| 政策                     | 特权                                                         | 全球菜单选择 | 资源描述符               |
| :----------------------- | :----------------------------------------------------------- | :----------- | :----------------------- |
| 查看 UI                  | 允许用户查看 UI                                              | 不适用       | `/flow`                  |
| 访问控制器               | 允许用户查看/修改控制器，包括集群中的报告任务、控制器服务、参数上下文和节点 | 控制器设置   | `/controller`            |
| 访问参数上下文           | 允许用户查看/修改参数上下文。除非被推翻，否则从"访问控制器"策略中继承了对参数上下文的访问。 | 参数上下文   | `/parameter-contexts`    |
| 查询来源                 | 允许用户提交证明搜索并请求事件血统                           | 数据证明     | `/provenance`            |
| 访问受限制的组件         | 允许用户创建/修改受限组件，前提是其他权限足够。受限组件可能指示需要哪些特定权限。可授予特定限制的权限，或授予任何限制。如果无论限制如何，都授予许可，用户可以创建/修改所有受限组件。 | 不适用       | `/restricted-components` |
| 访问所有策略             | 允许用户查看/修改所有组件的策略                              | 政策         | `/policies`              |
| 访问用户/用户组          | 允许用户查看/修改用户组                                      | 用户         | `/tenants`               |
| 检索站点到站点的详细信息 | 允许其他 NiFi 实例检索站点到站点的详细信息                   | 不适用       | `/site-to-site`          |
| 查看系统诊断             | 允许用户查看系统诊断                                         | 总结         | `/system`                |
| 代理用户请求             | 允许代理机器代表他人发送请求                                 | 不适用       | `/proxy`                 |
| 访问计数器               | 允许用户查看/修改计数器                                      | 计数器       | `/counters`              |

##### 组件级别访问策略

组件级别访问策略管理以下组件级别授权：

| 政策                   | 特权                                                         | 资源描述符和操作                                             |
| :--------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 查看组件               | 允许用户查看组件配置详细信息                                 | `resource="/<component-type>/<component-UUID>" action="R"`   |
| 修改组件               | 允许用户修改组件配置详细信息                                 | `resource="/<component-type>/<component-UUID>" action="W"`   |
| 操作组件               | 允许用户通过更改组件运行状态（启动/停止/启用/禁用）、远程端口传输状态或终止处理器线程来操作组件 | `resource="/operation/<component-type>/<component-UUID>" action="W"` |
| 查看来源               | 允许用户查看此组件生成的起源事件                             | `resource="/provenance-data/<component-type>/<component-UUID>" action="R"` |
| 查看数据               | 允许用户在出站连接中的流文件队列中以及通过源事件查看该组件的元数据和内容 | `resource="/data/<component-type>/<component-UUID>" action="R"` |
| 修改数据               | 允许用户在出站连接中清空流文件队列，并通过源事件提交重播     | `resource="/data/<component-type>/<component-UUID>" action="W"` |
| 查看策略               | 允许用户查看可以查看/修改组件的用户列表                      | `resource="/policies/<component-type>/<component-UUID>" action="R"` |
| 修改策略               | 允许用户修改可以查看/修改组件的用户列表                      | `resource="/policies/<component-type>/<component-UUID>" action="W"` |
| 通过站点到站点接收数据 | 允许端口接收来自 NiFi 实例的数据                             | `resource="/data-transfer/input-ports/<port-UUID>" action="W"` |
| 通过站点到站点发送数据 | 允许端口从 NiFi 实例发送数据                                 | `resource="/data-transfer/output-ports/<port-UUID>" action="W"` |

|      | 您可以将访问策略应用于除连接以外的所有组件类型。连接授权由连接源和目的地组件上的单独访问策略以及包含组件的流程组的访问策略推断。这在下面[的"创建连接](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#creating-a-connection)"和["编辑连接](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#editing-a-connection)"示例中进行了更详细的讨论。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

|      | 为了访问列表队列或删除队列以获取连接，用户需要获得组件上的"查看数据"和"修改数据"策略的权限。在聚类环境中，还必须在这些策略中添加所有节点，因为用户请求可以通过集合中的任何节点进行复制。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

##### 访问策略继承

管理员不需要手动为数据流中的每个组件创建策略。为了减少管理员在授权管理上花费的时间，政策从家长资源继承到儿童资源。例如，如果允许用户访问查看和修改流程组，则用户还可以查看和修改流程组中的组件。策略继承使管理员能够同时分配策略，并让策略在整个数据流中适用。

您可以覆盖继承的策略（如下[所示，请转动处理器](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#moving-a-processor)示例）。覆盖策略会删除继承的政策，打破从父母到孩子的继承链，并创建一个替换策略，根据需要添加用户。可以通过删除替换策略来恢复继承的策略及其用户。

|      | "查看策略"和"修改策略"组件级别的访问策略是此继承行为的例外。当用户被添加到任一策略中时，它们被添加到当前管理员列表中。它们不会凌驾于上级管理员的统治下。因此，仅显示"查看策略"和"修改策略"访问策略的组件特定管理员。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

|      | 您不能根据继承的策略修改用户/组。用户和组只能从父策略或覆盖策略中添加或删除。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 查看用户策略

从 UI 中，从全球菜单中选择"用户"。这将打开 NiFi 用户对话。

![User Policies Window](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331966.png)

选择查看用户策略图标 （![User Policies Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331065.png)).

![User Policies Detail](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331325.png)

用户策略窗口显示已为选定用户设置的全球和组件级别策略。选择"去"图标 （![Go To Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011337376.png)）导航到画布中的该组件。

#### 访问策略配置示例

了解如何创建和应用访问策略的最有效方法是浏览一些常见示例。以下方案假定用户 1 是管理员，而用户 2 是仅获得 UI 访问权限的新添加用户。

让我们从画布上的两个处理器开始，作为我们的起点：生成流文件和日志属性。

![Access Policy Config Start](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331892.png)

用户1可以将组件添加到数据流中，并能够移动、编辑和连接所有处理器。用户1可以看到根过程组和处理器的详细信息和属性。

![User1 Full Access](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331147.png)

用户 1 希望保持其当前对数据流及其组件的特权。

用户 2 无法将组件添加到数据流中，也无法移动、编辑或连接组件。根过程组和处理器的详细信息和属性隐藏在用户 2 中。

![User2 Restricted Access](https://cdn.jsdelivr.net/gh/zshipu/images/202111011331166.png)

##### 移动处理器

要允许用户 2 在数据流中移动生成流文件处理器，并且仅移动该处理器，用户 1 执行以下步骤：

1. 选择生成流文件处理器，以便突出显示。

2. 选择访问策略图标 （![Access Policies Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332879.png)） 从操作调色板和访问策略对话打开。

3. 从策略下拉中选择"修改组件"。处理器（子）上目前存在的"修改组件"策略是从用户1拥有特权的根过程组（父级）继承下来的"修改组件"策略。

   ![Processor Modify Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332669.png)

4. 选择策略继承消息中的覆盖链接。在创建替换策略时，您可以选择使用继承策略的副本或空策略进行覆盖。选择覆盖按钮以创建副本。

   ![Create Override Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332348.png)

5. 在创建的替换策略上，选择"添加用户"图标 （![添加用户图标](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332508.png)).在用户身份字段中查找或输入用户 2 并选择"确定"。通过这些更改，用户 1 能够在画布上移动两个处理器。用户 2 现在可以移动生成流文件处理器，但不能移动日志属性处理器。

   ![Processor Replacement Modify Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332737.png)

   ![User2 Moved Processor](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332954.png)

##### 编辑处理器

在上面的"移动处理器"示例中，用户 2 被添加到生成流文件的"修改组件"策略中。如果没有查看处理器属性的能力，用户 2 无法修改处理器的配置。为了编辑组件，用户必须同时使用"查看组件"和"修改组件"策略。要实现此，用户 1 执行以下步骤：

1. 选择生成流文件处理器。

2. 选择访问策略图标 （![Access Policies Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011338972.png)） 从操作调色板和访问策略对话打开。

3. 从策略下拉中选择"查看组件"。目前存在于处理器（儿童）上的"组件"策略是从用户1拥有特权的根过程组（父级）继承的"查看组件"策略。

   ![Processor View Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011332724.png)

4. 选择策略继承消息中的覆盖链接，保留副本策略的默认值并选择覆盖按钮。

5. 在创建的覆盖策略上，选择添加用户图标 （![添加用户图标](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333956.png)).在用户身份字段中查找或输入用户 2 并选择"确定"。通过这些更改，用户 1 能够查看和编辑画布上的处理器。用户2现在可以查看和编辑生成流文件处理器。

   ![Processor Replacement View Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333506.png)

   ![User2 Edit Processor](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333558.png)

##### 创建连接

在前两个示例中所述的访问策略配置中，用户 1 能够将生成流文件连接到日志属性：

![User1 Create Connection](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333570.png)

用户2 无法进行连接：

![User2 No Connection](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333936.png)

这是因为：

- 用户 2 在流程组上没有修改访问权限。
- 即使用户 2 能够查看和修改源组件（生成流文件），用户 2 在目的地组件（日志属性）上也没有访问策略。

要允许用户 2 将生成流文件连接到日志属性，如用户1：

1. 选择根过程组。操作调色板更新了根过程组的详细信息。
2. 选择访问策略图标 （![Access Policies Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333981.png)) 从操作调色板和访问策略对话打开。
3. 从策略下拉中选择"修改组件"。![Process Group Modify Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333510.png)
4. 选择添加用户图标 （![添加用户图标](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333726.png)).查找或输入用户2 并选择"确定"。

![Process Group Modify Policy Add User2](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333618.png)

通过在流程组的"修改组件"策略中添加用户2，则通过策略继承将用户2添加到日志属性处理器上的"修改组件"策略中。要确认这一点，请突出显示日志属性处理器并选择访问策略图标 （![Access Policies Icon](http://nifi.apache.org/docs/nifi-docs/html/images/iconAccessPolicies.png)） 从操作调色板：

![User2 Inherited Edit Processor](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333615.png)

通过这些更改，用户 2 现在可以将生成流文件处理器连接到日志属性处理器。

![User2 Can Connect](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333297.png)

![User2 Connected Processors](https://cdn.jsdelivr.net/gh/zshipu/images/202111011333646.png)

##### 编辑连接

假设用户 1 或用户 2 向根过程组添加了替换文本处理器：

![ReplaceText Processor Added](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334976.png)

用户 1 可以选择并更改现有连接（生成流文件与日志属性之间），以连接生成流文件以替换文本：

![User1 Edit Connection](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334325.png)

用户 2 无法执行此操作。

![User2 No Edit Connection](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334477.png)

要允许用户 2 将生成流文件连接到替换文本，如用户 1：

1. 选择根过程组。操作调色板更新了根过程组的详细信息。
2. 选择访问策略图标 （![Access Policies Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334596.png)).
3. 从策略下拉中选择"查看组件"。![Process Group View Policy](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334216.png)
4. 选择添加用户图标 （![添加用户图标](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334139.png)).查找或输入用户2 并选择"确定"。

![Process Group View Policy Add User2](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334796.png)

用户2 被添加到处理组的视图和修改策略中，现在可以将生成流文件处理器连接到替换文本处理器。

![User2 Edit Connection](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334301.png)

## 加密配置

本节概述了 NiFi 加密和解密数据的能力。

加密通信处理器允许对数据进行加密和解密，包括内部到 NiFi 以及与外部系统（如其他数据源和消费者）集成。`openssl`

### 关键衍生功能

关键衍生功能 （KDF） 是将人读信息（通常是密码或其他机密信息）转换为适合数据保护的加密密钥的机制。有关进一步的信息，请阅读[维基百科关于关键衍生功能的条目](https://en.wikipedia.org/wiki/Key_derivation_function)。目前，KDF 被实现所摄入，并返回用于加密或解密的完全初始化对象。由于使用 a， KDF 目前无法定制。未来的增强措施将包括在初始化时向 KDF 提供自定义成本参数的能力。作为一个解决，实例可以初始化与自定义成本参数在构造器中，但目前不支持。如果您不需要特定的 KDF，**则建议使用 Argon2，**因为它是一种坚固、安全、性能好且用户友好的默认值，并在多个平台上得到广泛支持。以下是目前由 NiFi 支持的 KDF（主要在基于密码的加密处理器 （PBE） 中）和相关说明：`CipherProvider``Cipher``CipherProviderFactory``CipherProvider``CipherProviderFactory``EncryptContent`

#### NIFI遗产 Kdf

- NiFi 用于 PBE 内部密钥派生的原始 KDF，这是 MD5 文摘在密码串联上的 1000 次迭代和 8 或 16 字节的随机盐（盐长度取决于选定的密码块大小）。
- 此 KDF**在 NiFi 0.5.0 之前被弃用**，仅应用于向后兼容性，以解密以前由 NiFi 传统版本加密的数据。

#### 开放SL PKCS#5 v1.5 EVP_BytesToKey

- 此 KDF 添加到 v0.4.0 中。
- 此 KDF 提供与使用 OpenSSL 默认 PBE 加密的数据的兼容性，称为 。这是 MD5 在密码的串联和随机 ASCII 盐的 8 字节上的单次迭代。OpenSSL 建议使用密钥源，但不会将命令线工具所需的库方法暴露给该工具，因此此 KDF 仍然是命令线加密的实际默认值。`EVP_BytesToKey``PBKDF2`

#### 布里普特

- 此 KDF 在 v0.5.0 中添加。

- [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt)是基于[吹鱼](https://en.wikipedia.org/wiki/Blowfish_(cipher))密码的自适应功能。此 KDF 建议，因为它自动包含随机 16 字节盐、可配置成本参数（或"工作因子"），并通过要求在密钥推导期间访问"大"内存块来硬化，以抵御使用[GPGPU（](https://en.wikipedia.org/wiki/General-purpose_computing_on_graphics_processing_units)内核之间共享内存）的蛮力攻击。它对[FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array)蛮力攻击的抵抗力较低，因为门阵列可以访问单独的嵌入式 RAM 块。

- 由于 Bcrypt 衍生哈希的长度始终为 184 位，因此将哈希输出（不包括算法、工作因子或盐）输入消化并截断为所需的键长度。这提供了雪崩效应对输入的好处。这一关键的拉伸机制是在阿帕奇NIFI1.12.0中引入的。`SHA-512`

  |      | 在此之前，向SHA-512消化功能提供了*完整的输出*（算法、工作因子、盐和哈希输出共480位）。NiFi 可以使用通过此旧过程导出的密钥透明地处理解密数据（低于 10 MiB）加密。 |
  | ---- | ------------------------------------------------------------ |
  |      |                                                              |

- 建议的最小工作系数为 12 （2）12关键衍生轮）（截至2016年2月1日商品硬件），应提高到合法系统遇到有害延迟的阈值（见下面的时间表或用于计算安全最低值）。`BcryptCipherProviderGroovyTest#testDefaultConstructorShouldProvideStrongWorkFactor()`

- 盐格式是。盐被划定，三个部分如下：`$2a$10$ABCDEFGHIJKLMNOPQRSTUV``$`

  - `2a`- 格式的版本。[这里](http://blog.ircmaxell.com/2012/12/seven-ways-to-screw-up-bcrypt.html)可以找到一个广泛的解释。NiFi 目前用于内部生成的所有盐。`2a`

  - `10`- 工作因素。这实际上是日志2值，因此总迭代计数为 210（1024） 在这种情况下。

  - `ABCDEFGHIJKLMNOPQRSTUV`- 22 个字符，Radix64 编码，未加垫，生盐值。此解码到关键推导中使用的 16 字节盐。

    |      | Bcrypt Radix64 编码与标准 MIME Base64 编码**不**兼容。 |
    | ---- | ------------------------------------------------------ |
    |      |                                                        |

#### 克里普特

- 此 KDF 在 v0.5.0 中添加。
- [Scrypt](https://en.wikipedia.org/wiki/Scrypt)是一种适应功能，专为响应而设计。建议使用此 KDF，因为它需要相对大量的内存才能进行每次推导，使其对硬件蛮力攻击具有抵抗力。`bcrypt`
- 建议的最低成本为 +2`N`14（16，384），+8，+1（截至2016年2月1日商品硬件）。 必须是一个积极的整数，小于消化功能输出的八分之一的长度（32 代表 SHA-256），并且是混合函数输出的八分之一的长度，定义为 。这些参数应增加到合法系统遇到有害延迟的阈值（请参阅下面的时间表或用于计算安全最低值）。`r``p``p``(2^32 − 1) * (Hlen/MFlen)``Hlen``MFlen``r * 128``ScryptCipherProviderGroovyTest#testDefaultConstructorShouldProvideStrongParameters()`
- 盐格式是。盐被划定，三个部分如下：`$s0$e0101$ABCDEFGHIJKLMNOPQRSTUV``$`
  - `s0`- 格式的版本。NiFi 目前用于内部生成的所有盐。`s0`
  - `e0101`- 成本参数。这实际上是一个六角形编码，使用班次。这可以形成/分析使用和。`N``r``p``Scrypt#encodeParams()``Scrypt#parseParameters()`
    - 一些外部库编码，并单独以形式（存储在六角形编码，即，或2`N``r``p``$4000$1$1$``N``0x4000``0d16384`14作为 = ）可用实用方法，将外部表单转换为内部表单。`0xe``0d14``ScryptCipherProvider#translateSalt()`
  - `ABCDEFGHIJKLMNOPQRSTUV`- 12-44 字符，Base64 编码，未调用，生盐值。这解码到关键衍生物中使用的 8-32 字节盐。

#### PBKDF2

- 此 KDF 在 v0.5.0 中添加。
- [基于密码的关键推导函数 2](https://en.wikipedia.org/wiki/PBKDF2)是一种自适应派生函数，它使用内部伪多功能 （PRF），并通过密码和盐（至少 16 字节）迭代多次。
- 建议PRF为或。使用 HMAC 加密哈希函数可以减轻长度扩展攻击。`HMAC/SHA-256``HMAC/SHA-512`
- 建议的最低迭代数为 160，000 次（截至 2016 年 2 月 1 日商品硬件）。此数字应每两年翻一番（请参阅下面的时间表或用于计算安全最低值）。`PBKDF2CipherProviderGroovyTest#testDefaultConstructorShouldProvideStrongIterationCount()`
- 此 KDF 并不难记忆（可以与商品硬件大规模并行），但仍被[NIST SP 800-132 （PDF）](http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf)和许多密码学家推荐为足够（当与适当的迭代计数和 HMAC 加密哈希功能一起使用时）。

#### 没有

- 此 KDF 在 v0.5.0 中添加。
- 此 KDF 不会对输入执行操作，并且是指示向密码提供原始密钥的标记。密钥必须在六角编码中提供，并且对于相关的密码/算法具有有效的长度。

#### 阿贡2

- 此 KDF 在 v1.12.0 中添加。
- [Argon2](https://en.wikipedia.org/wiki/Argon2)是 2015 年赢得密码哈希竞赛的关键衍生功能。此 KDF 建议，因为它提供了多种模式，可以针对预防 GPU 攻击、防止侧通道攻击或两者兼有。它允许可变输出键长度。
- 建议的最低成本为 +2`memory`16（65，536） KiB， +5， +8 （截至 2020 年 4 月 22 日商品硬件） 。[Argon2 规范文件 （PDF）](https://password-hashing.net/argon2-specs.pdf)第 9 节描述了用于确定推荐参数的算法。这些参数应增加到合法系统遇到有害延迟的阈值（用于计算安全最低值）。`iterations``parallelism``Argon2SecureHasherTest#testDefaultCostParamsShouldBeSufficient()`
- 盐格式是。盐被划定，四个部分如下：`$argon2id$v=19$m=65536,t=5,p=8$ABCDEFGHIJKLMNOPQRSTUV``$`
  - `argon2id`- 算法的"类型"（， ， ） 。NiFi 目前用于内部生成的所有盐。`2i``2d``2id``argon2id`
  - `v=19`- 小数算法的版本 （ = ） 。NiFi 目前用于内部生成的所有盐。`0d19``0x13``0d19`
  - `m=65536,t=5,p=8`- 成本参数。这包含按顺序排列的内存、迭代和并行。
  - `ABCDEFGHIJKLMNOPQRSTUV`- 12-44 字符，Base64 编码，未调用，生盐值。这解码到关键衍生物中使用的 8-32 字节盐。

##### 额外资源

- [最佳成本参数和关系的解释](http://stackoverflow.com/a/30308723/70465)
- [NIST 特别出版物 800-132](http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf)
- [OWASP 密码存储工作因子计算](https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet#Work_Factor)
- [PBKDF2 轮计算](http://security.stackexchange.com/a/3993/16485)
- [克里普特作为 KDF 与密码存储漏洞](http://blog.ircmaxell.com/2014/03/why-i-dont-recommend-scrypt.html)
- [克里普特 vs. 布莱普特 （截至 2010 年）](http://security.stackexchange.com/a/26253/16485)
- [布里普特 vs Pbkdf2](http://security.stackexchange.com/a/6415/16485)
- [为 Bcrypt 选择工作因子](http://wildlyinaccurate.com/bcrypt-choosing-a-work-factor/)
- [春季安全 Bcrypt](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/crypto/bcrypt/BCrypt.html)
- [开放式 EVP 字节到关键 PKCS#1v1.5](https://www.openssl.org/docs/man1.1.0/crypto/EVP_BytesToKey.html)
- [开放式 PBKDF2 KDF](https://wiki.openssl.org/index.php/Manual:PKCS5_PBKDF2_HMAC(3))
- [开放式 KDF 缺陷描述](http://security.stackexchange.com/a/29139/16485)

### 盐和IV编码

最初，处理器有一个从用户提供的密码中提取加密密钥的单一方法。这现在被称为模式，有效地。在 v0.4.0 中，添加了另一种源入密钥的方法，以便使用命令线工具与 NiFi 外部加密的内容兼容。这两[种关键衍生函数](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#key-derivation-functions)（KDF） 都有硬编码的消化功能和迭代计数，盐格式也是硬编码的。在 v0.5.0 中，引入了附加 KDF 以及可变迭代计数、工作因子和盐格式。此外，还引入*了原始密钥*加密。这需要将任意盐和初始化矢量 （IV） 编码到密码流中，以便 NiFi 或后续系统恢复解密这些消息。`EncryptContent``NiFiLegacy``MD5 digest, 1000 iterations``OpenSSL PKCS#5 v1.5 EVP_BytesToKey``openssl`

对于现有的 KDF，盐格式未更改。

#### NIFI遗产

输入的前 8 或 16 字节是盐。盐长度根据选定的算法的密码块长度确定。如果无法确定密码块大小（如流密码），则使用 8 字节的默认值。解密时，盐被读入并结合密码来获得加密密钥和 IV。`RC4`

![NiFi Legacy Salt Encoding](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334213.png)

#### 开放SL PKCS#5 v1.5 EVP_BytesToKey

OpenSSL 允许盐渍或无盐键派生。**未盐化密钥衍生是一种安全风险，不建议。*如果存在盐，输入的前 8 字节是 ASCII 字符串"Salted__"（），接下来的 8 字节是 ASCII 编码的盐。解密时，盐被读入并结合密码来获得加密密钥和 IV。如果没有盐头，则整个输入被视为密码文本。`0x53 61 6C 74 65 64 5F 5F`

![OpenSSL Salt Encoding](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334304.png)

对于新的 KDF，每个 KDF 都允许非确定性 IV，IV 必须与密码文本一起存储。这不是一个漏洞，因为 IV 不需要保密，而只是对于使用相同密钥加密的邮件来说，它是唯一的，以减少加密攻击的成功。对于这些 KDF，输出由盐组成，其次是盐分界器，UTF-8 字符串"NiFiSALT"（）和 IV，然后是 IV 划界器，UTF-8 字符串"NiFiIV"（），然后是密码文本。`0x4E 69 46 69 53 41 4C 54``0x4E 69 46 69 49 56`

#### 布里普特， 克里普特， Pbkdf2， 阿贡 2

![Bcrypt Salt & IV Encoding](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334042.png)

![Scrypt Salt & IV Encoding](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334552.png)

![PBKDF2 Salt & IV Encoding](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334208.png)

![Argon2 Salt & IV Encoding](https://cdn.jsdelivr.net/gh/zshipu/images/202111011334939.png)

### Java密码扩展 （JCE） 有限强度管辖权策略

由于美国的出口法规，默认的合资企业对它们可用[的加密操作强度施加了限制](http://docs.oracle.com/javase/7/docs/technotes/guides/security/SunProviders.html#importlimits)。例如，AES 操作默认仅限于。虽然加密安全，但可能会产生意想不到的后果，特别是在基于密码的加密 （PBE） 上。`128 bit keys``AES-128`

PBE 是从*用户提供的秘密材料*（通常是密码）中提取加密密钥进行加密或解密的过程。而不是人类记住一个（随机出现）32或64字符六角形字符串，使用密码或密码短语。

NiFi 提供的一些 PBE 算法由于基础密钥长度检查，对密码的长度施加了严格的限制。下面是一张表格，其中列出了加密强度有限的 JVM 上的最大密码长度。

| 算法                                 | 最大密码长度 |
| :----------------------------------- | :----------- |
| `PBEWITHMD5AND128BITAES-CBC-OPENSSL` | 16           |
| `PBEWITHMD5AND192BITAES-CBC-OPENSSL` | 16           |
| `PBEWITHMD5AND256BITAES-CBC-OPENSSL` | 16           |
| `PBEWITHMD5ANDDES`                   | 16           |
| `PBEWITHMD5ANDRC2`                   | 16           |
| `PBEWITHSHA1ANDRC2`                  | 16           |
| `PBEWITHSHA1ANDDES`                  | 16           |
| `PBEWITHSHAAND128BITAES-CBC-BC`      | 7            |
| `PBEWITHSHAAND192BITAES-CBC-BC`      | 7            |
| `PBEWITHSHAAND256BITAES-CBC-BC`      | 7            |
| `PBEWITHSHAAND40BITRC2-CBC`          | 7            |
| `PBEWITHSHAAND128BITRC2-CBC`         | 7            |
| `PBEWITHSHAAND40BITRC4`              | 7            |
| `PBEWITHSHAAND128BITRC4`             | 7            |
| `PBEWITHSHA256AND128BITAES-CBC-BC`   | 7            |
| `PBEWITHSHA256AND192BITAES-CBC-BC`   | 7            |
| `PBEWITHSHA256AND256BITAES-CBC-BC`   | 7            |
| `PBEWITHSHAAND2-KEYTRIPLEDES-CBC`    | 7            |
| `PBEWITHSHAAND3-KEYTRIPLEDES-CBC`    | 7            |
| `PBEWITHSHAANDTWOFISH-CBC`           | 7            |

### 允许不安全的加密模式

默认情况下，处理器设置中的属性设置为 。这意味着，如果提供了少于字符的密码，将发生验证错误。10 个字符是一个保守的估计值，没有考虑完整的熵计算、模式等。`Allow Insecure Cryptographic Modes``EncryptContent``not-allowed``10`

![Allow Insecure Cryptographic Modes](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335884.png)

在强度加密的 JVM 上，某些 PBE 算法将最大密码长度限制为 7，在这种情况下，将无法提供"安全"密码。建议为 JVM 安装 JCE 无限强度管辖权政策文件，以缓解此问题。

- [JCE 无限强度管辖权政策文件为 Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

如果在无法安装无限强度策略的系统上，建议切换到支持较长密码的算法（见上表）。

|      | 允许弱加密如果无法安装无限强度的管辖政策，设置可以更改为，但***不\*建议**这样做。更改此设置明确承认使用弱加密配置的固有风险。`Allow Weak Crypto``allowed` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

最好要求上游/下游系统切换到[键](https://cwiki.apache.org/confluence/display/NIFI/Encryption+Information)加密或使用 NiFi 支持的"强"[密钥衍生功能 （KDF）。](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#key-derivation-functions)

## 流量中的加密密码

NiFi 始终以加密格式存储所有以磁盘形式填充的敏感值（密码、令牌和其他凭据）。使用的加密算法由*nifi.属性*指定，加密密钥的源自密码由 nifi.属性指定（有关其他信息，请参阅[安全配置](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#security_configuration)）。在版本 1.12.0 之前，可用算法列表是该版本中由该版本中的 enum 支持的所有基于密码的加密 （PBE） 算法。不幸的是，其中许多算法都为旧的兼容性提供了条件，并使用弱键派生功能和阻止密码算法和操作模式。在 1.12.0 中，为注重安全的用户引入了一对自定义算法，以寻求对流量敏感值的更有力的保护。`nifi.sensitive.props.algorithm``nifi.sensitive.props.key``EncryptionMethod`

NiFi 支持多个配置选项，使用 AES 加卢瓦/计数器模式 （AES-GCM） 提供相关数据 （AEAD） 的认证加密。这些算法使用强大的键派生函数，根据配置的敏感属性键来提取指定长度的秘密密钥。每个键推导函数使用静态盐，以支持跨聚类节点的流量配置比较。每个关键推导函数还使用相关安全哈希实施类中定义的默认迭代和成本参数。

以下强加密方法可在属性中配置：`nifi.sensitive.props.algorithm`

- `NIFI_ARGON2_AES_GCM_128`
- `NIFI_ARGON2_AES_GCM_256`
- `NIFI_BCRYPT_AES_GCM_128`
- `NIFI_BCRYPT_AES_GCM_256`
- `NIFI_PBKDF2_AES_GCM_128`
- `NIFI_PBKDF2_AES_GCM_256`
- `NIFI_SCRYPT_AES_GCM_128`
- `NIFI_SCRYPT_AES_GCM_256`

每个关键推导函数使用以下默认参数：

- 阿贡2
  - 迭代： 5
  - 内存： 65536 KB
  - 并行性： 8
- 布里普特
  - 费用： 12
  - 衍生密钥文摘算法：SHA-512
- PBKDF2
  - 迭代： 160，000
  - 伪多功能系列：SHA-512
- 克里普特
  - 成本因素 （N）： 16384
  - 块大小因子 （r）： 8
  - 并行因子 （p）： 1

所有选项都需要**至少 12 个字符**的密码（值）。这意味着"默认"值（如果留空，则使用硬编码默认值）将是不够的。`nifi.sensitive.props.key`

## 配置文件中的加密密码

为了方便 NiFi 的安全设置，您可以使用命令线实用程序加密 NiFi 在启动时解密内存中的原始配置值。这种可扩展的保护方案透明地允许 NiFi 在操作中使用原始值，同时在休息时保护原始值。除了默认的 AES 加密提供商外，也可以在文件中配置哈希公司 Vault 加密提供商。`encrypt-config``bootstrap-hashicorp-vault.properties`

这是行为的改变：在 1.0 之前，所有配置值都存储在文件系统上的便文中。建议 POSIX 文件权限限制对这些文件的未经授权的访问。

如果不采取管理员操作，配置值仍不加密。

有关更多信息，请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)中的[加密配置](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#encrypt_config_tool)工具部分。

## NIFI工具包管理工具

此外，NiFi 工具包还包含用于管理员在独立和集群环境中支持 NiFi 维护的指挥线实用程序。这些实用程序包括：`tls-toolkit``encrypt-config`

- CLI - 该工具使管理员能够与 NiFi 和 NiFi 注册表实例进行交互，以自动执行部署版本流和管理流程组和集群节点等任务。`cli`
- 文件管理器 - 该工具使管理员能够从备份中备份、安装或恢复 NiFi 安装。`file-manager`
- 流分析器 - 该工具生成一个报告，帮助管理员了解可用于给定流量的背压存储的最大数据量。`flow-analyzer`
- 节点管理器 - 该工具使管理员能够对节点进行状态检查，以及从组集连接、断开或删除节点的能力。`node-manager`
- 通知 - 该工具使管理员能够向 NiFi UI 发送公告。`notify`
- S2S - 该工具使管理员能够将数据发送到或从 NiFi 流经站点到站点。`s2s`

有关每个实用程序的更多信息，请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)。

## 聚类配置

本节提供了 NiFi 聚类的快速概述以及如何设置基本聚类的说明。将来，我们希望提供深入涵盖 NiFi 聚类架构的补充文档。

![NiFi Cluster HTTP Access](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335916.png)

### 零领导聚类

NiFi 采用零领导聚类范式。集群中的每个节点具有相同的流，并在数据上执行相同的任务，但每个节点都基于不同的数据集工作。集群自动将数据分布到所有活动节点。

其中一个节点自动选择（通过阿帕奇ZooKeeper）作为集群协调员。然后，组中的所有节点都将向此节点发送心跳/状态信息，此节点负责断开在一段时间内不报告任何心跳状态的节点。此外，当新节点选择加入集群时，新节点必须首先连接到当前选出的集群协调员，以便获得最新的流量。如果集合协调员确定允许节点连接（基于其配置的防火墙文件），则向该节点提供当前流量，并且该节点能够加入该节点，前提是节点的流副本与集合协调员提供的副本相匹配。如果节点的流配置版本与集束协调员的版本不同，则节点将不会加入组集。

### 为什么是集群？

NiFi 管理员或数据流管理器 （DFMs） 可能会发现，在单台服务器上使用 NiFi 的一个实例不足以处理他们拥有的数据量。因此，一个解决方案是在多个 NiFi 服务器上运行相同的数据流。但是，这会产生管理问题，因为每次 DFM 想要更改或更新数据流时，它们必须在每个服务器上进行这些更改，然后单独监控每个服务器。通过聚类 NiFi 服务器，可以增加处理能力，同时拥有单个接口，通过该接口进行数据流更改和监控数据流。聚类允许 DFM 仅进行一次更改，然后将更改复制到组集的所有节点。通过单个接口，DFM 还可以监控所有节点的健康状况和状态。

### 术语

NiFi 聚类是独一无二的，并有自己的术语。在设置集群之前，了解以下术语非常重要：

**NiFi 群集协调员**：NiFi 聚类协调员是 NiFi 聚类中的节点，负责执行任务，以管理组中允许哪些节点，并为新加入的节点提供最新的流量。当数据流管理器管理组中的数据流时，他们能够通过组集中任何节点的用户界面进行管理。然后，将所做的任何更改复制到组中的所有节点。

**节点**：每个星团由一个或多个节点组成。节点进行实际数据处理。

**主节点**：每个组都有一个主节点。在此节点上，可以运行"隔离处理器"（见下文）。ZooKeeper用于自动选择主节点。如果该节点因任何原因与组断开，则将自动选择新的主节点。用户可以通过查看用户界面的群集管理页面来确定当前选择哪个节点为主要节点。

![Primary Node in Cluster Management UI](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335657.png)

**隔离处理器**：在 NiFi 聚类中，所有节点上都运行相同的数据流。因此，流中的每个组件都运行在每个节点上。但是，在某些情况下，DFM 不希望每个处理器在每个节点上运行。最常见的情况是使用处理器使用规模不好的协议与外部服务进行通信时。例如，GetSFTP 处理器从远程目录中取出。如果 GetSFTP 处理器在集群的每个节点上运行，并尝试同时从同一个远程目录中拉出，则可能会有比赛条件。因此，DFM 可以在主节点上配置 GetSFTP 以隔离运行，这意味着它仅在该节点上运行。有了适当的数据流配置，它可以在组集的其他节点中拉入数据并加载平衡数据。请注意，虽然此功能存在，但使用独立的 NiFi 实例来拉取数据并将其馈送至集群也很常见。这仅取决于可用资源以及管理员如何决定配置集群。

**心跳**：节点通过"心跳"向当前选出的集群协调员传达其健康状况和状态，让协调员知道他们仍然连接到集群并正常工作。默认情况下，节点每 5 秒发出一次心跳，如果群集协调员在 40 秒内（+ 5 秒 = 8）内未收到节点的心跳，则会因"心跳不足"而断开节点。5 秒和 8 倍设置可在*nifi.属性*文件中进行配置（有关更多信息，请参阅[聚类常见属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#cluster_common_properties)部分）。群集协调员断开节点的原因是协调员需要确保组中的每个节点是同步的，如果没有定期听到节点的声音，协调员无法确定它仍然与组集的其他节点同步。如果节点在 40 秒后发送新的心跳，协调员将自动请求节点重新加入组集，以包括节点流量的重新验证。由于心跳不足而断开和收到心跳后重新连接均报告给用户界面中的 DFM。

### 集群内的通信

如前所述，节点通过心跳与集群协调员通信。当选择集群协调员时，它会更新阿帕奇动物园守护者中著名的 ZNode 及其连接信息，以便节点了解将心跳发送到哪里。如果其中一个节点向下，组组中的其他节点不会自动拾取缺失节点的负载。DFM 可以配置故障转移意外事件的数据流;但是，这取决于数据流设计，并且不会自动发生。

当 DFM 对数据流进行更改时，收到更改流量请求的节点将这些更改传达到所有节点，并等待每个节点响应，表明它已对其本地流量进行了更改。

### 管理节点

#### 断开节点

DFM 可能会手动断开与组集集的节点。节点也可能因为其他原因而断开连接，例如由于心跳不足。当节点断开时，群集协调员将在用户界面上显示公告。在断开的节点问题解决之前，DFM 将无法对数据流进行任何更改。DFM 或管理员需要用节点解决问题，并在对数据流进行任何新更改之前解决它。但是，值得注意的是，仅仅因为节点断开并不意味着它不工作。这种情况的发生可能有几个原因，例如，当节点因网络问题而无法与群集协调员通信时。

要手动断开节点，请选择"断开"图标 （![Disconnect Icon](http://nifi.apache.org/docs/nifi-docs/html/images/iconDisconnect.png)） 从节点的行。

![Disconnected Node in Cluster Management UI](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335787.png)

可连接断开的节点 （![Connect Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335192.png)）， 卸载 （![Offload Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335233.png)） 或已删除 （![Delete Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335619.png)).

|      | 并非所有处于"断开"状态的节点都可以卸载。如果节点断开且无法访问，则节点无法接收卸载请求以开始卸载。此外，由于防火墙规则，卸载可能会中断或阻止。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

#### 卸载节点

保留在断开的节点上的流文件可以通过卸载重新平衡到组中的其他活动节点。在群集管理对话中，选择"卸载"图标 （![Offload Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335268.png)）用于断开的节点。这将停止所有处理器，终止所有处理器，停止在所有远程处理组上传输，并重新平衡流文件到集群中其他连接的节点。

![Offloading Node in Cluster Management UI](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335942.png)

由于遇到错误（内存外、没有网络连接等）而保持"卸载"状态的节点可以通过在节点上重新启动 NiFi 重新连接到组。卸载节点可以重新连接到组集（通过选择连接或在节点上重新启动 NiFi）或从组集中删除。

![Offloaded Node in Cluster Management UI](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335578.png)

#### 删除节点

在某些情况下，DFM 可能希望继续更改流量，即使节点未与聚类连接。在这种情况下，DFM 可能会选择从组组中完全删除节点。在群集管理对话中，选择"删除"图标 （![Delete Icon](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335438.png)）用于已断开或卸载的节点。删除后，节点在重新启动之前无法重新加入到组集。

#### 退役节点

将节点退役并将其从聚类中删除的步骤如下：

1. 断开节点。
2. 断开完成后，卸载节点。
3. 卸载完成后，删除节点。
4. 删除请求完成后，停止/删除主机上的 NiFi 服务。

#### NIFI CLI 节点命令

作为 UI 的替代方案，以下 NiFi CLI 命令可用于检索单个节点、检索节点列表以及连接/断开/卸载/删除节点：

- `nifi get-node`
- `nifi get-nodes`
- `nifi connect-node`
- `nifi disconnect-node`
- `nifi offload-node`
- `nifi delete-node`

有关更多信息，请参阅 NiFi[工具包指南中的 NiFi](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html) [CLI](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#nifi_CLI)部分。

### 流动选举

当聚类首次启动时，NiFi 必须确定哪个节点具有"正确"版本的流。这是通过对每个节点的流量进行投票来完成的。当节点尝试连接到聚类时，它会向群集协调员提供其本地流量的副本，以及（如果策略提供商允许通过 NiFi 进行配置）其用户、组和策略。如果尚未选择"正确"流，则节点的流与其他节点的流量进行比较。如果另一个节点的流与此流匹配，则为此流投下一票。如果还没有其他节点报告相同的流量，则此流将以一票之多添加到可能当选的流量池中。经过一段时间（通过设置属性进行配置）或一些节点投票（通过设置属性进行配置）后，流被选为流的"正确"副本。`nifi.cluster.flow.election.max.wait.time``nifi.cluster.flow.election.max.candidates`

任何数据流、用户、组和策略与当选者发生冲突的节点都将备份任何相互冲突的资源，并将本地资源替换为聚类资源。备份的执行方式取决于配置的访问策略提供商和用户组提供商。对于基于文件的访问策略提供商，备份将写入与现有文件相同的目录（例如，$NIFI_HOME/conf），并带有相同的名称，但带有""的后缀和时间戳。例如，如果流本身在 2020 年 1 月 1 日 12：05：03 与聚类流冲突，则节点的文件将被复制到该组，然后将组集合的流量写入。同样，这将发生在文件和文件。这样做是为了在必要时将备份文件重命名为"例如"手动恢复流量。`flow.xml.gz``flow.xml.gz.2020-01-01-12-05-03``flow.xml.gz``users.xml``authorizations.xml``flow.xml.gz`

请务必注意，在继承所选流量之前，NiFi 将首先阅读 FlowFile 存储库和任何交换文件，以确定数据流中的哪些队列当前包含数据。如果数据流中存在包含 FlowFile 的任何队列，则该队列也必须存在于选定的数据流中。如果该队列在选选出的数据流中不存在，则节点将不会继承数据流、用户、组和策略。相反，NiFi 将记录错误，并且无法启动。这可确保即使节点中存储的数据与集群的数据流不同，重新启动节点也不会导致数据丢失。

选举是按照"民众投票"进行的，并警告说，除非所有选举都是空的，否则获胜者永远不会是"空流"。这允许管理员删除节点的*流.xml.gz*文件并重新启动节点，因为知道除非没有发现其他流，否则节点的流量不会被投票选为"正确"流。如果有两个非空流获得相同票数，则将选择其中一个流。用于确定这些流量中哪些流量的方法尚未确定，并且可能随时在不通知的情况下更改。

### 基本集群设置

本节描述了由三个 NiFi 实例组成的简单三节点非安全集群的设置。

对于每个实例，需要更新*nifi.属性*文件中的某些属性。特别是，应根据您的情况评估 Web 和聚类属性，并相应地进行调整。本指南的[系统属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#system_properties)部分描述了所有属性;但是，在本节中，我们将关注为简单聚类设置的最低属性。

对于所有三种实例，[聚类常见属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#cluster_common_properties)可以留给默认设置。但是，请注意，如果您更改了这些设置，则必须在组集的每个实例上设置相同的设置。

对于每个节点，要配置的最小属性如下：

- 在*Web 属性*部分下，设置您希望节点运行的 HTTP 或 HTTPS 端口。此外，考虑您是否需要设置 HTTP 或 HTTPS 主机属性。组组中的所有节点应使用相同的协议设置。
- 根据*国家管理部分*，将财产设置为聚类状态提供商的标识符。确保集群状态提供商已配置在*状态管理.xml*文件中。有关更多信息，请参阅[配置状态提供商](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#state_providers)。`nifi.state.management.provider.cluster`
- 在*集群节点属性*下，设置如下：
  - `nifi.cluster.is.node`- 将此设置为*真实*。
  - `nifi.cluster.node.address`- 将此设置为节点的完全合格主机名。如果留空，则默认为 。`localhost`
  - `nifi.cluster.node.protocol.port`- 将此设置为高于 1024 的开放端口（任何较低的端口都需要根）。
  - `nifi.cluster.node.protocol.threads`- 应用于与组中其他节点通信的线程数。此属性默认为 。线程池用于复制所有节点的请求，线程池的线程永远不会少于此数量的线程。它将根据需要增长到属性设定的最大值。`10``nifi.cluster.node.protocol.max.threads`
  - `nifi.cluster.node.protocol.max.threads`- 应用于与组中其他节点通信的最大线程数。此属性默认为 。螺纹池用于对所有节点的复制请求，螺纹池将有一个由属性配置的"核心"大小。但是，如有必要，螺纹池将增加活动线程的数量，达到此属性设定的限制。`50``nifi.cluster.node.protocol.threads`
  - `nifi.zookeeper.connect.string`- 连接字符串，这是需要连接到阿帕奇ZooKeeper。这是一个逗号分离的主机名列表：端口对。例如。这应该包含ZooKeeper法定人数中所有ZooKeeper实例的列表。`localhost:2181,localhost:2182,localhost:2183`
  - `nifi.zookeeper.root.node`- 应该在ZooKeeper中使用的根 Znode 。ZooKeeper为存储数据提供了类似目录的结构。此结构中的每个"目录"都称为 ZNode。这表示应用于存储数据的根 ZNode 或"目录"。默认值是 。这对于正确设置非常重要，因为 NiFi 实例尝试加入的组由它连接到哪个ZooKeeper实例和指定的ZooKeeper根节点决定。`/root`
  - `nifi.cluster.flow.election.max.wait.time`- 指定在选择流为"正确"流之前等待的时间。如果已投票的节点数等于属性指定的数数，则聚类不会等待这么久。默认值是 。请注意，第一次投票一开始。`nifi.cluster.flow.election.max.candidates``5 mins`
  - `nifi.cluster.flow.election.max.candidates`- 指定组中导致提前选举流量所需的节点数。这样，如果我们至少达到组集中的节点数量，则组中的节点可以避免在开始处理之前等待很长时间。

现在，可以启动集群。命令实例启动并不重要。导航到其中一个节点的 URL，用户界面应与以下内容类似：

![Clustered User Interface](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335013.png)

### 故障 排除

如果您遇到问题，并且您的集群没有按描述工作，请调查节点上的*nifi 应用程序.log*和*nifi 用户.log*文件。如果需要，您可以通过编辑文件将记录级别更改为 DEBUG。具体来说，设置在以下行（而不是 ）：`conf/logback.xml``level="DEBUG"``"INFO"`

```
    <logger name="org.apache.nifi.web.api.config" level="INFO" additivity="false">        <appender-ref ref="USER_FILE"/>    </logger>
```

## 国家管理

NiFi 为处理器、报告任务、控制器服务以及持续状态的框架本身提供了一个机制。例如，这允许处理器从 NiFi 重新启动后关闭的地方恢复。此外，它还允许处理器存储某些信息，以便处理器可以从组集中的所有不同节点访问该信息。这允许一个节点从另一个节点离开的位置拾取，或在聚类中的所有节点之间进行协调。

### 配置国家提供商

当组件决定存储或检索状态时，它通过提供"范围" （ 节点本地或集群范围） 来存储或检索状态。然后，根据此范围以及配置的国家提供商确定用于存储和检索此状态的机制。*nifi.属性*文件包含与配置这些状态提供商相关的三种不同的属性。

| **财产**                                   | **描述**                                                     |
| ------------------------------------------ | ------------------------------------------------------------ |
| `nifi.state.management.configuration.file` | 首先是指定用于配置本地和/或集群范围的国家提供商的外部 XML 文件的属性。此 XML 文件可能包含多个提供商的配置 |
| `nifi.state.management.provider.local`     | 提供本 XML 文件中配置的当地国家提供商标识符的属性            |
| `nifi.state.management.provider.cluster`   | 同样，该属性提供此 XML 文件中配置的集群范围状态提供商的标识符。 |

此 XML 文件由顶级元素组成，该元件具有一个或多个元素以及零或多个元素。然后，每个元素都包含一个元素，用于指定*nifi.properties*文件中可以引用的标识符，以及指定用于给国家提供商提供说明的完全合格的类名称的元素。最后，每个元素可能都具有零或更多元素。每个元素都有一个属性，即国家提供者支持的名称。属性元素的文本内容是属性的价值。`state-management``local-provider``cluster-provider``id``class``property``property``name``property`

一旦这些国家提供者在*国家管理.xml*文件（或任何配置的文件）中配置了这些提供商，则这些提供商的标识符可以引用这些提供商。

默认情况下，地方国家提供者被配置为将数据粘在目录中。默认的集群状态提供商被配置为 。默认的基于ZooKeeper的提供商在使用之前必须填充其属性。如果多个 NiFi 实例将使用相同的ZooKeeper实例，也建议更改属性的价值。例如，人们可能会将值设置为 。A采取逗号分离的形式<托管>：<港>等。如果任何主机未指定端口，假设ZooKeeper默认。`WriteAheadLocalStateProvider``$NIFI_HOME/state/local``ZooKeeperStateProvider``Connect String``Root Node``/nifi/<team name>/production``Connect String``my-zk-server1:2181,my-zk-server2:2181,my-zk-server3:2181``2181`

在向ZooKeeper添加数据时，访问控制有两个选项：和 。如果该属性被设置为，那么任何人都可以登录 ZooKeeper，并拥有查看、更改、删除或管理数据的完整权限。如果指定，则只允许创建数据的用户读取、更改、删除或管理数据。为了使用该选项，NiFi 必须提供某种形式的身份验证。有关如何配置身份验证的更多信息，请参阅下面的[ZooKeeper访问控制](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#zk_access_control)部分。`Open``CreatorOnly``Access Control``Open``CreatorOnly``CreatorOnly`

如果 NiFi 被配置为以独立模式运行，则该元素无需在*国家管理.xml*文件中填充，如果填充，则实际上将予以忽略。但是，该元素必须始终存在并填充。此外，如果 NiFi 在群集中运行，则每个节点还必须具有当前和正确配置的元素。否则，NiFi 将无法启动。`cluster-provider``local-provider``cluster-provider`

虽然这些提供商需要配置的属性并不多，但它们被外部化为单独*的国家管理.xml*文件，而不是通过*nifi.属性*文件进行配置，仅仅是因为不同的实现可能需要不同的属性，并且比将提供商的属性与所有其他 NiFi 框架特定的道具混合在一起要容易得多瑞斯

应当指出，如果处理器和其他组件使用分组范围保存状态，则如果该实例是独立实例（不在组集中）或与组集断开，则将使用本地状态提供程序。这也意味着，如果一个独立实例迁移成为集群，那么该状态将不再可用，因为该组件将开始使用聚类状态提供商而不是本地状态提供商。

### 嵌入式ZooKeeper服务器

如上所述，全聚类状态的默认状态提供商是 。在本文编写本报告时，这是唯一存在用于处理全集群状态的国家提供商。这意味着 NiFi 依赖ZooKeeper来充当集群。然而，有许多环境，其中NiFi部署的地方没有现有的ZooKeeper合奏被维护。为了避免迫使管理员也维护单独的ZooKeeper实例的负担，NiFi 提供了启动嵌入式ZooKeeper服务器的选项。`ZooKeeperStateProvider`

| **财产**                                              | **描述**                                                     |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.state.management.embedded.zookeeper.start`      | 具体说明 NiFi 的此实例是否应运行嵌入式ZooKeeper服务器        |
| `nifi.state.management.embedded.zookeeper.properties` | 属性文件，提供ZooKeeper属性使用，如果设置为`nifi.state.management.embedded.zookeeper.start``true` |

这可以通过将*nifi.属性*设置为应运行嵌入式 ZooKeeper 服务器的节点来实现。一般来说，建议在 3 或 5 个节点上运行ZooKeeper。在少于 3 个节点上运行，在失败时提供更少的耐用性。在多个 5 个节点上运行通常产生的网络流量比必要的要多。此外，在 4 个节点上运行ZooKeeper不会比在 3 个节点上运行更有益，ZooKeeper 需要大多数节点是主动的才能工作。但是，由管理员决定最适合 NiFi 特定部署的节点数量。`nifi.state.management.embedded.zookeeper.start``true`

如果该属性设置为*，nifi. 属性中的属性*也变得相关。这指定了ZooKeeper属性文件使用。至少，此属性文件需要填充 Zoo 守护者服务器列表。服务器被指定为属性的形式，以，到。截至 NiFi 1.10.x，ZooKeeper已升级到 3.5.5，服务器现在定义与客户端口附加在年底根据[ZooKeeper文档](https://zookeeper.apache.org/doc/r3.5.2-alpha/zookeeperReconfig.html#sc_reconfig_clientport)。因此，这些服务器中的每一个都被配置为<主机名>：<quorum端口>[<领导人选举端口>][角色]：[<客户端口地址>：]<客户端口>。作为一个简单的例子，这将是。此节点列表应是 NiFi 聚类中的相同节点，该节点的属性设置为 。还要注意，由于 ZooKeeper 将监听这些端口，因此可能需要配置防火墙来打开这些端口以进行传入流量，至少在集群中的节点之间。`nifi.state.management.embedded.zookeeper.start``true``nifi.state.management.embedded.zookeeper.properties``server.1``server.2``server.n``server.1 = myhost:2888:3888;2181``nifi.state.management.embedded.zookeeper.start``true`

当使用嵌入式ZooKeeper时，。/*conf/ZooKeeper.属性*文件有一个属性命名。默认情况下，此值设置为 。如果不止一个 NiFi 节点运行嵌入式ZooKeeper，则必须告诉服务器它是哪个。这是通过创建一个名为*myid*的文件并将其放入ZooKeeper的数据目录来实现的。此文件的内容应是服务器的索引，具体由 。因此，对于动物园守护者服务器之一，我们将通过执行以下命令来实现此目的：`dataDir``./state/zookeeper``server.<number>`

```
cd $NIFI_HOMEmkdir statemkdir state/zookeeperecho 1 > state/zookeeper/myid
```

对于下一个运行动物园守护者的 NiFi 节点，我们可以通过执行以下命令来实现此目的：

```
cd $NIFI_HOMEmkdir statemkdir state/zookeeperecho 2 > state/zookeeper/myid
```

等等。

有关用于管理ZooKeeper的属性的更多信息，请参阅[ZooKeeper管理指南](https://zookeeper.apache.org/doc/current/zookeeperAdmin.html)。

有关保护嵌入式动物园守护者服务器的信息，请参阅下面[的 Kerberos 部分的"保护ZooKeeper](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#securing_zookeeper)"。

### ZooKeeper访问控制

ZooKeeper通过访问控制列表 （ACL） 机制对其数据提供访问控制。当数据被写给 ZooKeeper 时，NiFi 将提供 ACL，表示允许任何用户对数据拥有完全权限，或者 ACL 表示只允许创建数据的用户访问数据。使用哪个 ACL 取决于属性的价值（有关更多信息，请参阅[配置状态提供商](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#state_providers)部分）。`Access Control``ZooKeeperStateProvider`

为了使用 ACL 表示只有创建者才能访问数据，我们需要告诉ZooKeeper谁是造物主。实现这一目标有三种机制。第一个机制是使用 Kerberos 提供身份验证。有关更多信息，请参阅[Kerbers 在NIFI的ZooKeeper客户端](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#zk_kerberos_client)。

第二个选项，即确保网络通信被加密，是使用支持 TLS 的 ZooKeeper 服务器上的 X.509 证书进行身份验证。有关更多信息，请参阅[TLS 保护ZooKeeper](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#zk_tls_client)。

第三个选项是使用用户名和密码。此配置通过指定属性的值和属性的价值（有关更多信息，请参阅[配置状态提供商](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#state_providers)部分）进行配置。不过，这里要记住的一点是，ZooKeeper会以纯文本传递密码。这意味着，除非 ZooKeeper 以一个实例集群的身份在本地主机上运行，或者与 ZooKeeper 的通信仅通过加密通信（如 VPN 或 SSL 连接）进行，否则不应使用用户名和密码。`Username``Password``ZooKeeperStateProvider`

### 保护ZooKeeper与克贝罗斯

当 NiFi 与ZooKeeper通信时，默认情况下，所有通信都是不安全的，任何登录ZooKeeper的人都能够查看和操作存储在ZooKeeper中的所有 NiFi 状态。为了防止这种情况，一个选项是使用 Kerberos 来管理身份验证。

为了确保与 Kerberos 的通信安全，我们需要确保客户端和服务器都支持相同的配置。下面提供了配置 NiFi ZooKeeper客户端和嵌入式ZooKeeper服务器以使用 Kerberos 的说明。

如果 Kerberos 尚未在您的环境中设置，您可以在红帽客户门户处查找有关安装和设置 Kerberos 服务器的信息[：配置 Kerberos 5 服务器](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/Configuring_a_Kerberos_5_Server.html)。此指南假定 Kerberos 已安装在 NiFi 运行的环境中。

请注意，在 NiFi 节点中对嵌入式ZooKeeper服务器进行缩放和将ZooKeeper NiFi 客户端进行缩放的以下程序将要求安装 Kerberos 客户端库。这是通过：

```
yum install krb5-workstation
```

完成此工作后*，/etc/krb5.conf*将需要针对您组织的 Kerberos 环境进行适当配置。

#### 克贝里化嵌入式ZooKeeper服务器

系统上的*krb5.conf*文件与嵌入式ZooKeeper服务器应与 krb5kdc 服务运行系统上的文件相同。使用嵌入式动物园守护者服务器时，我们可以选择使用 Kerberos 来保护服务器的安全。所有节点配置为启动嵌入式ZooKeeper和使用 Kerberos 应遵循这些步骤。使用嵌入式动物园守护者服务器时，我们可以选择使用 Kerberos 来保护服务器的安全。所有节点配置为启动嵌入式ZooKeeper和使用 Kerberos 应遵循这些步骤。

为了使用 Kerberos，我们首先需要为我们的ZooKeeper服务器生成一个 Kerberos 校长。以下命令在 krb5kdc 服务运行的服务器上运行。这是通过卡德明工具完成的：

```
kadmin: addprinc "zookeeper/myHost.example.com@EXAMPLE.COM"
```

在这里，我们正在创建一个校长与主要，使用领域。我们需要使用一个名字是校长。在这种情况下，服务是和实例名称是（我们主机的完全合格名称）。`zookeeper/myHost.example.com``EXAMPLE.COM``<service name>/<instance name>``zookeeper``myHost.example.com`

接下来，我们需要为此本委托人创建一个 KeyTab，此命令在服务器上运行，带有嵌入式ZooKeeper服务器的 NiFi 实例：

```
kadmin: xst -k zookeeper-server.keytab zookeeper/myHost.example.com@EXAMPLE.COM
```

这将创建当前目录中指定的文件。我们现在可以将该文件复制到目录中。我们应该确保只有运行 NiFi 的用户才能阅读此文件。`zookeeper-server.keytab``$NIFI_HOME/conf/`

我们需要重复上述步骤的NiFi的每一个实例，将运行嵌入式动物园守护者服务器，一定要替换，或任何完全合格的主机名动物园守护者服务器将运行。`myHost.example.com``myHost2.example.com`

现在，我们有我们的 KeyTab 为每一个服务器，将运行 NiFi， 我们将需要配置 NiFi 的嵌入式动物园守护者服务器来使用此配置.ZooKeeper使用 Java 认证和授权服务 （JAAS），因此我们需要创建一个 JAAS 兼容的文件在目录中，创建一个名为*ZooKeeper-jaas.conf*的文件（如果客户端已经配置为通过 Kerberos 进行身份验证，此文件将已经存在。没关系，只需添加到文件中）。我们将添加到此文件，以下片段：`$NIFI_HOME/conf/`

```
Server {  com.sun.security.auth.module.Krb5LoginModule required  useKeyTab=true  keyTab="./conf/zookeeper-server.keytab"  storeKey=true  useTicketCache=false  principal="zookeeper/myHost.example.com@EXAMPLE.COM";};
```

请务必用相应的本金（包括服务器的完全合格域名）替换上述值。`principal`

接下来，我们需要告诉 NiFi 将此用作我们的 JAAS 配置。这是通过设置一个JVM系统属性完成的，所以我们将编辑*会议/引导.conf*文件。如果客户端已被配置为使用 Kerberos，则没有必要使用，就像上面所做的那样。否则，我们将在*引导文件*中添加以下行：

```
java.arg.15=-Djava.security.auth.login.config=./conf/zookeeper-jaas.conf
```

|      | 文件中的此附加行不必是 15 号，只需添加到*bootstrap.conf*文件中。使用适合配置的任何号码。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

我们将希望通过运行以下命令来初始化我们的 Kerberos 机票：

```
kinit –kt zookeeper-server.keytab "zookeeper/myHost.example.com@EXAMPLE.COM"
```

同样，请务必以适当的价值替换本金，包括您的领域和您完全合格的主机名。

最后，我们需要告诉 Kerberos 服务器使用 SASL 身份验证提供商。为此，我们编辑*$NIFI_HOME/conf/zookeeper.属性*文件，并添加以下行：

```
authProvider.1=org.apache.zookeeper.server.auth.SASLAuthenticationProviderkerberos.removeHostFromPrincipal=truekerberos.removeRealmFromPrincipal=truejaasLoginRenew=3600000requireClientAuthScheme=sasl
```

在将标识与 Znode 上应用的 acls 进行比较之前，该属性和属性用于使用户主名正常化。默认情况下，使用完整的本金，但设置和属性的真实将指示ZooKeeper从登录用户的身份中删除主机和领域进行比较。如果 NiFi 节点（在同一集群内）使用具有不同主机/领域值的本金，可以配置这些 kerberos 属性，以确保节点的身份正常化，并且节点将适当访问ZooKeeper共享的 Znodes。`kerberos.removeHostFromPrincipal``kerberos.removeRealmFromPrincipal``kerberos.removeHostFromPrincipal``kerberos.removeRealmFromPrincipal`

最后一行是可选的，但规定客户必须使用 Kerberos 与我们的ZooKeeper实例进行通信。

现在，我们可以启动 NiFi，嵌入式ZooKeeper服务器将使用 Kerberos 作为身份验证机制。

#### 克贝里宁NIFI的ZooKeeper客户

|      | 运行嵌入式ZooKeeper服务器的 NiFi 节点也需要遵循以下程序，因为它们也将同时充当客户端。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

使用ZooKeeper验证用户的首选机制是使用 Kerberos。为了使用 Kerberos 进行身份验证，我们必须配置一些系统属性，以便ZooKeeper客户端知道用户是谁以及 KeyTab 文件的位置。所有配置为存储使用和使用 Kerberos 的集群状态的节点应遵循这些步骤。`ZooKeeperStateProvider`

首先，我们必须创建在与ZooKeeper沟通时使用的本金。这通常通过工具完成：`kadmin`

```
kadmin: addprinc "nifi@EXAMPLE.COM"
```

克贝罗斯校长由三个部分组成：主要部分、实例和领域。在这里，我们正在创建一个校长与主要，没有实例，和领域。主要（在此例中）是通过 Kerberos 进行身份验证时用于识别用户的标识符。`nifi``EXAMPLE.COM``nifi`

创建本金后，我们需要为校长创建一个 KeyTab：

```
kadmin: xst -k nifi.keytab nifi@EXAMPLE.COM
```

此键盘文件可以复制到其他带有嵌入式ZooKeeper服务器的 NiFi 节点。

这将创建一个名为*nifi.keytab*的当前目录中的文件。我们现在可以将该文件复制到目录中。我们应该确保只有运行 NiFi 的用户才能阅读此文件。`$NIFI_HOME/conf/`

接下来，我们需要配置 NiFi 来使用此 KeyTab 进行身份验证。由于ZooKeeper使用 Java 认证和授权服务 （JAAS），我们需要创建一个 JAAS 兼容的文件。在目录中，创建一个名为*ZooKeeper-jaas.conf*的文件，并添加到它下面的片段：`$NIFI_HOME/conf/`

```
Client {  com.sun.security.auth.module.Krb5LoginModule required  useKeyTab=true  keyTab="./conf/nifi.keytab"  storeKey=true  useTicketCache=false  principal="nifi@EXAMPLE.COM";};
```

然后，我们需要告诉 NiFi 将此用作我们的 JAAS 配置。这是通过设置一个JVM系统属性完成的，所以我们将编辑*会议/引导.conf*文件。我们在此文件的任意一个行中添加以下行，以便告诉 NiFi JVM 使用此配置：

```
java.arg.15=-Djava.security.auth.login.config=./conf/zookeeper-jaas.conf
```

最后，我们需要更新*nifi.属性*，以确保 NiFi 知道应用 SASL 特定的 ACL 为 Znodes，它将创建在ZooKeeper集群管理。为了实现此操作，*请在$NIFI_HOME/conf/nifi.属性*文件中，并编辑下列属性如下所示：

```
nifi.zookeeper.auth.type=saslnifi.zookeeper.kerberos.removeHostFromPrincipal=truenifi.zookeeper.kerberos.removeRealmFromPrincipal=true
```

|      | 并且应该与ZooKeeper配置中设置的内容一致。`kerberos.removeHostFromPrincipal``kerberos.removeRealmFromPrincipal` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

我们可以通过运行以下命令来初始化我们的 Kerberos 门票：

```
kinit -kt nifi.keytab nifi@EXAMPLE.COM
```

现在，当我们开始 NiFi 时，它会使用 Kerberos 在与ZooKeeper通信时以用户身份进行身份验证。`nifi`

#### 故障排除克贝罗斯配置

使用 Kerberos 时，使用完全合格的域名而不是使用*本地托管*是进口的。请确保每个服务器的完全合格主机名在以下位置使用：

- *邦联/ZooKeeper.属性*文件应使用FQDN的，。。。`server.1``server.2``server.N`
- ZooKeeper的财产提供者`Connect String`
- */etc/主机*文件还应将 FQDN 解析为**未**在此的 IP 地址。`127.0.0.1`

如果不这样做，可能导致类似以下错误：

```
2016-01-08 16:08:57,888 ERROR [pool-26-thread-1-SendThread(localhost:2181)] o.a.zookeeper.client.ZooKeeperSaslClient An error: (java.security.PrivilegedActionException: javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Server not found in Kerberos database (7) - LOOKING_UP_SERVER)]) occurred when evaluating ZooKeeper Quorum Member's  received SASL token. ZooKeeper Client will go to AUTH_FAILED state.
```

如果与 Kerberos 沟通或验证存在问题，此[故障排除指南](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jgss/tutorials/Troubleshooting.html)可能具有价值。

以上故障排除指南中最重要的注释之一是打开 Kerberos 的调试输出的机制。这是通过设置环境变量来完成的。在 NiFi 中，通过在*$NIFI_HOME/conf/引导.conf*文件中添加以下行来实现此目的：`sun.security.krb5.debug`

```
java.arg.16=-Dsun.security.krb5.debug=true
```

这将导致调试输出被写入 NiFi 引导日志文件。默认情况下，这位于*$NIFI_HOME/日志/NIFI引导.log。*此输出可能相当冗长，但为排除 Kerberos 故障提供了极其有价值的信息。

### 用 TLS 保护ZooKeeper

如上所述，默认情况下，与ZooKeeper的沟通不安全。安全地对ZooKeeper进行身份验证并与ZooKeeper通信的第二个选项是使用支持 TLS 的ZooKeeper服务器（自ZooKeeper的 3.5.x 版本以来可用）使用基于证书的身份验证。在ZooKeeper指南中可以找到在外部ZooKeeper合奏上启用 TLS[的](https://zookeeper.apache.org/doc/r3.5.5/zookeeperAdmin.html#sc_authOptions)说明。

一旦你有一个TLS启用的ZooKeeper实例，TLS可以通过设置启用为NiFi客户端。默认情况下，ZooKeeper客户将使用钥匙店和信托商店的现有属性。如果您需要为 ZooKeeper 提供单独的 TLS 配置，您可以创建单独的钥匙店和信托商店，并在*$NIFI_HOME/conf/nifi.属性*文件中配置以下属性：`nifi.zookeeper.client.secure=true``nifi.security.*`

| 属性名称                                   | 描述                                                         | 违约   |
| :----------------------------------------- | :----------------------------------------------------------- | :----- |
| `nifi.zookeeper.security.truststorePasswd` | 信托商店的密码。                                             | *没有* |
| `nifi.zookeeper.client.secure`             | 是否使用客户 Tls 来协调ZooKeeper。                           | 假     |
| `nifi.zookeeper.security.keystore`         | 钥匙店的文件名，其中包含与ZooKeeper沟通时要使用的私人密钥。  | *没有* |
| `nifi.zookeeper.security.keystoreType`     | 自选。钥匙店的类型。必须是，或.如果没有指定类型将从文件扩展中确定（， ， ， ） 。`PKCS12``JKS``PEM``.p12``.jks``.pem` | *没有* |
| `nifi.zookeeper.security.keystorePasswd`   | 钥匙店的密码。                                               | *没有* |
| `nifi.zookeeper.security.truststore`       | 将用于验证动物园守护者服务器的信托商店的档案名。             | *没有* |
| `nifi.zookeeper.security.truststoreType`   | 自选。信托商店的类型。必须是，或.如果没有指定类型将从文件扩展中确定（， ， ， ） 。`PKCS12``JKS``PEM``.p12``.jks``.pem` | *没有* |

无论是使用默认安全属性还是ZooKeeper特定属性，钥匙店和信托商店都必须包含适当的钥匙和证书，以便与ZooKeeper一起使用（即，无论哪种方式，钥匙和证书都需要与ZooKeeper配置保持一致）。NiFi 的 TLS 工具包可用于帮助生成用于ZooKeeper客户/服务器访问的关键商店和信托商店。

更新上述属性并启动 NiFi 后，与ZooKeeper的网络通信将是安全的，ZooKeeper现在将在验证访问时使用 NiFi 节点的证书本金。这将反映在日志消息中，如ZooKeeper服务器上的以下信息：

```
2020-02-24 23:37:52,671 [myid:2] - INFO  [nioEventLoopGroup-4-1:X509AuthenticationProvider@172] - Authenticated Id 'CN=nifi-node1,OU=NIFI' for Scheme 'x509'
```

ZooKeeper使用 Netty 支持网络加密和基于证书的身份验证。启用 TLS 后，必须配置 ZooKeeper 服务器及其客户端以使用基于 Netty 的连接，而不是默认的 NIO 实现。这是自动配置为NIFI时，设置为*真*。启用 Netty 后，您应该*在$NIFI_HOME/日志/nifi-app*中看到以下日志消息.log：`nifi.zookeeper.client.secure`

```
2020-02-24 23:37:54,082 INFO [nioEventLoopGroup-3-1] o.apache.zookeeper.ClientCnxnSocketNetty SSL handler added for channel: [id: 0xa831f9c3]2020-02-24 23:37:54,104 INFO [nioEventLoopGroup-3-1] o.apache.zookeeper.ClientCnxnSocketNetty channel is connected: [id: 0xa831f9c3, L:/172.17.0.4:56510 - R:8e38869cd1d1/172.17.0.3:2281]
```

### 嵌入式ZooKeeper与 TLS

NiFi 集群可以使用嵌入在 NiFi 本身中的ZooKeeper实例进行部署，所有节点都可以与该实例进行通信。截至 NiFi 1.13.0，节点和此嵌入式ZooKeeper之间的通信现在可以通过 TLS 进行保护。1.13 之前的 NiFi 版本没有使用嵌入式 ZooKeeper 的安全客户端访问。连接客户端的配置将与外部ZooKeeper的运行方式相同。即，默认情况下，它将使用 nifi.属性文件中的属性，除非您指定具有上述明示的 ZooKeeper 钥匙店/信托商店属性。`nifi.security.*``nifi.zookeeper.security.*`

服务器配置将以与不安全的嵌入式服务器相同的方式运行，但与集（通常是端口）一样。`secureClientPort``2281`

示例*$NIFI_家庭/邦联/ZooKeeper.属性*文件：

```
secureClientPort=2281initLimit=10autopurge.purgeInterval=24syncLimit=5tickTime=2000dataDir=./state/zookeeperautopurge.snapRetainCount=30server.1=nifi1.example.com:2888:3888server.2=nifi2.example.com:2888:3888server.3=nifi3.example.com:2888:3888
```

当使用三个节点 NiFi 集群时，上述配置文件将建立一个三个节点 ZooKeeper 法定人数，每个节点在安全端口 2281 上监听客户端端连接，2888 用于法定人数通信，3888 用于领导人选举。

|      | 在使用安全服务器时，安全嵌入的ZooKeeper服务器会忽略*$NIFI_HOME/conf/zookeeper.属性*中指定的任何客户端或端子端。即，如果 NiFi 嵌入式ZooKeeper暴露了安全的ClientPort，它不会暴露不安全的客户端，无论配置如何。这是嵌入式服务器和外部动物园守护者服务器之间的行为差异，确保嵌入式ZooKeeper要么安全运行，要么不安全地运行，但不是两者的混合体。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

以下是在*$NIFI_HOME/conf/nifi.属性*中设置的相关属性的示例，以运行并连接到此法定人数：

```
nifi.security.keystore=./conf/keystore.jksnifi.security.keystoreType=jksnifi.security.keystorePasswd=passwordnifi.security.keyPasswd=passwordnifi.security.truststore=./conf/truststore.jksnifi.security.truststoreType=jksnifi.security.truststorePasswd=passwordnifi.security.user.authorizer=managed-authorizernifi.zookeeper.connect.string=nifi1.example.com:2281,nifi2.example.com:2281,nifi3.example.com:2281nifi.zookeeper.connect.timeout=10 secsnifi.zookeeper.session.timeout=10 secsnifi.zookeeper.root.node=/nifinifi.zookeeper.client.secure=truenifi.state.management.embedded.zookeeper.start=truenifi.state.management.embedded.zookeeper.properties=./conf/zookeeper.propertiesnifi.state.management.configuration.file=./conf/state-management.xmlnifi.state.management.provider.cluster=zk-provider
```

### ZooKeeper迁移者

您可以使用该工具执行以下任务：`zk-migrator`

- 将ZooKeeper信息从一个ZooKeeper集群移到另一个
- 迁移ZooKeeper节点所有权

例如，您可能需要在您时使用ZooKeeper迁移器：

- 从 NiFi 0.x 升级到使用嵌入式ZooKeeper的 NiFi 1.x
- 从 NiFi 0.x 或 1.x 中的嵌入式ZooKeeper迁移到外部ZooKeeper
- 升级从 NiFi 0.x 与外部ZooKeeper到 NiFi 1.x 与相同的外部ZooKeeper
- 从外部ZooKeeper迁移到 NiFi 1.x 中的嵌入式ZooKeeper

有关更多信息，请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)中的[ZooKeeper迁移器](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#zookeeper_migrator)部分。

## 引导属性

目录中的*引导.conf*文件允许用户配置如何启动 NiFi 的设置。这包括参数，如 Java 堆的大小、Java命令运行的内容以及 Java 系统属性。`conf`

在这里，我们将解决文件中提供的不同属性。只有在 NiFi 停止并重新启动后，此文件的任何更改才会生效。

| **财产**                           | **描述**                                                     |
| ---------------------------------- | ------------------------------------------------------------ |
| `java`                             | 指定完全合格的 java 命令运行。默认情况下，它只是，但可以更改为绝对路径或参考环境变量，如`java``$JAVA_HOME/bin/java` |
| `run.as`                           | 运行 NiFi 的用户名。例如，如果 NiFi 应作为用户运行，则将此值设置为将导致 NiFi 过程以用户身份运行。此属性在 Windows 上被忽略。对于 Linux，指定的用户可能需要数独权限。`nifi``nifi``nifi` |
| `preserve.environment`             | 是否在使用时保护壳体环境（参见"sudo-E"人页）。默认情况下，这设置为错误。`run.as` |
| `lib.dir`                          | 用于 NiFi 的*lib*目录。默认情况下，此设置为`./lib`           |
| `conf.dir`                         | 用于 NiFi 的*邦联*目录。默认情况下，此设置为`./conf`         |
| `graceful.shutdown.seconds`        | 当 NiFi 被指示关闭时，引导程序将等待此秒数，以便该过程干净地关闭。在此时间内，如果服务仍在运行，Bootstrap 将处理该过程，或突然终止该过程。`kill` |
| `java.arg.N`                       | 流程开始时，任何数量的 JVM 参数都可以传递给 NiFi JVM。这些参数的定义是添加属性到*引导.conf*开始。除区分属性名称外，其余属性名称无关，并且将予以忽略。默认值包括最小和最大 Java 堆大小的属性、要使用的垃圾收集器、Java IO 临时目录等。`java.arg.` |
| `nifi.bootstrap.sensitive.key`     | 加密敏感配置值的根键（六价格式）。当 NiFi 启动时，此根键用于解密*nifi. 属性*文件中的敏感值，以便以后使用。加密配置工具可用于指定根键、加密*nifi.属性*中的敏感值和更新*引导。conf。*请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#encrypt_config_tool)示例。 |
| `notification.services.file`       | 当 NiFi 启动或停止时，或者当引导器检测到 NiFi 已死亡时，引导器能够向相关方发送有关这些事件的通知。此配置通过指定 XML 文件来定义可以使用哪些通知服务。有关此文件的更多资料，可在[通知服务](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#notification_services)部分找到。 |
| `notification.max.attempts`        | 如果通知服务已配置但无法执行其功能，则将再次尝试最多次尝试次数。此属性配置的最大尝试次数。默认值是 。`5` |
| `nifi.start.notification.services` | 此属性是与属性中定义的通知服务相对应的通知服务的逗号分离的通知服务标识符列表。只要 NiFi 启动，带有指定标识符的服务将用于通知其配置的接收者。`notification.services.file` |
| `nifi.stop.notification.services`  | 此属性是与属性中定义的通知服务相对应的通知服务的逗号分离的通知服务标识符列表。只要 NiFi 被停止，带有指定标识符的服务将用于通知其配置的接收者。`notification.services.file` |
| `nifi.died.notification.services`  | 此属性是与属性中定义的通知服务相对应的通知服务的逗号分离的通知服务标识符列表。如果引导确定 NiFi 意外死亡，则带有指定标识符的服务将用于通知其配置的接收者。`notification.services.file` |

## 通知服务

当 NiFi 启动启动或停止 NiFi 或检测到它意外死亡时，它能够通知配置的接收者。目前，提供的唯一机制是发送电子邮件或 HTTP POST 通知。通知服务配置文件是配置通知功能的 XML 文件。

XML 文件的默认位置是*conf/引导通知服务.xml*但是此值可以在*conf/引导.conf*文件中更改。

XML 文件的语法如下：

```
<services>    <!-- any number of service elements can be defined. -->    <service>        <id>some-identifier</id>        <!-- The fully-qualified class name of the Notification Service. -->        <class>org.apache.nifi.bootstrap.notification.email.EmailNotificationService</class>        <!-- Any number of properties can be set using this syntax.             The properties available depend on the Notification Service. -->        <property name="Property Name 1">Property Value</property>        <property name="Another Property Name">Property Value 2</property>    </service></services>
```

一旦配置了所需的服务，则可以在*bootstrap.conf*文件中引用它们。

### 电子邮件通知服务 

第一个通知是发送电子邮件和实施是。它具有以下可用属性：`org.apache.nifi.bootstrap.notification.email.EmailNotificationService`

| **财产**               | **必填** | **描述**                                                     |
| ---------------------- | -------- | ------------------------------------------------------------ |
| `SMTP Hostname`        | 真       | 用于发送电子邮件通知的 SMTP 服务器的主机名                   |
| `SMTP Port`            | 真       | 用于 SMTP 通信的端口                                         |
| `SMTP Username`        | 真       | SMTP 帐户的用户名                                            |
| `SMTP Password`        |          | SMTP 帐户的密码                                              |
| `SMTP Auth`            |          | 指示是否应使用身份验证的标记                                 |
| `SMTP TLS`             |          | 指示是否应启用 TLS 的标记                                    |
| `SMTP Socket Factory`  |          | `javax.net.ssl.SSLSocketFactory`                             |
| `SMTP X-Mailer Header` |          | 即将发送的电子邮件的头中使用的 X-邮件                        |
| `Content Type`         |          | 用于解释电子邮件内容的 Mime 类型，例如`text/plain``text/html` |
| `From`                 | 真       | 指定电子邮件地址用作发件人。否则，"友好名称"可以用作"从地址"，但该值必须以双报价封装。 |
| `To`                   |          | 收件人要包含在电子邮件的"到行"中                             |
| `CC`                   |          | 收件人要包含在电子邮件的 CC 行中                             |
| `BCC`                  |          | 收件人包含在电子邮件的 BCC 行中                              |

除了上述按要求标记的属性外，还必须设置至少一个属性或属性。`To``CC``BCC`

配置电子邮件服务的完整示例如下所示：

```
     <service>        <id>email-notification</id>        <class>org.apache.nifi.bootstrap.notification.email.EmailNotificationService</class>        <property name="SMTP Hostname">smtp.gmail.com</property>        <property name="SMTP Port">587</property>        <property name="SMTP Username">username@gmail.com</property>        <property name="SMTP Password">super-secret-password</property>        <property name="SMTP TLS">true</property>        <property name="From">"NiFi Service Notifier"</property>        <property name="To">username@gmail.com</property>     </service>
```

### HTTP 通知服务 

第二个通知是发送HTTP邮政请求和实施是。它具有以下可用属性：`org.apache.nifi.bootstrap.notification.http.HttpNotificationService`

| **财产**              | **必填** | **描述**                                                     |
| --------------------- | -------- | ------------------------------------------------------------ |
| `URL`                 | 真       | 将通知发送到的 URL。支持表达语言。                           |
| `Connection timeout`  |          | 连接到远程服务的最大等待时间。支持表达语言。这默认为 。`10s` |
| `Write timeout`       |          | 远程服务阅读发送的请求的最大等待时间。支持表达语言。这默认为 。`10s` |
| `Truststore Filename` |          | 信托商店的完全合格文件名                                     |
| `Truststore Type`     |          | 信托商店的类型。要么或`JKS``PKCS12`                          |
| `Truststore Password` |          | 信托商店的密码                                               |
| `Keystore Filename`   |          | 钥匙店的完全合格文件名                                       |
| `Keystore Type`       |          | 钥匙店的类型。要么或`JKS``PKCS12`                            |
| `Keystore Password`   |          | 钥匙店的密码                                                 |
| `Key Password`        |          | 密钥的密码。如果没有指定，但指定了钥匙店文件名、密码和类型，则键密码将假定为与钥匙店密码相同。 |
| `SSL Protocol`        |          | 用于此 SSL 上下文的算法。这可以是或。`SSL``TLS`              |

除了上述属性外，还可以添加动态属性。它们将作为头添加到 HTTP 请求中。支持表达语言。

通知消息位于 POST 请求的主体中。通知类型在"通知.类型"中，主题使用头"通知.主题"。

配置 HTTP 服务的完整示例可能如下所示：

```
     <service>        <id>http-notification</id>        <class>org.apache.nifi.bootstrap.notification.http.HttpNotificationService</class>        <property name="URL">https://testServer.com:8080/</property>        <property name="Truststore Filename">localhost-ts.jks</property>        <property name="Truststore Type">JKS</property>        <property name="Truststore Password">localtest<property>        <property name="Keystore Filename">localhost-ts.jks</property>        <property name="Keystore Type">JKS</property>        <property name="Keystore Password">localtest</property>        <property name="notification.timestamp">${now()}</property>     </service>
```

## 代理配置

在代理后面运行 Apache NiFi 时，在部署过程中需要注意几个关键项目。

- NiFi 由许多 Web 应用程序（Web UI、Web API、文档、自定义 UI、数据查看器等）组成，因此需要为**根路**配置映射。这样，所有上下文路径都会相应地传递。例如，如果只映射上下文路径，更新属性的自定义 UI 将不起作用，因为它在 。`/nifi``/update-attribute-ui-<version>`
- NiFi 的 REST API 将为图表上的每个组件生成尿素。由于请求是通过代理发出的，生成的 URI 的某些元素需要被覆盖。在不覆盖的情况下，用户将能够查看画布上的数据流，但无法修改现有组件。请求将尝试直接回电给 NiFi，而不是通过代理。当代理向 NiFi 实例生成 HTTP 请求时，可以通过添加以下 HTTP 头来覆盖 URI 的元素：

```
X-ProxyScheme - the scheme to use to connect to the proxyX-ProxyHost - the host of the proxyX-ProxyPort - the port the proxy is listening onX-ProxyContextPath - the path configured to map to the NiFi instance
```

- 如果 NiFi 运行安全，则需要授权任何代理用户请求。这些可以通过全球菜单在 NiFi UI 中配置。一旦这些权限到位，代理可以开始代理用户请求。最终用户身份必须在 HTTP 头中继。例如，如果最终用户向代理发送请求，则代理必须对用户进行身份验证。在此之后，代理可以将请求发送到 NiFi。在此请求中，应添加 HTTP 头，具体如下。

```
X-ProxiedEntitiesChain: <end-user-identity>
```

如果将代理配置为发送到其他代理，则从第二个代理向 NiFi 提出的请求应包含如下头。

```
X-ProxiedEntitiesChain: <end-user-identity><proxy-1-identity>
```

设置所需属性的示例 Apache 代理配置可能看起来像以下属性。完整的代理配置不在本文档的范围范围之外。请参阅代理文档以获取部署环境和使用案例的指导。

```
...<Location "/my-nifi">    ...	SSLEngine On	SSLCertificateFile /path/to/proxy/certificate.crt	SSLCertificateKeyFile /path/to/proxy/key.key	SSLCACertificateFile /path/to/ca/certificate.crt	SSLVerifyClient require	RequestHeader add X-ProxyScheme "https"	RequestHeader add X-ProxyHost "proxy-host"	RequestHeader add X-ProxyPort "443"	RequestHeader add X-ProxyContextPath "/my-nifi"	RequestHeader add X-ProxiedEntitiesChain "<%{SSL_CLIENT_S_DN}>"	ProxyPass https://nifi-host:8443	ProxyPassReverse https://nifi-host:8443	...</Location>...
```

- 必须更新其他 NiFi 代理配置，以便允许预期主机和上下文路径 HTTP 头。
  - 默认情况下，如果 NiFi 运行安全，它只会接受带有主机头的 HTTP 请求，该请求与主机（:p或），这是它必须接受的。如果 NiFi 要接受指向其他主机的请求[:p），则需要配置预期值。在代理后面或在容器化环境中运行时可能需要此。这配置在使用属性（例如）的*nifi.属性*中的逗号分离列表中。接受 IPv6 地址。有关其他详细信息，请参阅 RFC 5952 第[4](https://tools.ietf.org/html/rfc5952#section-4)节和第[6](https://tools.ietf.org/html/rfc5952#section-6)节。`nifi.web.proxy.host``localhost:18443, proxyhost:443`
  - NiFi 将仅接受带有 X 代理文本路径、X 转发上下文或 X 转发前缀标题的 HTTP 请求，如果*nifi. 属性*中的属性允许值。此属性接受预期值的逗号分离列表。如果传入请求具有不允许列表中未存在的 X-代理文本路径、X 转发上下文或 X 转发前缀标题值，则将显示"发生了意外错误"页面，并将错误写入*nifi-app.log。*`nifi.web.proxy.context.path`
- 代理服务器和 NiFi 集群需要额外的配置才能使 NiFi 站点到站点在反向代理后面工作。有关详细信息，请参阅[站点到站点路由属性以了解详细](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#site_to_site_reverse_proxy_properties)信息。
  - 为了通过反向代理通过站点到站点协议传输数据，代理和站点对站点客户端号 NiFi 用户都需要有以下策略，"检索站到站点的详细信息"，"通过站点到站点接收数据"以进行输入端口，以及"通过站点到站点发送数据"以用于输出端口。

## 克贝罗斯服务

NiFi 可配置为使用克贝罗斯 SPNEGO（或"克贝罗斯服务"）进行身份验证。在这种情况下，用户将点击 REST 端点，服务器将使用状态代码和挑战响应头进行响应。这将通信到浏览器以使用 GSS-API 并加载用户的 Kerberos 票，并在随后的请求中将其用作 Base64 编码的头值。这将是形式。NiFi 将尝试与 KDC 验证此票。如果成功，用户的*本金*将作为身份返回，流量将遵循登录/凭据身份验证，因为将发出 JWT 作为响应，以防止 Kerberos 身份验证在随后的每个请求上出现不必要的开销。如果无法验证该票，它将返回相应的错误响应代码。然后，如果已配置，用户将能够向登录表单提供其 Kerberos 凭据。有关详细信息，请参阅[Kerberos](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#kerberos_login_identity_provider)登录身份提供商。`/access/kerberos``401``WWW-Authenticate: Negotiate``Authorization: Negotiate YII…``KerberosLoginIdentityProvider`

NiFi 将只对 Kerberos SPNEGO 关于 HTTPS 连接的谈判做出回应，因为从未验证过不安全请求。

以下属性必须设置在*nifi.属性*中，以便启用 Kerberos 服务身份验证。

| **财产**            | **必填** | **描述**                       |
| ------------------- | -------- | ------------------------------ |
| `Service Principal` | 真       | NiFi 用于与 KDC 沟通的服务原则 |
| `Keytab Location`   | 真       | 包含服务主体的密钥塔的文件路径 |

有关完整文档，请参阅[Kerberos 属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#kerberos_properties)。

### 笔记

- Kerberos 在许多地方对案例敏感，错误消息（或缺乏错误消息）可能无法充分解释。检查配置文件中服务主体的案例敏感性。公约是.`HTTP/fully.qualified.domain@REALM`
- 浏览器在处理 SPNEGO 谈判时具有不同程度的限制。有些人会向任何请求它的域提供本地 Kerberos 票，而另一些则通过允许列表提前明确指定受信任的域名。参见[春季安全 Kerberos - 参考文档：用于为普通浏览器进行 SPNEGO 谈判的附录 E. 配置浏览](http://docs.spring.io/autorepo/docs/spring-security-kerberos/1.0.2.BUILD-SNAPSHOT/reference/htmlsingle/#browserspnegoconfig)器。
- 某些浏览器 （旧版 IE） 不支持最近的加密算法（如 AES），并且仅限于旧算法 （DES）。生成键盘时应注意这一点。
- 必须配置 KDC，并为 NiFi 定义服务原则和导出的键盘。Kerberos 服务器配置和管理的综合说明超出了本文档的范围（请参阅[麻省理工学院 Kerberos 管理指南](http://web.mit.edu/kerberos/krb5-current/doc/admin/index.html)），但示例如下：

在 KDC 中添加服务器服务委托人并从 KDC 中出口密钥塔布：`nifi.nifi.apache.org`

```
root@kdc:/etc/krb5kdc# kadmin.localAuthenticating as principal admin/admin@NIFI.APACHE.ORG with password.kadmin.local:  listprincsK/M@NIFI.APACHE.ORGadmin/admin@NIFI.APACHE.ORG...kadmin.local:  addprinc -randkey HTTP/nifi.nifi.apache.orgWARNING: no policy specified for HTTP/nifi.nifi.apache.org@NIFI.APACHE.ORG; defaulting to no policyPrincipal "HTTP/nifi.nifi.apache.org@NIFI.APACHE.ORG" created.kadmin.local:  ktadd -k /http-nifi.keytab HTTP/nifi.nifi.apache.orgEntry for principal HTTP/nifi.nifi.apache.org with kvno 2, encryption type des3-cbc-sha1 added to keytab WRFILE:/http-nifi.keytab.Entry for principal HTTP/nifi.nifi.apache.org with kvno 2, encryption type des-cbc-crc added to keytab WRFILE:/http-nifi.keytab.kadmin.local:  listprincsHTTP/nifi.nifi.apache.org@NIFI.APACHE.ORGK/M@NIFI.APACHE.ORGadmin/admin@NIFI.APACHE.ORG...kadmin.local: qroot@kdc:~# ll /http*-rw------- 1 root root 162 Mar 14 21:43 /http-nifi.keytabroot@kdc:~#
```

## 分析框架

NiFi 具有内部分析框架，可根据队列上阈值的配置设置，能够预测背压发生。默认用于预测的模型是普通最小方块 （OLS） 线性回归。它使用来自队列的最近观测结果（对象数或内容大小随着时间的推移），并计算该数据的回归行。然后，该行的方程用于确定将在给定时间间隔内达到的下一个值（例如，未来 5 分钟内排队的对象数）。以下是用于预测的队列/对象计数的线性回归模型示例图：

![Back pressure prediction based on Queue/Object Count](https://cdn.jsdelivr.net/gh/zshipu/images/202111011335262.png)

为了生成预测，对本地状态快照历史记录进行查询以获取足够的数据以生成模型。默认情况下，每分钟都会捕获组件状态快照。内部模型至少需要 2 个或更多观测来生成预测，因此默认情况下可能需要长达 2 分钟或更长的时间才能获得预测。如果预测比默认情况下提供的要早，则可以使用*nifi.属性*中的值调整快照的时间。`nifi.components.status.snapshot.frequency`

NiFi 在默认情况下使用模型的 R 方形分数在发送预测信息之前评估模型的有效性。一个重要注意事项：R-Square 是衡量回归线与观测数据的接近程度与预测的准确程度：因此，可能会有一定程度的错误。如果计算模型的 R 方形分数符合配置阈值（如所定义），则模型将用于预测。否则，在生成分数超过阈值的模型之前，不会使用该模型，并且无法提供预测。但是，默认 R 方形阈值可以根据预测要求进行调整。`nifi.analytics.connection.model.score.threshold``.90`

当出现背压时，可以配置预测间隔以进一步投影出来。还可以配置预测查询间隔，以确定应查询过去观测结果的追溯时间，以便生成模型。对这些设置的调整可能需要调整模型的评分阈值，以选择能够提供合理预测的分数。`nifi.analytics.predict.interval``nifi.analytics.query.interval`

有关配置分析属性的完整信息，请参阅[分析](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#analytics_properties)属性。

## 系统属性

目录中的*nifi.属性*文件是控制 NiFi 运行方式的主要配置文件。本节概述了此文件中的属性及其设置选项。`conf`

|      | 时间段和数据大小的值必须包括测量单位，例如"10 秒"或"10 MB"，而不仅仅是"10"。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

|      | 更改*nifi.属性*后，重新启动 NiFi 以使更改生效。 |
| ---- | ----------------------------------------------- |
|      |                                                 |

### 升级建议

*nifi.属性*文件的内容相对稳定，但可以从版本更改为版本。在升级时查看此文件并注意任何更改始终是一个好主意。

考虑配置下面标有星号（）的项目，这样升级将更容易。例如，将默认目录配置更改为主根部安装之外的位置。这样，这些项目可以通过升级保留在配置的位置，允许 NiFi 找到所有存储库和配置文件，并在旧版本停止和新版本启动后立即取回其关闭的位置。此外，管理员可以重用此*nifi.属性*文件和任何其他配置文件，而无需在每次升级时重新配置它们。有关详细信息，请参阅[升级 NiFi。](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#upgrading_nifi)`*`

### 核心属性 

*nifi. 属性*文件的第一部分用于核心属性。这些属性适用于整个核心框架。

| **财产**                                           | **描述**                                                     |
| -------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.flow.configuration.file`*                    | 流配置文件的位置（即包含当前在 NiFi 图上显示的内容的文件）。默认值是 。`./conf/flow.xml.gz` |
| `nifi.flow.configuration.archive.enabled`*         | 指定 NiFi 在更新流量时是否自动创建流量的备份副本。默认值是 。`true` |
| `nifi.flow.configuration.archive.dir`*             | 保存流的备份副本的存档目录的位置*.xml。*默认值是 。NiFi 删除旧存档文件，以根据存档文件的使用寿命、总大小和文件数量（分别指定）和属性来限制磁盘使用。如果没有指定这些存档限制，NiFi 使用默认条件，即用于和用于。 此清理机制仅考虑自动创建存档*流.xml*文件。如果此存档目录中还有其他文件或目录，NiFi 将忽略它们。自动创建的档案有文件名与ISO 8601格式时间戳前缀后。那是。例如。NiFi 在清理存档目录时检查文件名。如果您想在此目录中保留特定存档，而不必担心 NiFi 删除它，则可以通过使用不同的文件名模式复制它来这样做。`./conf/archive``nifi.flow.configuration.archive.max.time``max.storage``max.count``30 days``max.time``500 MB``max.storage``<original-filename>``<year><month><day>T<hour><minute><second>+<timezone offset>_<original filename>``20160706T160719+0900_flow.xml.gz` |
| `nifi.flow.configuration.archive.max.time`*        | 存档*流.xml文件的*寿命。NiFi 将在更新流时删除过期的存档文件*.xml*如果指定此属性。到期日根据当前系统时间和存档流的最后修改时间戳*确定.xml。*如果*nifi.属性*中没有指定存档限制，NiFi 会删除比。`30 days` |
| `nifi.flow.configuration.archive.max.storage`*     | 存档*流.xml*文件允许的总数据大小。NiFi 将删除最古老的存档文件，直到总存档文件大小小于此配置值（如果指定此属性）。如果*nifi.属性*中没有指定存档限制，NiFi 将对此进行使用。`500 MB` |
| `nifi.flow.configuration.archive.max.count`*       | 允许的存档文件数量。NiFi 将删除最古老的存档文件，以便在指定此属性时只能保留 N 最新档案。 |
| `nifi.flowcontroller.autoResumeState`              | 指示 NiFi 图上的组件是否应恢复到其最后状态。默认值是 。`true` |
| `nifi.flowcontroller.graceful.shutdown.period`     | 指示关闭期。默认值是 。`10 secs`                             |
| `nifi.flowservice.writedelay.interval`             | 当对*流量进行许多更改时.xml*此属性指定在写出更改之前等待多长时间，以便将更改分批为单个更改。默认值是 。`500 ms` |
| `nifi.administrative.yield.duration`               | 如果组件允许意外异常逃逸，则视为 bug。因此，该框架将暂停（或在行政上产生）该时间的组件。这样做是为了使组件不会消耗大量的系统资源，因为它已知在现有状态中存在问题。默认值是 。`30 secs` |
| `nifi.bored.yield.duration`                        | 当一个组件没有工作要做（即"无聊"）时，这是它会等待的时间量，然后检查它是否有新的数据要处理。这样，它就不会通过检查新工作而经常消耗 CPU 资源。设置此属性时，请注意，它可以为不经常有工作可做组件添加额外的延迟，因为一旦它们进入此"无聊"状态，他们将等待此时间，然后再检查更多工作。默认值是 。`10 ms` |
| `nifi.queue.backpressure.count`                    | 在两个组件之间绘制新连接时，这是该连接的背压对象阈值的默认值。默认值是，并且值必须是一个整数。`10000` |
| `nifi.queue.backpressure.size`                     | 在两个组件之间绘制新连接时，这是该连接的背压数据大小阈值的默认值。默认值是，并且值必须是数据大小，包括测量单位。`1 GB` |
| `nifi.authorizer.configuration.file`*              | 这是指定授权人定义方式的文件的位置。默认值是 。`./conf/authorizers.xml` |
| `nifi.login.identity.provider.configuration.file`* | 这是指定用户名/密码身份验证方式的文件的位置。只有在配置了提供商标识符的情况下才会考虑此文件。默认值是 。`nifi.security.user.login.identity.provider``./conf/login-identity-providers.xml` |
| `nifi.templates.directory`*                        | 这是保存流模板的目录位置（仅用于向后兼容性）。模板存储在*流中.xml.gz*从 NiFi 1.0 开始。模板目录可用于（批量）导入模板进入*流.xml.gz*自动在NiFi启动。默认值是 。`./conf/templates` |
| `nifi.ui.banner.text`                              | 这是横幅文本，可以配置为显示在用户界面的顶部。默认情况下，它是空白的。 |
| `nifi.ui.autorefresh.interval`                     | 用户界面自动刷新的时间间隔。默认值是 。`30 secs`             |
| `nifi.nar.library.directory`                       | 纳库的位置。默认值现在和现在都应该按现在的状态留下。注： 额外的库目录可以通过使用具有唯一后缀和单独路径的前缀作为值来指定。       例如，要提供另外两个库位置，用户还可以指定其他属性，其密钥为：提供三个总位置，包括 。  `./lib``nifi.nar.library.directory.``nifi.nar.library.directory.lib1=/nars/lib1``nifi.nar.library.directory.lib2=/nars/lib2``nifi.nar.library.directory` |
| `nifi.nar.working.directory`                       | 叙述工作目录的位置。默认值现在和现在都应该按现在的状态留下。`./work/nar` |
| `nifi.documentation.working.directory`             | 文档工作目录。默认值现在和现在都应该按现在的状态留下。`./work/docs/components` |
| `nifi.processor.scheduling.timeout`                | 是时候等待处理器的生命周期操作 （和 ） 完成之前， 其他生命周期操作 （例如，**停止**） 可以调用。默认值是 。`@OnScheduled``@OnUnscheduled``1 min` |

### 国家管理 

财产文件的国家管理部分提供了一个机制，用于配置本地和全集群的组件机制，以便组件保持状态。有关如何使用此信息，请参阅[国家管理](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#state_management)部分。

| **财产**                                              | **描述**                                                     |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.state.management.configuration.file`            | 包含本地和集群范围状态提供商配置的 XML 文件。默认值是 。`./conf/state-management.xml` |
| `nifi.state.management.provider.local`                | 要使用的地方国家提供者的 ID。此值必须与国家管理文件中其中一个元素*的价值相匹配.xml。*`id``local-provider` |
| `nifi.state.management.provider.cluster`              | 要使用的聚类状态提供商的 ID。此值必须与国家管理文件中其中一个元素*的价值相匹配.xml。*如果不进行聚类，则此值将被忽略，但组集中的节点需要该值。`id``cluster-provider` |
| `nifi.state.management.embedded.zookeeper.start`      | 具体说明 NiFi 的此实例是否应启动嵌入式ZooKeeper服务器。这与ZooKeeper国家提供者一起使用。 |
| `nifi.state.management.embedded.zookeeper.properties` | 指定包含已启动的嵌入式 ZooKeeper 服务器配置的属性文件（如果该属性设置为`nifi.state.management.embedded.zookeeper.start``true`) |

### H2 设置

H2 设置部分定义了 H2 数据库的设置，该数据库跟踪用户访问和流量控制器历史记录。

| **财产**                   | **描述**                                                     |
| -------------------------- | ------------------------------------------------------------ |
| `nifi.database.directory`* | H2 数据库目录的位置。默认值是 。`./database_repository`      |
| `nifi.h2.url.append`       | 此属性指定了添加到 H2 数据库连接字符串的其他参数。应使用默认值，不应更改。是的：。`;LOCK_TIMEOUT=25000;WRITE_DELAY=0;AUTO_SERVER=FALSE` |

### 流文件存储库

FlowFile 存储库跟踪系统中每个 FlowFile 的属性和当前状态。默认情况下，此存储库与所有其他存储库安装在同一根安装目录中：但是，如果可用，建议将其配置在单独的驱动器上。

目前，流程文件存储库有三个实施，详情如下。

| **财产**                                  | **描述**                                                     |
| ----------------------------------------- | ------------------------------------------------------------ |
| `nifi.flowfile.repository.implementation` | 流文件存储库实现。默认值是 。其他当前选项是和 。`org.apache.nifi.controller.repository.WriteAheadFlowFileRepository``org.apache.nifi.controller.repository.VolatileFlowFileRepository``org.apache.nifi.controller.repository.RocksDBFlowFileRepository` |

|      | 切换存储库实现只能在没有排队流量文件的情况下执行，并且只应谨慎执行。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 提前写流量文件存储库

```
WriteAheadFlowFileRepository`是默认实现。它持续流文件到磁盘，并可选配置以同步磁盘的所有更改。这是非常昂贵的，可以显著降低NiFi性能。但是，如果是，如果突然断电或操作系统崩溃，则可能会有数据丢失的可能性。默认值是 。`false``false
```

| **财产**                                       | **描述**                                                     |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `nifi.flowfile.repository.wal.implementation`  | 如果存储库实现配置为使用该属性，则此属性可用于指定应使用"提前写入日志"的实施。默认值是 。此版本的提前写日志添加到 Apache NiFi 的 1.6.0 版中，其开发是为了解决旧实施中存在的问题。如果发生断电或操作系统崩溃，旧的实现容易错误地恢复 FlowFiles。这可能导致在断电或操作系统崩溃后，在重新启动时将错误的属性或内容分配给 FlowFile。但是，如果需要，仍然可以选择使用以前的实施并接受该风险（例如，如果新实施显示一些意外错误）。为此，将此属性的价值设置为 。另一个可用的实现是 。如果此属性的价值发生变化，重新启动后，NiFi 仍将恢复使用以前配置的存储库编写的记录，并删除以前配置的实现所写的文件。`WriteAheadFlowFileRepository``org.apache.nifi.wali.SequentialAccessWriteAheadLog``org.wali.MinimalLockingWriteAheadLog``org.apache.nifi.wali.EncryptedSequentialAccessWriteAheadLog` |
| `nifi.flowfile.repository.directory`*          | 流文件存储库的位置。默认值是 。`./flowfile_repository`       |
| `nifi.flowfile.repository.checkpoint.interval` | 流文件存储库检查点间隔。默认值是 。`2 mins`                  |
| `nifi.flowfile.repository.always.sync`         | 如果设置为，存储库的任何更改都将同步到磁盘，这意味着 NiFi 将要求操作系统不要缓存信息。这是非常昂贵的，可以显著降低NiFi性能。但是，如果是，如果突然断电或操作系统崩溃，则可能会有数据丢失的可能性。默认值是 。`true``false``false` |

### 加密写提前流文件存储库属性

以上定义的所有属性（参见["提前写流文件存储库](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#write-ahead-flowfile-repository)"）仍然适用。此处仅列出了特定于加密的属性。有关更多信息，请参阅[用户指南中的加密 FlowFile 存储库](http://nifi.apache.org/docs/nifi-docs/html/user-guide.html#encrypted-flowfile)。

|      | 与加密内容和源库不同，存储库的实现在这里不会改变，只有*基础写入日志实现*。这允许更清洁的分离和更灵活的实现选择。应更改的属性，以启用加密是 。`nifi.flowfile.repository.wal.implementation` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

| **财产**                                                     | **描述**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.flowfile.repository.encryption.key.provider.implementation` | 这是**关键提供商**的完全合格的班级名称。关键提供商是用于访问加密密钥以保护内容声明的数据商店界面。目前有三个实现：直接从*nifi.属性*读取密钥，从加密文件中读取密钥，从标准中读取密钥。`StaticKeyProvider``FileBasedKeyProvider``KeyStoreKeyProvider``java.security.KeyStore` |
| `nifi.flowfile.repository.encryption.key.provider.location`  | 通往关键定义资源的路径（空为或类似路径为）。对于未来的提供商（如 HSM），这可能是一个连接字符串或 URL。`StaticKeyProvider``./keys.nkp``FileBasedKeyProvider` |
| `nifi.flowfile.repository.encryption.key.provider.password`  | 用于解密密密钥定义资源（如密钥商店）的密码。`KeyStoreKeyProvider` |
| `nifi.flowfile.repository.encryption.key.id`                 | 用于加密的主动密钥 ID（例如）。`Key1`                        |
| `nifi.flowfile.repository.encryption.key`                    | 要使用的密钥。关键格式是六角形编码 （） 但也可以使用 NiFi 工具包中的工具进行加密（请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)中的加密[配置工具](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#encrypt_config_tool)部分以了解更多信息）。`StaticKeyProvider``0123456789ABCDEFFEDCBA98765432100123456789ABCDEFFEDCBA9876543210``./encrypt-config.sh` |
| `nifi.flowfile.repository.encryption.key.id.`*               | 允许为 。例如，该线路将提供可用的密钥。`StaticKeyProvider``nifi.flowfile.repository.encryption.key.id.Key2=012…210``Key2` |

最简单的配置如下：

```
nifi.flowfile.repository.implementation=org.apache.nifi.controller.repository.WriteAheadFlowFileRepositorynifi.flowfile.repository.wal.implementation=org.apache.nifi.wali.EncryptedSequentialAccessWriteAheadLognifi.flowfile.repository.encryption.key.provider.implementation=org.apache.nifi.security.kms.StaticKeyProvidernifi.flowfile.repository.encryption.key.provider.location=nifi.flowfile.repository.encryption.key.id=Key1nifi.flowfile.repository.encryption.key=0123456789ABCDEFFEDCBA98765432100123456789ABCDEFFEDCBA9876543210
```

### 挥发性流文件存储库

此实现将 FlowFiles 存储在内存中而不是磁盘上。如果电源/机器发生故障或 NiFi 重新启动，**将导致**数据丢失。要使用此实现，请设置为 。`nifi.flowfile.repository.implementation``org.apache.nifi.controller.repository.VolatileFlowFileRepository`

### 罗克德布流文件存储库

此实现利用了 RocksDB 关键值存储。它使用周期性同步，以确保没有创建或接收的数据丢失（只要设置）。如果发生故障（例如断电），通过系统（即路由和转换）完成的 FlowFiles*工作*可能仍然丢失。具体来说，这些操作的记录可能会丢失，将受影响的 FlowFiles 恢复到以前的有效状态。从那里，他们将恢复正常的流路径。此保证是以延迟为系统添加新数据的操作为代价的。此延迟是可配置的（作为），并且可以调整到各个系统。`nifi.flowfile.repository.rocksdb.accept.data.loss``false``nifi.flowfile.repository.rocksdb.sync.period`

此存储库的配置参数分为两类，"以 NiFi 为中心"和"以 RocksDB 为中心"。以 NiFi 为中心的设置与 FlowFile 存储库的操作及其与 NiFi 的交互有关。以岩石数据库为中心的设置与基础岩石数据库回购上的设置直接相关。有关这些设置的更多信息可以在 RocksDB 文档中找到[：https://github.com/facebook/rocksdb/wiki/RocksJava-Basics。](https://github.com/facebook/rocksdb/wiki/RocksJava-Basics)

|      | Windows 用户需要确保"微软可视C++ 2015 可再分配"安装，以便此存储库工作。有关详细信息，请参阅以下链接[：https://github.com/facebook/rocksdb/wiki/RocksJava-Basics#maven-windows。](https://github.com/facebook/rocksdb/wiki/RocksJava-Basics#maven-windows) |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

要使用此实现，请设置为 。`nifi.flowfile.repository.implementation``org.apache.nifi.controller.repository.RocksDBFlowFileRepository`

**以 NiFi 为中心的配置属性**：

| **财产**                                                     | **描述**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.flowfile.repository.directory`                         | 流文件存储库的位置。默认值为'/flowfile_repository'。         |
| `nifi.flowfile.repository.rocksdb.sync.warning.period`       | 如果无法同步，记录警告的频率。默认值为 30 秒。               |
| `nifi.flowfile.repository.rocksdb.claim.cleanup.period`      | 标记内容声明的频率可破坏（以便可以从内容回购中删除它们）。默认值为 30 秒。 |
| `nifi.flowfile.repository.rocksdb.deserialization.threads`   | 在恢复 FlowFile 状态的启动中使用多少线程。默认值为 16。      |
| `nifi.flowfile.repository.rocksdb.deserialization.buffer.size` | 用于启动恢复 FlowFile 状态的缓冲器大小。默认值为 1000。      |
| `nifi.flowfile.repository.rocksdb.sync.period`               | 迫使同步到磁盘的频率。这是数据创建操作可以阻止的最大期限（如果是）。默认值为 10 毫秒。`nifi.flowfile.repository.rocksdb.accept.data.loss``false` |
| `nifi.flowfile.repository.rocksdb.accept.data.loss`          | 是否接受已接收/创建数据的损失。如果数据丢失是可以接受的，则设置此设置会增加吞吐量。默认值是假的。`true` |
| `nifi.flowfile.repository.rocksdb.enable.stall.stop`         | 是否启用根据配置的限制将寄存器的失速/停止写到存储库。启用此功能允许系统通过限制（延迟或拒绝）增加节点上的总 FlowFile 计数的操作来保护自己，以防止系统不堪重负。默认值是假的。 |
| `nifi.flowfile.repository.rocksdb.stall.period`              | 遇到指定标准时停滞的时间段。默认值为 100 毫秒。              |
| `nifi.flowfile.repository.rocksdb.stall.flowfile.count`      | 开始停滞的 FlowFile 计数写信给回购。默认值为 800000。        |
| `nifi.flowfile.repository.rocksdb.stall.heap.usage.percent`  | 开始停滞的堆使用写到回购。默认值为 95%。                     |
| `nifi.flowfile.repository.rocksdb.stop.flowfile.count`       | 流文件计数，开始停止创建新的流文件。默认值为 1100000。       |
| `nifi.flowfile.repository.rocksdb.stop.heap.usage.percent`   | 堆使用，开始停止创建新的流文件。默认值为 99.9%。             |
| `nifi.flowfile.repository.rocksdb.remove.orphaned.flowfiles.on.startup` | 是否允许存储库删除在启动时无法识别的 FlowFiles。由于这通常是配置或同步错误的结果，因此默认情况下会禁用该错误。只有当您绝对确定要丢失有关数据时，才应启用此功能。默认值是假的。 |
| `nifi.flowfile.repository.rocksdb.enable.recovery.mode`      | 是否启用"恢复模式"。这限制了一次加载到图形中的流文件数量，但实际上并未从系统中删除任何流文件（或内容）。这允许恢复在启动时遇到"记忆错误"或类似错误的系统。除非有必要恢复系统，否则不应启用此功能，并且应尽快禁用。**警告：**在恢复模式下，**不要**对图形进行修改。图表的更改可能导致无法从存储库中恢复进一步的 FlowFiles。默认值是假的。 |
| `nifi.flowfile.repository.rocksdb.recovery.mode.flowfile.count` | 在"恢复模式"中加载到图形中的流文件数。当 FlowFiles 离开系统时，额外的流文件将被加载到此限值。此设置不会阻止 FlowFiles 通过正常方式进入系统。默认值为 5000。 |

**以岩石DB为中心的配置属性：**

| **财产**                                                     | **描述**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.flowfile.repository.rocksdb.parallel.threads`          | 用于冲洗和压实的螺纹数。一个好的价值是内核的数量。有关更多信息，请参阅罗克德布。默认值为 8。`DBOptions.setIncreaseParallelism()` |
| `nifi.flowfile.repository.rocksdb.max.write.buffer.number`   | 内存中建立的写入缓冲的最大数量。有关更多信息，请参阅罗克德布/ 有关此处。默认值为 4。`ColumnFamilyOptions.setMaxWriteBufferNumber()``max_write_buffer_number` |
| `nifi.flowfile.repository.rocksdb.write.buffer.size`         | 在转换为磁盘文件中的排序数据之前，要在内存中积累的数据量。较大的值会提高性能，尤其是在批量负载期间。向上写缓冲器可以同时在内存中保存，因此您可能需要调整此参数以控制内存使用。有关更多信息，请参阅罗克德布/ 有关此处。默认值为 256 MB。`max_write_buffer_number``ColumnFamilyOptions.setWriteBufferSize()``write_buffer_size` |
| `nifi.flowfile.repository.rocksdb.level.0.slowdown.writes.trigger` | 对 0 级文件数量的软限制。此时，写作速度减慢。小于 0 的值意味着 0 级文件数量不会触发减速。有关更多信息，请参阅岩石数据库/ 有关更多信息。默认值为 20。`ColumnFamilyOptions.setLevel0SlowdownWritesTrigger()``level0_slowdown_writes_trigger` |
| `nifi.flowfile.repository.rocksdb.level.0.stop.writes.trigger` | 级别 0 文件的最大数量。此时将停止写作。有关更多信息，请参阅岩石数据库/ 有关更多信息。默认值为 40。`ColumnFamilyOptions.setLevel0StopWritesTrigger()``level0_stop_writes_trigger` |
| `nifi.flowfile.repository.rocksdb.delayed.write.bytes.per.second` | 如果触发减速，则给 DB 的有限写入率。如果压实进一步落后，RocksDB可能会决定放慢速度。有关更多信息，请参阅岩石数据库。默认值为 16 MB。`DBOptions.setDelayedWriteRate()` |
| `nifi.flowfile.repository.rocksdb.max.background.flushes`    | 指定并发背景冲洗作业的最大数量。有关更多信息，请参阅岩石数据库/ 有关更多信息。默认值为 1。`DBOptions.setMaxBackgroundFlushes()``max_background_flushes` |
| `nifi.flowfile.repository.rocksdb.max.background.compactions` | 指定并发背景压实作业的最大数量。有关更多信息，请参阅岩石数据库/ 有关更多信息。默认值为 1。`DBOptions.setMaxBackgroundCompactions()``max_background_compactions` |
| `nifi.flowfile.repository.rocksdb.min.write.buffer.number.to.merge` | 在写入存储之前，要合并的写入缓冲器的最小数量。有关更多信息，请参阅岩石数据库/ 有关更多信息。默认值为 1。`ColumnFamilyOptions.setMinWriteBufferNumberToMerge()``min_write_buffer_number_to_merge` |
| `nifi.flowfile.repository.rocksdb.stat.dump.period`          | 将岩石数据库、 统计数据倾倒到日志的时期。有关更多信息，请参阅岩石数据库/ 有关更多信息。默认值为 600 秒。`DBOptions.setStatsDumpPeriodSec()``stats_dump_period_sec` |

### 掉期管理

NiFi 将 FlowFile 信息保留在内存 （JVM） 中，但在传入数据激增期间，流文件信息可以开始占据大量 JVM，从而使系统性能受到影响。为了抵消这种影响，NiFi 将 FlowFile 信息暂时"交换"到磁盘中，直到更多 JVM 空间再次可用。这些属性控制该过程的发生方式。

| **财产**                           | **描述**                                                     |
| ---------------------------------- | ------------------------------------------------------------ |
| `nifi.swap.manager.implementation` | 交换管理器实现。默认值是 。有一个替代实现，即加密磁盘上的交换文件内容。为 FlowFile 存储库配置的加密密钥用于使用 AES-GCM 算法执行加密。`org.apache.nifi.controller.FileSystemSwapManager``EncryptedFileSystemSwapManager` |
| `nifi.queue.swap.threshold`        | NiFi 开始将流文件信息交换到磁盘的队列阈值。默认值是 。`20000` |

### 内容存储库

内容存储库保存系统中所有流文件的内容。默认情况下，它与所有其他存储库安装在同一根安装目录中：但是，如果可用，管理员可能会希望将其配置在单独的驱动器上。如果没有别的，最好是如果内容存储库不在同一驱动器上的 FlowFile 存储库。在处理大量数据的数据流中，内容存储库可能会填满磁盘，而 FlowFile 存储库（如果也在该磁盘上）可能会损坏。为了避免这种情况，在不同的驱动器上配置这些存储库。

| **财产**                                 | **描述**                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| `nifi.content.repository.implementation` | 内容存储库实现。默认值现在和应该谨慎更改。要将流文件内容存储在内存中而不是磁盘上（如果发生电源/机器故障，可能会丢失数据），请将此属性设置为 。`org.apache.nifi.controller.repository.FileSystemRepository``org.apache.nifi.controller.repository.VolatileContentRepository` |

### 文件系统内容存储库属性

| **财产**                                               | **描述**                                                     |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.content.repository.implementation`               | 内容存储库实现。默认值现在和应该谨慎更改。要将流文件内容存储在内存中而不是磁盘上（如果发生电源/机器故障，可能会丢失数据），请将此属性设置为 。`org.apache.nifi.controller.repository.FileSystemRepository``org.apache.nifi.controller.repository.VolatileContentRepository` |
| `nifi.content.claim.max.appendable.size`               | 内容声明的最大大小。默认值是 。`1 MB`                        |
| `nifi.content.repository.directory.default`*           | 内容存储库的位置。默认值是 。注：可以使用具有独特后缀和单独路径的前缀作为值来指定多个内容存储库。       例如，要提供两个额外的位置作为内容存储库的一部分，用户还可以指定其他属性，其密钥为：提供三个总位置，包括 。  `./content_repository``nifi.content.repository.directory.``nifi.content.repository.directory.content1=/repos/content1``nifi.content.repository.directory.content2=/repos/content2``nifi.content.repository.directory.default` |
| `nifi.content.repository.archive.max.retention.period` | 如果启用了存档（见下文），则此属性指定了保存存档数据的最大时间。默认值是 。`nifi.content.repository.archive.enabled``12 hours` |
| `nifi.content.repository.archive.max.usage.percentage` | 如果启用了存档（见下文），则此属性必须具有指示开始删除存档数据的内容存储库磁盘使用百分比值。如果存档是空的，内容存储库磁盘的使用率高于此百分比，则暂时禁用存档。当磁盘使用率低于此百分比时，将恢复存档。默认值是 。`nifi.content.repository.archive.enabled``50%` |
| `nifi.content.repository.archive.enabled`              | 要启用内容存档，应设置为并指定上述属性的价值。内容归档使来源 UI 能够查看或重播不再处于数据流队列中的内容。默认情况下，启用存档。`true``nifi.content.repository.archive.max.usage.percentage` |
| `nifi.content.repository.always.sync`                  | 如果设置为，存储库的任何更改都将同步到磁盘，这意味着 NiFi 将要求操作系统不要缓存信息。这是非常昂贵的，可以显著降低NiFi性能。但是，如果是，如果突然断电或操作系统崩溃，则可能会有数据丢失的可能性。默认值是 。`true``false``false` |
| `nifi.content.viewer.url`                              | 如果有网络内容查看器，则 URL。默认情况下，它是空白的。       |

### 加密文件系统内容存储库属性

以上定义的所有属性（参见[文件系统内容存储库属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#file-system-content-repository-properties)）仍然适用。此处仅列出了特定于加密的属性。有关更多信息，请参阅[用户指南中的加密内容存储库](http://nifi.apache.org/docs/nifi-docs/html/user-guide.html#encrypted-content)。

| **财产**                                                     | **描述**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.content.repository.encryption.key.provider.implementation` | 这是**关键提供商**的完全合格的班级名称。关键提供商是用于访问加密密钥以保护内容声明的数据商店界面。目前有三个实现：直接从*nifi.属性*读取密钥，从加密文件中读取密钥，从标准中读取密钥。`StaticKeyProvider``FileBasedKeyProvider``KeyStoreKeyProvider``java.security.KeyStore` |
| `nifi.content.repository.encryption.key.provider.location`   | 通往关键定义资源的路径（空为或类似路径为）。对于未来的提供商（如 HSM），这可能是一个连接字符串或 URL。`StaticKeyProvider``./keys.nkp``FileBasedKeyProvider` |
| `nifi.content.repository.encryption.key.provider.password`   | 用于解密密密钥定义资源（如密钥商店）的密码。`KeyStoreKeyProvider` |
| `nifi.content.repository.encryption.key.id`                  | 用于加密的主动密钥 ID（例如）。`Key1`                        |
| `nifi.content.repository.encryption.key`                     | 要使用的密钥。关键格式是六角形编码 （） 但也可以使用 NiFi 工具包中的工具进行加密（请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)中的加密[配置工具](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#encrypt_config_tool)部分以了解更多信息）。`StaticKeyProvider``0123456789ABCDEFFEDCBA98765432100123456789ABCDEFFEDCBA9876543210``./encrypt-config.sh` |
| `nifi.content.repository.encryption.key.id.`*                | 允许为 。例如，该线路将提供可用的密钥。`StaticKeyProvider``nifi.content.repository.encryption.key.id.Key2=012…210``Key2` |

最简单的配置如下：

```
nifi.content.repository.implementation=org.apache.nifi.controller.repository.crypto.EncryptedFileSystemRepository
nifi.content.repository.encryption.key.provider.implementation=org.apache.nifi.security.kms.StaticKeyProvider
nifi.content.repository.encryption.key.provider.location=
nifi.content.repository.encryption.key.id=Key1
nifi.content.repository.encryption.key=0123456789ABCDEFFEDCBA98765432100123456789ABCDEFFEDCBA9876543210
```

### 挥发性内容存储库属性

| **财产**                                      | **描述**                                          |
| --------------------------------------------- | ------------------------------------------------- |
| `nifi.volatile.content.repository.max.size`   | 内容存储库在内存中的最大大小。默认值是 。`100 MB` |
| `nifi.volatile.content.repository.block.size` | 内容存储库块大小。默认值是 。`32 KB`              |

### 普罗旺斯仓库

证明存储库包含与数据证明相关的信息。接下来的四个部分是普罗旺斯存储库属性。

| **财产**                                    | **描述**                                                     |
| ------------------------------------------- | ------------------------------------------------------------ |
| `nifi.provenance.repository.implementation` | 证明存储库实施。默认值是 。另外还有三个存储库。要将产地事件存储在内存中而不是磁盘上（在这种情况下，所有事件都会在重新启动时丢失，并且事件将按先发制人的顺序被逐出），将此属性设置为 。这在 Java 堆中留下了可配置的证明事件数量，因此可以保留的事件数量非常有限。`org.apache.nifi.provenance.WriteAheadProvenanceRepository``org.apache.nifi.provenance.VolatileProvenanceRepository`有第三个和第四个选项可用：和 .最初编写这些事件的简单目标是在生成时持续生成证明事件，并提供按顺序在这些事件上进行重述的能力。后来，人们希望能够压缩数据，以便存储更多的数据。之后，添加了对数据进行索引和查询的能力。随着需求的不断变化，存储库不断变化，无需进行重大重新设计。当用于负责处理大量小流量流文件的 NiFi 实例时，可以迅速成为瓶颈。然后编写这些文件是为了提供与提供更好的性能相同的功能。在 NiFi 的 1.2.0 版中添加了该版本。自那时以来，它已被证明是非常稳定和稳健的，因此被默认执行。现在被认为是弃用，不应该再使用。如果管理一个NIFI的例子，目前正在使用，强烈建议升级到。这样做就像将实施属性值更改为 。由于证明存储库是向后兼容的，因此不会丢失数据或功能。`org.apache.nifi.provenance.PersistentProvenanceRepository``org.apache.nifi.provenance.EncryptedWriteAheadProvenanceRepository``PersistentProvenanceRepository``PersistentProvenanceRepository``WriteAheadProvenanceRepository``PersistentProvenanceRepository``WriteAheadProvenanceRepository``PersistentProvenanceRepository``PersistentProvenanceRepository``WriteAheadProvenanceRepository``org.apache.nifi.provenance.PersistentProvenanceRepository``org.apache.nifi.provenance.WriteAheadProvenanceRepository`该数据建立在并确保数据在静止时加密。`EncryptedWriteAheadProvenanceRepository``WriteAheadProvenanceRepository`**注意：**将利用由。但是，可能无法读取由 。因此，一旦证明存储库更改为使用，它就不能在不删除证明存储库中的数据的情况下更改回该存储库。`WriteAheadProvenanceRepository``PersistentProvenanceRepository``PersistentProvenanceRepository``WriteAheadProvenanceRepository``WriteAheadProvenanceRepository``PersistentProvenanceRepository` |

### 提前写出证明存储库属性

| **财产**                                              | **描述**                                                     |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.provenance.repository.directory.default`*       | 证明库的位置。默认值是 。注： 多个来源存储库可以通过使用具有独特后缀和单独路径的前缀作为值来指定。       例如，要提供两个额外的位置作为来源存储库的一部分，用户还可以指定其他属性，其密钥为：提供三个总位置，包括 。  `./provenance_repository``nifi.provenance.repository.directory.``nifi.provenance.repository.directory.provenance1=/repos/provenance1``nifi.provenance.repository.directory.provenance2=/repos/provenance2``nifi.provenance.repository.directory.default` |
| `nifi.provenance.repository.max.storage.time`         | 保存数据来源信息的最大时间。默认值是 。`24 hours`            |
| `nifi.provenance.repository.max.storage.size`         | 一次存储的最大数据来源信息量。默认值是 。数据证明功能可以消耗大量的存储空间，因为保存了如此多的数据。对于生产环境，1-2 TB 或以上的值并不罕见。存储库将写入单个"事件文件"（或一组"事件文件"，如果多个存储位置被定义，如上文所述），直到事件文件达到属性中定义的大小。然后，它将"翻滚"，并开始编写新的事件到一个新的文件。数据总是一次从一个文件中老化，因此不建议将大量数据写入单个"事件文件"，因为这样可以防止旧数据如此顺利地老化。`10 GB``nifi.provenance.repository.rollover.size` |
| `nifi.provenance.repository.rollover.size`            | 要写到单个"事件文件"的数据量。默认值是 。对于产生大量数据证明的生产环境，其价值也非常合理。`100 MB``1 GB` |
| `nifi.provenance.repository.query.threads`            | 用于证明存储库查询的线程数。默认值是 。`2`                   |
| `nifi.provenance.repository.index.threads`            | 用于索引证明事件的线程数量，以便它们可搜索。默认值是 。对于在大量 FlowFiles 上运行的流量，证明事件的索引可能会成为瓶颈。如果发生这种情况，增加此属性的价值可能会提高证明存储库处理这些记录的速度，从而产生更好的总体吞吐量。建议每个存储位置至少使用 1 个线程（即，如果有 3 个存储位置，则应至少使用 3 个线程）。对于高吞吐量环境（提供更多 CPU 和磁盘 I/O）时，显著增加此值可能有意义。通常每个存储位置超过 2-4 线程是不有价值的。但是，这可以根据与 I/O 资源相比可用的 CPU 资源进行调整。`2` |
| `nifi.provenance.repository.compress.on.rollover`     | 指示在"事件文件"翻滚时是否压缩来源信息。默认值是 。`true`    |
| `nifi.provenance.repository.always.sync`              | 如果设置为，存储库的任何更改都将同步到磁盘，这意味着 NiFi 将要求操作系统不要缓存信息。这是非常昂贵的，可以显著降低NiFi性能。但是，如果是，如果突然断电或操作系统崩溃，则可能会有数据丢失的可能性。默认值是 。`true``false``false` |
| `nifi.provenance.repository.indexed.fields`           | 这是一个逗号分离的字段列表，应索引并使之可搜索。未编入索引的字段将无法搜索。有效字段是： ， ， ， ， ， ， .默认值为： .`EventType``FlowFileUUID``Filename``TransitURI``ProcessorID``AlternateIdentifierURI``Relationship``Details``EventType, FlowFileUUID, Filename, ProcessorID` |
| `nifi.provenance.repository.indexed.attributes`       | 这是一个逗号分离的 FlowFile 属性列表，应进行索引和可搜索。默认情况下，它是空白的。但是，要考虑的一些好例子是以及您可能使用的任何自定义属性，这些属性对于您的用例很有价值。`filename``mime.type` |
| `nifi.provenance.repository.index.shard.size`         | 存储库使用阿帕奇·卢塞尼执行索引和搜索功能。此值表示在存储库开始编写到新索引之前，Lucene 指数应变得有多大。在搜索证明存储库时，碎片大小的大值将导致更多的 Java 堆使用，但应提供更好的性能。默认值是 。但是，这是由于大多数用户开始使用 NiFi 的非常小的环境中对默认值进行了调整。对于生产环境，建议将此值更改为 。一旦索引中的所有证明事件都与"事件文件"分离，该索引也将被销毁。`500 MB``4``8 GB`**注意：**此值应小于（不超过物业的一半）。`nifi.provenance.repository.max.storage.size` |
| `nifi.provenance.repository.max.attribute.length`     | 指示 FlowFile 属性从存储库检索证明事件时的最大长度。如果任何属性的长度超过此值，则当事件被检索时，该属性将被截断。默认值是 。`65536` |
| `nifi.provenance.repository.concurrent.merge.threads` | 阿帕奇·卢塞内在索引中创建多个"段"。这些段定期合并在一起，以便提供更快的查询。此属性指定**允许用于每个**存储目录的最大线程数。默认值是 。对于高吞吐量环境，建议设置大于合并线程数的索引线程数 （ 存储位置数） 。例如，如果有 2 个存储位置，并且将索引线程数设置为，则合并线程的数量可能小于 。虽然这样做并非关键，但设置大于此的合并线程数量可能导致所有指数线程用于合并，这将导致 NiFi 流在索引发生时周期性地暂停，导致某些数据的处理延迟比其他数据高得多。`2``8``4` |
| `nifi.provenance.repository.warm.cache.frequency`     | 每次运行证明查询时，查询必须首先搜索 Apache Lucene 指数（至少在大多数情况下 - 经常运行一些查询，并且将结果缓存以避免搜索 Lucene 指数）。当 Lucene 指数首次打开时，它可能非常昂贵，需要几秒钟。这因具有许多不同的指数而变得更加复杂，并且可能导致普罗旺斯查询需要更长的时间。索引打开后，操作系统的磁盘缓存通常会保留足够的数据，使重新打开索引的速度更快 - 至少在一段时间内，直到磁盘缓存驱逐此数据。如果设置此值，NiFi 将定期打开每个 Lucene 索引，然后关闭该索引，以便"加热"缓存。当证明存储库很大时，这将导致更快的查询。然而，与所有伟大的事情一样，它也带来了成本。加热缓存确实需要一些 CPU 资源，但更重要的是，它会从操作系统磁盘缓存中驱逐其他数据，并导致从磁盘中读取（可能大量）数据。这可能导致 NiFi 性能降低。但是，如果 NiFi 在 CPU 和磁盘未充分利用的环境中运行，此功能可能会导致更快的证明查询。此属性的默认值为空白（即禁用）。 |

### 加密写提前证明存储库属性

以上定义的所有属性（参见["提前写"存储库属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#write-ahead-provenance-repository-properties)）仍然适用。此处仅列出了特定于加密的属性。有关更多信息，请参阅[用户指南中的加密证明存储库](http://nifi.apache.org/docs/nifi-docs/html/user-guide.html#encrypted-provenance)。

| **财产**                                                     | **描述**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.provenance.repository.encryption.key.provider.implementation` | 这是**关键提供商**的完全合格的班级名称。关键提供商是用于访问加密密钥以保护来源事件的数据商店界面。目前有三个实现：直接从*nifi.属性*读取密钥，从加密文件中读取密钥，从标准中读取密钥。`StaticKeyProvider``FileBasedKeyProvider``KeyStoreKeyProvider``java.security.KeyStore` |
| `nifi.provenance.repository.encryption.key.provider.location` | 通往关键定义资源的路径（空为或类似路径为）。对于未来的提供商（如 HSM），这可能是一个连接字符串或 URL。`StaticKeyProvider``./keys.nkp``FileBasedKeyProvider` |
| `nifi.provenance.repository.encryption.key.provider.password` | 用于解密密密钥定义资源（如密钥商店）的密码。`KeyStoreKeyProvider` |
| `nifi.provenance.repository.encryption.key.id`               | 用于加密的主动密钥 ID（例如）。`Key1`                        |
| `nifi.provenance.repository.encryption.key`                  | 要使用的密钥。关键格式是六角形编码 （） 但也可以使用 NiFi 工具包中的工具进行加密（请参阅[NiFi 工具包指南](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html)中的加密[配置工具](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#encrypt_config_tool)部分以了解更多信息）。`StaticKeyProvider``0123456789ABCDEFFEDCBA98765432100123456789ABCDEFFEDCBA9876543210``./encrypt-config.sh` |
| `nifi.provenance.repository.encryption.key.id.`*             | 允许为 。例如，该线路将提供可用的密钥。`StaticKeyProvider``nifi.provenance.repository.encryption.key.id.Key2=012…210``Key2` |

最简单的配置如下：

```
nifi.provenance.repository.implementation=org.apache.nifi.provenance.EncryptedWriteAheadProvenanceRepositorynifi.provenance.repository.encryption.key.provider.implementation=org.apache.nifi.security.kms.StaticKeyProvidernifi.provenance.repository.encryption.key.provider.location=nifi.provenance.repository.encryption.key.id=Key1nifi.provenance.repository.encryption.key=0123456789ABCDEFFEDCBA98765432100123456789ABCDEFFEDCBA9876543210
```

### 持久证明存储库属性

| **财产**                                          | **描述**                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.provenance.repository.directory.default`*   | 证明库的位置。默认值是 。注： 多个来源存储库可以通过使用具有独特后缀和单独路径的前缀作为值来指定。       例如，要提供两个额外的位置作为来源存储库的一部分，用户还可以指定其他属性，其密钥为：提供三个总位置，包括 。  `./provenance_repository``nifi.provenance.repository.directory.``nifi.provenance.repository.directory.provenance1=/repos/provenance1``nifi.provenance.repository.directory.provenance2=/repos/provenance2``nifi.provenance.repository.directory.default` |
| `nifi.provenance.repository.max.storage.time`     | 保存数据来源信息的最大时间。默认值是 。`24 hours`            |
| `nifi.provenance.repository.max.storage.size`     | 一次存储的最大数据来源信息量。默认值是 。`10 GB`             |
| `nifi.provenance.repository.rollover.time`        | 在滚动最新数据来源信息之前等待的时间量，以便在用户界面中提供。默认值是 。`30 secs` |
| `nifi.provenance.repository.rollover.size`        | 一次滚动的信息量。默认值是 。`100 MB`                        |
| `nifi.provenance.repository.query.threads`        | 用于证明存储库查询的线程数。默认值是 。`2`                   |
| `nifi.provenance.repository.index.threads`        | 用于索引证明事件的线程数量，以便它们可搜索。默认值是 。对于在大量 FlowFiles 上运行的流量，证明事件的索引可能会成为瓶颈。如果是这样的话，将出现一个公告，表示"数据流的速度超过来源记录速率。减慢流量以适应。如果发生这种情况，增加此属性的价值可能会提高证明存储库处理这些记录的速度，从而产生更好的总体吞吐量。`2` |
| `nifi.provenance.repository.compress.on.rollover` | 指示在滚动时是否压缩来源信息。默认值是 。`true`              |
| `nifi.provenance.repository.always.sync`          | 如果设置为，存储库的任何更改都将同步到磁盘，这意味着 NiFi 将要求操作系统不要缓存信息。这是非常昂贵的，可以显著降低NiFi性能。但是，如果是，如果突然断电或操作系统崩溃，则可能会有数据丢失的可能性。默认值是 。`true``false``false` |
| `nifi.provenance.repository.journal.count`        | 应用于序列化证明事件数据的期刊文件数量。增加此值将允许更多任务同时更新存储库，但稍后将导致更昂贵的期刊文件合并。理想情况下，此值应等于预期同时更新存储库的线程数，但 16 个线程往往在必须的环境中工作良好。默认值是 。`16` |
| `nifi.provenance.repository.indexed.fields`       | 这是一个逗号分离的字段列表，应索引并使之可搜索。未编入索引的字段将无法搜索。有效字段是： ， ， ， ， ， ， .默认值为： .`EventType``FlowFileUUID``Filename``TransitURI``ProcessorID``AlternateIdentifierURI``Relationship``Details``EventType, FlowFileUUID, Filename, ProcessorID` |
| `nifi.provenance.repository.indexed.attributes`   | 这是一个逗号分离的 FlowFile 属性列表，应进行索引和可搜索。默认情况下，它是空白的。但一些好的例子要考虑是，以及任何自定义的Tritube，你可能会使用，这是有价值的，你的使用的情况下。`filename``uuid``mime.type` |
| `nifi.provenance.repository.index.shard.size`     | 在搜索证明存储库时，碎片大小的大值将导致更多的 Java 堆使用，但应提供更好的性能。默认值是 。`500 MB` |
| `nifi.provenance.repository.max.attribute.length` | 指示 FlowFile 属性从存储库检索证明事件时的最大长度。如果任何属性的长度超过此值，则当事件被检索时，该属性将被截断。默认值是 。`65536` |

### 挥发性证明存储库属性

| **财产**                                 | **描述**                                         |
| ---------------------------------------- | ------------------------------------------------ |
| `nifi.provenance.repository.buffer.size` | 证明存储库缓冲器大小。默认值是起源事件。`100000` |

### 状态历史存储库

状态历史记录存储库包含用户界面中的组件状态历史记录和节点状态历史工具的信息。以下属性控制这些工具的工作原理。

| **财产**                                           | **描述**                                                     |
| -------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.components.status.repository.implementation` | 状态历史存储库实施。默认值是，它存储内存中的状态历史记录。 还支持并在磁盘上存储状态历史信息，以便可跨重新启动，并可以存储更长的时间。`org.apache.nifi.controller.status.history.VolatileComponentStatusRepository``org.apache.nifi.controller.status.history.EmbeddedQuestDbStatusHistoryRepository` |
| `nifi.components.status.snapshot.frequency`        | 此值表示捕获组件状态历史记录的快照的频率。默认值是 。`1 min` |

#### 在内存存储库中

如果属性的价值是，状态历史数据将存储在内存中。如果应用程序停止，所有收集到的信息都将丢失。`nifi.components.status.repository.implementation``VolatileComponentStatusRepository`

并协同工作，以确定要保留的历史数据量。例如，要配置两天的历史数据，每 5 分钟发生一次数据点快照，则配置为"5 分钟"和缓冲。为了进一步解释此示例，该时间段每 60 分钟就有 12 个（60 / 5）快照窗口。要将这些数据保留 48 小时（12 * 48），您最终的缓冲尺寸为 576。`buffer.size``snapshot.frequency``snapshot.frequency`

| **财产**                                        | **描述**                                        |
| ----------------------------------------------- | ----------------------------------------------- |
| `nifi.components.status.repository.buffer.size` | 指定状态历史存储库的缓冲大小。默认值是 。`1440` |

#### 持久存储库

如果属性的价值是，状态历史数据将以持久的方式存储到磁盘中。数据将在重新启动之间保存。`nifi.components.status.repository.implementation``EmbeddedQuestDbStatusHistoryRepository`

| **财产**                                                | **描述**                                                     |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.status.repository.questdb.persist.node.days`      | 节点状态数据（如无存储库磁盘空间、垃圾收集信息等）的保存天数。默认值是 。`14` |
| `nifi.status.repository.questdb.persist.component.days` | 组件状态数据（即每个处理器、连接等的统计数据）将保留的天数。默认值是 。`3` |
| `nifi.status.repository.questdb.persist.location`       | 持久状态历史存储库的位置。默认值是 。`./status_repository`   |

### 站点到站点属性

当数据流中配置远程处理组时，这些属性控制 NiFi 的此实例如何与 NiFi 的远程实例进行通信。远程流程组可以从 RAW 和 HTTP 中选择运输协议。命名的属性是原始运输协议的特定属性。同样，HTTP 运输协议的特定属性也是如此。`nifi.remote.input.socket.*``nifi.remote.input.http.*`

| **财产**                                 | **描述**                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| `nifi.remote.input.host`                 | 将提供给客户端的主机名称，用于连接到此 NiFi 实例进行站点到站点的通信。默认情况下，它是来自 。在类似 UNIX 的操作系统上，这通常是来自命令的输出。`InetAddress.getLocalHost().getHostName()``hostname` |
| `nifi.remote.input.secure`               | 这表明此 NiFi 实例和远程 NiFi 实例之间的通信是否应是安全的。默认情况下，它被设置为 。为了安全地到现场工作，请设置属性。还必须配置许多其他[安全属性](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#security_properties)。`false``true` |
| `nifi.remote.input.socket.port`          | 用于站点对站点通信的远程输入插座端口。默认情况下，它是空白的，但它必须具有价值，才能将 RAW 插座用作站点到站点的传输协议。 |
| `nifi.remote.input.http.enabled`         | 具体说明 HTTP 站点到站点是否应在此主机上启用。默认情况下，它被设置为 。 站点到站点的客户是否使用 HTTP 或 HTTPS 取决于 。如果它被设置为，那么请求将作为 HTTPS 发送到 。如果设置为 ，HTTP 请求将发送到 。`true``nifi.remote.input.secure``true``nifi.web.https.port``false``nifi.web.http.port` |
| `nifi.remote.input.http.transaction.ttl` | 指定交易在服务器上可以存活多久。默认情况下，它被设置为 。 如果在此时间段之后，站点到站点的客户端未执行下一个操作，则从远程 NiFi 实例中丢弃该交易。例如，当客户端创建交易但不发送或接收流文件时，或者当客户端发送或接收流文件但不确认该交易时。`30 secs` |
| `nifi.remote.contents.cache.expiration`  | 指定 NiFi 在通过站点到站点进行通信时应缓存有关远程 NiFi 实例的信息的时间。默认情况下，NiFi 将缓 存来自远程系统的响应。这使得 NiFi 能够避免不断向远程系统提出 HTTP 请求，当 NiFi 的此实例具有许多远程过程组实例时，这一点尤为重要。`30 secs` |

### 反向代理的站点到站点路由属性

站点到站点需要客户端和远程 NiFi 节点之间的点对点通信。例如，如果远程 NiFi 聚类有 3 个节点（并且）， 则必须访问每个远程节点的客户请求。`nifi0``nifi1``nifi2`

如果计划通过互联网或公司防火墙接收/传输来自/到站点到站点客户的数据，则可以在 NiFi 聚类节点前部署反向代理服务器，作为将客户端请求路由到上游 NiFi 节点的网关，以减少必须暴露的服务器和端口数量。

在这种环境中，同一 NiFi 聚类也有望由同一网络中的站点对站点客户访问。将 FlowFiles 发送到自己，以便在 NiFi 聚类节点之间进行负载分配，这可能是一个典型的示例。在这种情况下，客户请求应直接路由到节点，而无需通过反向代理。

为了支持此类部署，远程 NiFi 集群需要根据客户端请求上下文动态地暴露其站点到站点端点。以下属性配置对等应如何暴露给客户。路由定义由 4 个属性组成，，并按和。可以配置多个路由定义。 表示站点到站点的传输协议，即 或。`when``hostname``port``secure``protocol``name``protocol``RAW``HTTP`

| **财产**                                       | **描述**                                                     |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `nifi.remote.route.{protocol}.{name}.when`     | 布尔价值，或.控制是否应使用此名称的路由定义。`true``false`   |
| `nifi.remote.route.{protocol}.{name}.hostname` | 指定主机名，该主机将被介绍给站点到站点的客户进行进一步通信。 |
| `nifi.remote.route.{protocol}.{name}.port`     | 指定端口编号，该端口号将介绍给站点到站点的客户进行进一步通信。 |
| `nifi.remote.route.{protocol}.{name}.secure`   | 布尔价值，或.指定是否应通过安全协议访问远程对等。默认到 。`true``false``false` |

以上所有路由属性都可以使用 NiFi 表达语言从请求上下文计算目标对等描述。可用变量包括：

| **可变名称**                   | **描述**                                                     |
| ------------------------------ | ------------------------------------------------------------ |
| `s2s.{source|target}.hostname` | 请求来源的主机名和原始目标。                                 |
| `s2s.{source|target}.port`     | 与上述情况相同，用于端口。源端口可能没有用处，因为它只是一个客户端端端口 TCP 端口。 |
| `s2s.{source|target}.secure`   | 与上述相同，无论是否安全。                                   |
| `s2s.protocol`                 | 正在使用的站点到站点协议的名称，或 。`RAW``HTTP`             |
| `s2s.request`                  | 当前请求类型的名称，或 。有关详细信息，请参阅下面的站点到站点协议序列。`SiteToSiteDetail``Peers` |
| `HTTP request headers`         | HTTP 请求头值可以按其名称转介。                              |

#### 站点到站点协议序列

正确配置这些属性需要对站点到站点协议序列进行一些了解。

1. 客户端通过向指定的远程 URL 发送 HTTP （S） 请求来启动站点到站点协议，以获取远程聚类站点到站点信息。具体来说，要*"/NIFI-阿皮/站点到现场*"。此请求被调用。`SiteToSiteDetail`
2. 远程 NiFi 节点响应其输入和输出端口，以及 RAW 和 TCP 运输协议的 TCP 端口编号。
3. 客户发送另一个请求，以便使用#2 返回的 TCP 端口号码来获取远程对等。根据此请求，原始插座通信用于原始运输协议，而 HTTP 则继续使用 HTTP （S）。此请求被调用。`Peers`
4. 远程 NiFi 节点会响应包含主机名、端口、安全和工作负载（如排队流文件数量）的可用远程对等列表。从此，客户端和远程 NiFi 节点之间将进行进一步通信。
5. 客户端根据工作负载信息决定从/到哪个对等传输数据。
6. 客户端向远程 NiFi 节点发送创建交易的请求。
7. 远程 NiFi 节点接受交易。
8. 数据发送到目标对等。可批量发送多个数据包。
9. 当没有更多的数据要发送或达到批量限制时，交易通过计算发送数据的 CRC32 哈希在两端得到确认。
10. 交易在两端都承诺。

#### 反向代理配置

大多数反向代理软件都实现了 HTTP 和 TCP 代理模式。对于 NiFi RAW 站点到站点协议，需要 HTTP 和 TCP 代理配置，并且至少需要打开 2 个端口。NiFi HTTP 站点到站点协议可以将反向代理所需的打开端口数量最小化为 1。

在反向代理设置正确的 HTTP 头对于 NiFi 正确工作至关重要，不仅路由请求，还授权客户请求。另请参阅[代理配置](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#proxy_configuration)以了解详细信息。

有两种类型的请求-NiFi-节点映射技术，这些技术可以应用于反向代理服务器。一个是"节点的服务器名称"，另一个是"端口编号到节点"。

使用"服务器名称到节点"，同一端口可用于根据请求的服务器名称（例如）将请求路由到不同的上游 NiFi 节点。主机名称分辨率应配置为将不同的主机名称映射到相同的反向代理地址，这可以通过添加 /etc/主机文件或 DNS 服务器条目来完成。此外，如果客户端反向代理使用 HTTPS，则反向代理服务器证书应具有通配符通用名称或 SAN，以便由不同的主机名称访问。`nifi0.example.com``nifi1.example.com`

某些反向代理技术不支持服务器名称路由规则，在这种情况下，使用"端口编号到节点"技术。"端口编号到节点"映射要求 N 开端口位于由 N 节点组成的 NiFi 聚类的反向代理。

实际配置请参阅以下示例。

#### 站点到站点和反向代理示例

下面是一些反向代理和 NiFi 设置，以说明配置文件的外观。

下图中的客户端 1 代表没有直接访问 NiFi 节点的客户端，它通过反向代理访问，而客户端 2 则具有直接访问权限。

在此示例中，Nginx 用作反向代理。

##### 示例 1： RAW - 节点映射的服务器名称

![Server name to Node mapping](https://cdn.jsdelivr.net/gh/zshipu/images/202111011336502.svg)

1. 客户端 1 启动站点到站点协议，请求被路由到上游 NiFi 节点之一。NiFi 节点计算 RAW 的站点到站点端口。通过*以下所示的 nifi.属性*中的路由规则**示例**1，返回端口 10443。
2. 客户1要求同行，请求被路由到。NiFi 节点通过**示例 1**路由规则计算可用的对等，转换为因此，，并返回。`nifi.example.com:10443``nifi0:8081``nifi0:8081``nifi0.example.com:10443``nifi1``nifi2``nifi0.example.com:10443``nifi1.example.com:10443``nifi2.example.com:10443`
3. 客户端 1 决定用于进一步沟通。`nifi2.example.com:10443`
4. 另一方面，Client2 有两个 URIs 用于站点到站点的引导 URI，并使用其中之一启动协议。**示例 1**路由与此请求不匹配，并返回端口 8081。
5. 客户2询问同行从。**示例 1**不匹配，因此原始的，并且按原样返回。`nifi1:8081``nifi0:8081``nifi1:8081``nifi2:8081`
6. 客户端 2 决定用于进一步沟通。`nifi2:8081`

在*nifi.属性*中定义的路由规则**示例 1（**所有节点具有相同的路由配置）：

```
# S2S Routing for RAW, using server name to nodenifi.remote.route.raw.example1.when=\${X-ProxyHost:equals('nifi.example.com'):or(\${s2s.source.hostname:equals('nifi.example.com'):or(\${s2s.source.hostname:equals('192.168.99.100')})})}nifi.remote.route.raw.example1.hostname=${s2s.target.hostname}.example.comnifi.remote.route.raw.example1.port=10443nifi.remote.route.raw.example1.secure=true
```

*nginx.conf* ：

```
http {

    upstream nifi {
        server nifi0:8443;
        server nifi1:8443;
        server nifi2:8443;
    }

    # Use dnsmasq so that hostnames such as 'nifi0' can be resolved by /etc/hosts
    resolver 127.0.0.1;

    server {
        listen 443 ssl;
        server_name nifi.example.com;
        ssl_certificate /etc/nginx/nginx.crt;
        ssl_certificate_key /etc/nginx/nginx.key;

        proxy_ssl_certificate /etc/nginx/nginx.crt;
        proxy_ssl_certificate_key /etc/nginx/nginx.key;
        proxy_ssl_trusted_certificate /etc/nginx/nifi-cert.pem;

        location / {
            proxy_pass https://nifi;
            proxy_set_header X-ProxyScheme https;
            proxy_set_header X-ProxyHost nginx.example.com;
            proxy_set_header X-ProxyPort 17590;
            proxy_set_header X-ProxyContextPath /;
            proxy_set_header X-ProxiedEntitiesChain <$ssl_client_s_dn>;
        }
    }
}

stream {

    map $ssl_preread_server_name $nifi {
        nifi0.example.com nifi0;
        nifi1.example.com nifi1;
        nifi2.example.com nifi2;
        default nifi0;
    }

    resolver 127.0.0.1;

    server {
        listen 10443;
        proxy_pass $nifi:8081;
    }
}
```

##### 示例 2： RAW - 端口编号到节点映射

![Port number to Node mapping](https://cdn.jsdelivr.net/gh/zshipu/images/202111011336100.svg)

**示例 2**路由将原始主机名称（和） 映射到不同的代理端口（和） 使用和表达。`nifi0``nifi1``nifi2``10443``10444``10445``equals``ifElse`

在*nifi.属性*中定义的路由规则**示例 2（**所有节点具有相同的路由配置）：

```
# S2S Routing for RAW, using port number to nodenifi.remote.route.raw.example2.when=\${X-ProxyHost:equals('nifi.example.com'):or(\${s2s.source.hostname:equals('nifi.example.com'):or(\${s2s.source.hostname:equals('192.168.99.100')})})}nifi.remote.route.raw.example2.hostname=nifi.example.comnifi.remote.route.raw.example2.port=\${s2s.target.hostname:equals('nifi0'):ifElse('10443',\${s2s.target.hostname:equals('nifi1'):ifElse('10444',\${s2s.target.hostname:equals('nifi2'):ifElse('10445',\'undefined')})})}nifi.remote.route.raw.example2.secure=true
```

*nginx.conf* :

```
http {
    # Same as example 1.
}

stream {

    map $ssl_preread_server_name $nifi {
        nifi0.example.com nifi0;
        nifi1.example.com nifi1;
        nifi2.example.com nifi2;
        default nifi0;
    }

    resolver 127.0.0.1;

    server {
        listen 10443;
        proxy_pass nifi0:8081;
    }
    server {
        listen 10444;
        proxy_pass nifi1:8081;
    }
    server {
        listen 10445;
        proxy_pass nifi2:8081;
    }
}
```

##### 示例 3： HTTP - 节点映射的服务器名称

![Server name to Node mapping](https://cdn.jsdelivr.net/gh/zshipu/images/202111011336865.svg)

在*nifi.属性*中定义的路由规则**示例 3（**所有节点具有相同的路由配置）：

```
# S2S Routing for HTTP
nifi.remote.route.http.example3.when=${X-ProxyHost:contains('.example.com')}
nifi.remote.route.http.example3.hostname=${s2s.target.hostname}.example.com
nifi.remote.route.http.example3.port=443
nifi.remote.route.http.example3.secure=true
```

*nginx.conf* ：

```
http {
    upstream nifi_cluster {
        server nifi0:8443;
        server nifi1:8443;
        server nifi2:8443;
    }

    # If target node is not specified, use one from cluster.
    map $http_host $nifi {
        nifi0.example.com:443 "nifi0:8443";
        nifi1.example.com:443 "nifi1:8443";
        nifi2.example.com:443 "nifi2:8443";
        default "nifi_cluster";
    }

    resolver 127.0.0.1;

    server {
        listen 443 ssl;
        server_name ~^(.+\.example\.com)$;
        ssl_certificate /etc/nginx/nginx.crt;
        ssl_certificate_key /etc/nginx/nginx.key;

        proxy_ssl_certificate /etc/nginx/nginx.crt;
        proxy_ssl_certificate_key /etc/nginx/nginx.key;
        proxy_ssl_trusted_certificate /etc/nginx/nifi-cert.pem;

        location / {
            proxy_pass https://$nifi;
            proxy_set_header X-ProxyScheme https;
            proxy_set_header X-ProxyHost $1;
            proxy_set_header X-ProxyPort 443;
            proxy_set_header X-ProxyContextPath /;
            proxy_set_header X-ProxiedEntitiesChain <$ssl_client_s_dn>;
        }
    }
}
```

### 网络属性

这些属性与基于 Web 的用户界面相关。

| **财产**                              | **描述**                                                     |
| ------------------------------------- | ------------------------------------------------------------ |
| `nifi.web.http.host`                  | HTTP 主机。默认值为空白。                                    |
| `nifi.web.http.port`                  | HTTP 端口。默认值为空白。                                    |
| `nifi.web.http.port.forwarding`       | 转发传入 HTTP 请求的端口。此属性设计用于"端口转发"，当 NiFi 必须由非根用户启动才能获得更好的安全性时，它需要通过低端口才能通过防火墙。例如，要通过 80 端口上的 HTTP 协议曝光 NiFi，但实际在端口 8080 上收听，您需要配置操作系统级别的端口转发，例如将请求重定向为 80 到 8080 的 （macOS）。然后设置为 8080，并设置为 80。默认情况下，它是空白的。`nifi.web.http.host``iptables``pfctl``nifi.web.http.port``nifi.web.http.port.forwarding` |
| `nifi.web.http.network.interface`*    | NiFi 应为 HTTP 请求绑定的网络界面的名称。默认情况下，它是空白的。注： 多个网络接口可以通过使用具有独特后缀和单独网络接口名称的前缀作为值来指定。       例如，要提供两个额外的网络接口，用户还可以指定其他属性，其密钥为：提供三个网络总接口，包括 。  `nifi.web.http.network.interface.``nifi.web.http.network.interface.eth0=eth0``nifi.web.http.network.interface.eth1=eth1``nifi.web.http.network.interface.default` |
| `nifi.web.https.host`                 | HTTPS 主机。默认值是 。`127.0.0.1`                           |
| `nifi.web.https.port`                 | 赫特普斯端口。默认值是 。`8443`                              |
| `nifi.web.https.port.forwarding`      | 相同， 但与 Https 的安全通信。默认情况下，它是空白的。`nifi.web.http.port.forwarding` |
| `nifi.web.https.ciphersuites.include` | 用于初始化码头 HTTPS 端口的 SSLContext 的密码套件。如果未指定，则使用运行时 SSLContext 默认值。 |
| `nifi.web.https.ciphersuites.exclude` | SSL 客户端可能不使用的密码套件可建立与码头的连接。如果未指定，则使用运行时 SSLContext 默认值。在 Chrome 中，与 Jetty 协商的 SSL 密码可以在"开发人员工具"插件中、"安全"选项卡中进行检查。在 Firefox 中，与 Jetty 协商的 SSL 密码可以在浏览器地址栏 URL 左侧的"安全连接"小部件中检查。 |
| `nifi.web.https.network.interface`*   | NiFi 应为 HTTPS 请求绑定的网络界面的名称。默认情况下，它是空白的。注： 多个网络接口可以通过使用具有独特后缀和单独网络接口名称的前缀作为值来指定。       例如，要提供两个额外的网络接口，用户还可以指定其他属性，其密钥为：提供三个网络总接口，包括 。  `nifi.web.https.network.interface.``nifi.web.https.network.interface.eth0=eth0``nifi.web.https.network.interface.eth1=eth1``nifi.web.https.network.interface.default` |
| `nifi.web.jetty.working.directory`    | 码头工作目录的位置。默认值是 。`./work/jetty`                |
| `nifi.web.jetty.threads`              | 码头线程的数量。默认值是 。`200`                             |
| `nifi.web.max.header.size`            | 请求和响应头允许的最大大小。默认值是 。`16 KB`               |
| `nifi.web.proxy.host`                 | 允许 HTTP 主机头值的逗号分离列表，以考虑 NiFi 何时安全运行，并将收到对不同主机的请求[:p或），而不是它所必须的。例如，在 Docker 容器中或代理后面运行时（例如本地托运行：18443，代理托运行：443）。默认情况下，此值是空白的，这意味着 NiFi 应只允许向主机发送 niFi 必须发送的请求[:p或）。 |
| `nifi.web.proxy.context.path`         | 允许 HTTP X 代理文本路径、X 转发上下文或 X 转发前缀标题值的逗号分离列表。。默认情况下，此值为空白，这意味着包含代理上下文路径的所有请求均被拒绝。配置此属性将允许在此列表中包含代理路径的请求。 |
| `nifi.web.max.content.size`           | PUT 和 POST 请求的最大尺寸 （HTTP）。没有为向后兼容性设置默认值。为此属性提供值可启用所有传入的 API 请求（站点到站点和聚类通信除外）的筛选。建议值是 。`Content-Length``Content-Length``20 MB` |
| `nifi.web.max.requests.per.second`    | 每秒连接的最大请求数。超过此请求先被延迟，然后被限制。       |
| `nifi.web.request.ip.whitelist`       | IP 地址的逗号分离列表。用于指定客户端的 IP 地址，这些地址可能超过每秒的最大请求 （）。不适用于 Web 请求超时。`nifi.web.max.requests.per.second` |
| `nifi.web.request.timeout`            | Web 请求的请求超时。运行时间超过此时间的请求将被迫以 HTTP 503 服务不可用响应结束。默认值是 。`60 secs` |

### 安全属性

这些属性与 NiFi 中的各种安全功能相关。其中许多属性在本管理员指南[的安全配置](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#security_configuration)部分中包含更多详细内容。

| **财产**                                       | **描述**                                                     |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `nifi.sensitive.props.key`                     | 这是用于加密处理器中配置的任何敏感属性值的密码。默认情况下，它是空白的，但系统管理员应为其提供价值。它可以是任何长度的字符串，虽然建议的最小长度是 10 个字符。请注意，一旦设置此密码并配置了一个或多个敏感处理器属性，此密码就不应更改。 |
| `nifi.sensitive.props.algorithm`               | 用于加密敏感属性的算法。默认值是 。`NIFI_PBKDF2_AES_GCM_256` |
| `nifi.sensitive.props.provider`                | 敏感的属性提供商。默认值是 。`BC`                            |
| `nifi.sensitive.props.additional.keys`         | 逗号除默认敏感属性外，还分离了要加密的*nifi.属性*中的属性列表（参见[配置文件中的加密密码](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#encrypt-config_tool)）。 |
| `nifi.security.autoreload.enabled`             | 具体说明如果检测到钥匙店和信托商店的更新，是否应自动重新加载 SSL 上下文工厂。默认情况下，它被设置为 。`false` |
| `nifi.security.autoreload.interval`            | 指定检查钥匙店和信托商店以获取更新的间隔。仅适用于设置为 。默认值是 。`nifi.security.autoreload.enabled``true``10 secs` |
| `nifi.security.keystore`*                      | 钥匙店的完整路径和名称。默认情况下，它是空白的。             |
| `nifi.security.keystoreType`                   | 钥匙店类型。默认情况下，它是空白的。                         |
| `nifi.security.keystorePasswd`                 | 钥匙店密码。默认情况下，它是空白的。                         |
| `nifi.security.keyPasswd`                      | 关键密码。默认情况下，它是空白的。                           |
| `nifi.security.truststore`*                    | 信托商店的完整路径和名称。默认情况下，它是空白的。           |
| `nifi.security.truststoreType`                 | 信托商店类型。默认情况下，它是空白的。                       |
| `nifi.security.truststorePasswd`               | 信托商店密码。默认情况下，它是空白的。                       |
| `nifi.security.user.authorizer`                | 指定授权人文件中配置的*授权人.xml*文件中要使用。默认情况下，它被设置为 。`file-provider` |
| `nifi.security.allow.anonymous.authentication` | 在 HTTPS 上运行时是否允许匿名身份验证。如果设置为真实，则不需要客户证书通过 TLS 进行连接。 |
| `nifi.security.user.login.identity.provider`   | 这表示要使用哪种类型的登录身份提供商。默认值是空白的，可以设置为来自文件中指定文件中的提供商的标识符。设置此属性将触发 NiFi 以支持用户名/密码身份验证。`nifi.login.identity.provider.configuration.file` |
| `nifi.security.ocsp.responder.url`             | 这是在线证书状态协议 （OCSP） 响应器的 URL（如果正在使用）。默认情况下，它是空白的。 |
| `nifi.security.ocsp.responder.certificate`     | 如果使用 OCSP 响应者证书，则此位置。默认情况下，它是空白的。 |

### 标识映射属性

这些属性可用于使用户身份正常化。实施后，由不同身份提供者（证书、LDAP、Kerberos）认证的身份在 NiFi 内部受到相同的处理。因此，避免了重复用户，用户特定配置（如授权）只需每个用户设置一次。

以下示例演示了 Kerberos 证书和委托人对 DN 的正常化：

```
nifi.security.identity.mapping.pattern.dn=^CN=(.*?), OU=(.*?), O=(.*?), L=(.*?), ST=(.*?), C=(.*?)$
nifi.security.identity.mapping.value.dn=$1@$2
nifi.security.identity.mapping.transform.dn=NONE
nifi.security.identity.mapping.pattern.kerb=^(.*?)/instance@(.*?)$
nifi.security.identity.mapping.value.kerb=$1@$2
nifi.security.identity.mapping.transform.kerb=NONE
```

每个属性的最后一段是用于将模式与重置值关联的标识符。当用户向 NiFi 提出请求时，会检查他们的身份，看其是否与这些模式的词汇顺序相符。对于匹配的第一个，使用属性中指定的替换。因此，使用与上面的 DN 映射模式和 DN 映射值匹配的登录。用户正常化到 。`nifi.security.identity.mapping.value.xxxx``CN=localhost, OU=Apache NiFi, O=Apache, L=Santa Monica, ST=CA, C=US``$1@$2``localhost@Apache NiFi`

除了映射之外，还可以应用转换。支持的版本是（不应用转换）、（身份小写）和（身份加写）。如果不具体说明，默认值为 。`NONE``LOWER``UPPER``NONE`

|      | 这些映射还适用于"初始管理员身份"、"集群节点标识"以及*授权人文件*中的任何旧用户.xml文件以及从 LDAP 导入的用户（参见[授权人.xml设置](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#authorizers-setup)）。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

也可以映射组名。下列示例将接受现有的组名，但会降低其用例。当与外部授权人一起使用时，这可能会有所帮助。

```
nifi.security.group.mapping.pattern.anygroup=^(.*)$
nifi.security.group.mapping.value.anygroup=$1
nifi.security.group.mapping.transform.anygroup=LOWER
```

|      | 这些映射适用于*授权人*中引用的任何遗留组.xml 以及从 LDAP 进口的组。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 集群常见属性

设置 NiFi 聚类时，应在所有节点上以同样的方式配置这些属性。

| **财产**                                       | **描述**                                                     |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `nifi.cluster.protocol.heartbeat.interval`     | 节点应向群集协调员发出心跳的间隔。默认值是 。`5 sec`         |
| `nifi.cluster.protocol.heartbeat.missable.max` | 在群集协调员将节点状态更新为断开之前，群集协调员可能会错过组集节中的最大心跳数。默认值是 。`8` |
| `nifi.cluster.protocol.is.secure`              | 这表明集群通信是否安全。默认值是 。`false`                   |

### 集群节点属性

为聚类节点配置这些属性。

| **财产**                                         | **描述**                                                     |
| ------------------------------------------------ | ------------------------------------------------------------ |
| `nifi.cluster.is.node`                           | 如果实例是组中的节点，则设置为此。默认值是 。`true``false`   |
| `nifi.cluster.node.address`                      | 节点的完全合格地址。默认情况下，它是空白的。                 |
| `nifi.cluster.node.protocol.port`                | 节点的协议端口。默认情况下，它是空白的。                     |
| `nifi.cluster.node.protocol.threads`             | 应用于与组中其他节点通信的线程数。此属性默认到，但对于大型集群，此值可能需要更大。`10` |
| `nifi.cluster.node.protocol.max.threads`         | 应用于与组中的其他节点通信的最大线程数。此属性默认为 。`50`  |
| `nifi.cluster.node.event.history.size`           | 当组集中的节点状态更改时，生成事件，可在集束页面中查看。此值表示每个节点要保留多少事件。默认值是 。`25` |
| `nifi.cluster.node.connection.timeout`           | 当连接到组中的另一个节点时，指定该节点应等待多长时间，然后再考虑连接失败。默认值是 。`5 secs` |
| `nifi.cluster.node.read.timeout`                 | 当与组中的另一个节点通信时，指定该节点应等待多长时间才能从远程节点接收信息，然后再考虑与节点的通信失败。默认值是 。`5 secs` |
| `nifi.cluster.node.max.concurrent.requests`      | 可复制到组中的节点的未完成 Web 请求的最大数量。如果超出此请求数，嵌入式码头服务器将返回"409：冲突"响应。此属性默认为 。`100` |
| `nifi.cluster.firewall.file`                     | 节点防火墙文件的位置。这是一个文件，可用于列出所有允许连接到集群的节点。它提供了额外的安全层。默认情况下，此值是空白的，这意味着无需使用防火墙文件。 |
| `nifi.cluster.flow.election.max.wait.time`       | 指定在选择流为"正确"流之前等待的时间。如果已投票的节点数等于属性指定的数数，则聚类不会等待这么久。默认值是 。请注意，第一次投票一开始。`nifi.cluster.flow.election.max.candidates``5 mins` |
| `nifi.cluster.flow.election.max.candidates`      | 指定导致提前选举流量所需的节点数。这样，如果我们至少达到组集中的节点数量，则组中的节点可以避免在开始处理之前等待很长时间。 |
| `nifi.cluster.load.balance.port`                 | 指定端口以收听传入连接，以便对聚类中的负载平衡数据进行监听。默认值是 。`6342` |
| `nifi.cluster.load.balance.host`                 | 指定主机名，以收听传入的连接，以平衡整个组集的数据。如果没有指定，将默认属性所用值。`nifi.cluster.node.address` |
| `nifi.cluster.load.balance.connections.per.node` | 在此节点和组中彼此节点之间创建的最大连接数。例如，如果组组中有 5 个节点，并且此值设置为 4，则最多将设置 20 个插座连接以用于负载平衡目的（5 x 4 = 20）。默认值是 。`1` |
| `nifi.cluster.load.balance.max.thread.count`     | 用于将数据从此节点传输到组中其他节点的最大线程数。虽然给定线程一次只能写到单个插座，但单个线程能够同时为多个连接提供服务，因为给定连接可能无法在任何给定时间读取/编写。默认值是 。即，无论组中有多少节点，多达 8 个线程将负责将数据传输到其他节点。`8`**注意：**增加此值将允许用于与集群中的其他节点进行通信并将数据编写到内容和流文件存储库的其他线程。但是，如果此属性的值大于聚类中的节点数乘以每个节点的连接数（），则将不会获得进一步的好处，资源将被浪费。`nifi.cluster.load.balance.connections.per.node` |
| `nifi.cluster.load.balance.comms.timeout`        | 在与另一个节点通信时，如果在阅读或写到插座时，此时间量没有取得任何进展，则会抛出超时例外。然后，这将导致数据被重审或发送到集群中的另一个节点，具体取决于配置的负载平衡策略。默认值是 。`30 sec` |

### ZooKeeper属性

NiFi 依靠阿帕奇ZooKeeper来确定集群中的哪个节点应发挥主节点的作用，以及哪个节点应扮演群集协调员的角色。必须配置这些属性才能让 NiFi 加入集群。

| **财产**                                   | **描述**                                                     |
| ------------------------------------------ | ------------------------------------------------------------ |
| `nifi.zookeeper.connect.string`            | 连接字符串，这是需要连接到阿帕奇ZooKeeper。这是一个逗号分离的主机名列表：端口对。例如。这应该包含ZooKeeper法定人数中所有ZooKeeper实例的列表。必须指定此属性以加入集集，并且没有默认值。`localhost:2181,localhost:2182,localhost:2183` |
| `nifi.zookeeper.connect.timeout`           | 连接到ZooKeeper后要等多久才能考虑连接失败。默认值是 。`3 secs` |
| `nifi.zookeeper.session.timeout`           | 在会话到期之前，在与ZooKeeper失去连接后还要等多久。默认值是 。`3 secs` |
| `nifi.zookeeper.root.node`                 | 应该用在ZooKeeper身上的根 Znode 。ZooKeeper为存储数据提供了类似目录的结构。此结构中的每个"目录"都称为 ZNode。这表示应用于存储数据的根 ZNode 或"目录"。默认值是 。这对于正确设置非常重要，因为 NiFi 实例尝试加入的组由它连接到哪个ZooKeeper实例和指定的ZooKeeper根节点决定。`/root` |
| `nifi.zookeeper.client.secure`             | 是否使用客户 Tls 来协调ZooKeeper。                           |
| `nifi.zookeeper.security.keystore`         | 钥匙店的文件名，其中包含与ZooKeeper沟通时要使用的私人密钥。  |
| `nifi.zookeeper.security.keystoreType`     | 自选。钥匙店的类型。必须是，或.如果没有指定类型将从文件扩展中确定（， ， ， ） 。`PKCS12``JKS``PEM``.p12``.jks``.pem` |
| `nifi.zookeeper.security.keystorePasswd`   | 钥匙店的密码。                                               |
| `nifi.zookeeper.security.truststore`       | 将用于验证动物园守护者服务器的信托商店的档案名。             |
| `nifi.zookeeper.security.truststoreType`   | 自选。信托商店的类型。必须是，或.如果没有指定类型将从文件扩展中确定（， ， ， ） 。`PKCS12``JKS``PEM``.p12``.jks``.pem` |
| `nifi.zookeeper.security.truststorePasswd` | 信托商店的密码。                                             |

### 克贝罗斯属性

| **财产**                                          | **描述**                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.kerberos.krb5.file`*                        | krb5 文件的位置，如果使用的话。默认情况下，它是空白的。此时，每个 NiFi 实例只允许指定一个 krb5 文件，因此此属性在此处进行配置，以支持 SPNEGO 和服务本金，而不是在单个处理器中。如有必要，krb5 文件可以支持多个领域。例：`/etc/krb5.conf` |
| `nifi.kerberos.service.principal`*                | 如果使用，NIFI·克贝罗斯服务负责人的姓名。默认情况下，它是空白的。请注意，此属性是 NiFi 作为客户验证的其他系统。示例： 或`nifi/nifi.example.com``nifi/nifi.example.com@EXAMPLE.COM` |
| `nifi.kerberos.service.keytab.location`*          | 如果使用，NIFI·克贝罗斯钥匙塔的文件路径。默认情况下，它是空白的。请注意，此属性是 NiFi 作为客户验证的其他系统。例：`/etc/nifi.keytab` |
| `nifi.kerberos.spnego.principal`*                 | 如果使用，NIFI·克贝罗斯服务负责人的姓名。默认情况下，它是空白的。请注意，此属性用于验证 NiFi 用户。示例： 或`HTTP/nifi.example.com``HTTP/nifi.example.com@EXAMPLE.COM` |
| `nifi.kerberos.spnego.keytab.location`*           | 如果使用，NIFI·克贝罗斯钥匙塔的文件路径。默认情况下，它是空白的。请注意，此属性用于验证 NiFi 用户。例：`/etc/http-nifi.keytab` |
| `nifi.kerberos.spengo.authentication.expiration`* | 如果使用，则成功 Kerberos 用户身份验证的有效期。默认值是 。`12 hours` |

### 分析属性

这些属性决定了内部 NiFi 预测分析能力（如背压预测）的行为，并且应以相同的方式在所有节点上进行配置。

| **财产**                                          | **描述**                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| `nifi.analytics.predict.enabled`                  | 这表明是否应启用对聚类进行预测。默认值是 。`false`           |
| `nifi.analytics.predict.interval`                 | 应进行分析预测（例如队列饱和）的时间间隔。默认值是 。`3 mins` |
| `nifi.analytics.query.interval`                   | 查询过去观测的时间间隔（例如最后 3 分钟的快照）。默认值是 。注：此值应至少比确保检索到足够的观测结果以进行预测大 3 倍。`5 mins``nifi.components.status.snapshot.frequency` |
| `nifi.analytics.connection.model.implementation`  | 用于进行连接预测的状态分析模型的实现类。默认值是 。`org.apache.nifi.controller.status.analytics.models.OrdinaryLeastSquares` |
| `nifi.analytics.connection.model.score.name`      | 应用于评估模型的评分类型名称。默认值是 。`rSquared`          |
| `nifi.analytics.connection.model.score.threshold` | 评分值的阈值（模型分数应高于给定阈值）。默认值是 。`.90`     |

### 运行时间监控属性

长期运行的任务监视器定期检查 NiFi 处理器执行器线程，并为运行时间较长的人员生成警告日志和公告消息。它可用于检测可能卡住 / 悬挂处理器的任务。请注意任务监视器的性能影响：它为可能影响正常流执行的每次运行创建一个线程转储。通过定义其属性的不值，可以禁用长期运行任务监视器，并且默认禁用该监视器。要启用它，需要用有效的时间段来配置它和属性。`nifi.monitor.long.running.task.schedule``nifi.monitor.long.running.task.threshold`

| **财产**                                   | **描述**                                                     |
| ------------------------------------------ | ------------------------------------------------------------ |
| `nifi.monitor.long.running.task.schedule`  | 连续执行长期任务监视器（例如）之间的时间段。`1 min`          |
| `nifi.monitor.long.running.task.threshold` | 任务超出的时间段被视为长期运行，即卡住/悬挂（例如）。`5 mins` |

### 自定义属性

要配置自定义属性，以便使用 NiFi 的表达语言：

- 创建自定义属性。确保：
  - 每个自定义属性都包含不同的属性值，因此它不会被现有环境属性、系统属性或 FlowFile 属性覆盖。
  - 聚类环境中的每个节点都配置相同的自定义属性。
- 随自定义属性文件的位置进行更新：`nifi.variable.registry.properties`

| **财产**                            | **描述**                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| `nifi.variable.registry.properties` | 这是一个组合分离的文件位置路径列表，用于一个或多个自定义属性文件。 |

- 重新启动您的 NiFi 实例，以便获取更新。

自定义属性也可以在 NiFi UI 中配置。有关更多信息，请参阅用户指南中的["变量窗口](http://nifi.apache.org/docs/nifi-docs/html/user-guide.html#Variables_Window)"部分。

## 升级NIFI

下面的说明是从 1.x.0 版本升级到另一个版本时需要遵循的一般步骤。

在升级之前，您应仔细查看["发布说明"，](https://cwiki.apache.org/confluence/display/NIFI/Release+Notes)以确保您了解新版本中所做的更改及其对现有数据流和/或环境的影响。此外，请检查[迁移指导](https://cwiki.apache.org/confluence/display/NIFI/Migration+Guidance)页面，了解在特定 NiFi 版本之间移动时应注意的项目。

|      | 组集中的所有节点必须升级到相同的 NiFi 版本，因为不同 NiFi 版本的节点不在同一组群中支持。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 保留自定义处理器

如果您有任何自定义的 NAR，请在升级期间将其存储在集中位置，具体如下：

1. 创建第二个库目录，称为 。`custom_lib`

2. 将您的自定义 NAR 移动到此新的 lib 目录。

3. 在*nifi. 属性*文件中添加一条新行， 以指定此新的 lib 目录：

   ```
   nifi.nar.library.directory=./lib
   nifi.nar.library.directory.custom=/opt/configuration_resources/custom_lib
   ```

### 保留修改后的 NAR

如果您已修改任何默认 NAR 文件，升级将覆盖这些更改。保留以下定制内容：

1. 识别并保存您对默认 NAR 文件所做的更改。
2. 执行您的 NiFi 升级。
3. 在新的 NiFi 实例中实现相同的 NAR 文件更改。

### 清除活动和关闭现有 NiFi

在您现有的 NiFi 安装上：

1. 停止所有源处理器以防止新数据的摄入。
2. 允许 NiFi 运行，直到数据流中的任何队列中没有活动数据。
3. 关闭您现有的 NiFi 实例。

### 安装新的 NiFi 版本

将新 NiFi 安装到与现有 NiFi 安装平行的目录中。

1. 下载[最新版本](https://nifi.apache.org/download.html)的阿帕奇NIFI。

2. 将 NiFi *.tar*文件（）解压缩为与现有 NiFi 目录平行的目录。例如，如果您的现有 NiFi 安装已安装，请在 。`tar -xvzf file-name``/opt/nifi/existing-nifi/``/opt/nifi/new-nifi/`

3. 如果要升级 NiFi 聚类，请在组集的每个节点上重复这些步骤。

   ```
   Host Machine - Node 1
   |--> opt/
      |--> existing-nifi
      |--> new-nifi
   ```

   ```
   Host Machine - Node 2|--> opt/   |--> existing-nifi   |--> new-nifi
   ```

   ```
   Host Machine - Node 3|--> opt/   |--> existing-nifi   |--> new-nifi
   ```

|      | 确保新 NiFi 目录的所有文件和目录所有权与您在现有目录上设置的内容相匹配。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

### 更新新 NiFi 安装的配置文件

使用现有 NiFi 安装中的配置文件手动更新新 NiFi 部署中的相应属性。

|      | 一般来说，不要将配置文件从现有的 NiFi 版本复制到新的 NiFi 版本。较新的配置文件可能会引入新的属性，如果您复制和粘贴配置文件，这些属性将丢失。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

使用以下表来指导位于 。`<installation-directory>/conf`

| 配置文件                                                     | 必要的更改                                                   |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| *授权人.xml*                                                 | 将现有授权机构中的配置复制到新的 NiFi 文件*.xml。*`<authorizer>…</authorizer>`如果您正在使用授权人，请确保将*用户.xml*和*授权.xml*文件从现有文件复制到新的 NiFi。`file-provider`配置最佳实践建议在 NiFi 基础目录之外创建一个单独的位置来存储此类配置文件，例如： .如果您将这些文件存储在单独的目录中，则不需要移动它们。相反，确保新的 NiFi 指向相同的文件。`/opt/nifi/configuration-resources/` |
| *引导通知服务.xml*                                           | 使用现有的 NiFi*引导通知服务.xml*文件更新新 NiFi 中的属性。  |
| *引导. 康夫*                                                 | 使用现有的 NiFi*引导. conf*文件来更新新 NiFi 中的属性。      |
| *流.xml.gz*                                                  | 如果您保留了存储流（）、副本*流的*默认位置.xml.gz从现有到新的 NiFi 基础安装目录。如果您通过*nifi.属性*存储流到外部位置，请更新该属性指向该位置。`<installation-directory>/conf/``conf``nifi.flow.configuration.file`如果您正在通过*nifi.*属性中的敏感属性密钥加密数据流中的敏感组件属性，请确保在流量中复制时使用相同的密钥*.xml.gz。*如果您需要更改密钥，请参阅下面[的"用敏感属性迁移流量](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#sensitive_flow_migration)"部分。 |
| *NIFI. 属性*                                                 | 使用现有的*nifi.属性在新的 NiFi*文件中填充相同的属性。**注意：**此文件包含大多数 NiFi 配置设置，因此请确保正确复制了值。 |
| 如果您遵循 NiFi 最佳实践，以下属性应指向基础 NiFi 安装路径外的外部目录。如果下面的属性指向 NiFi 基础安装路径内的目录，则必须将目标目录复制到新的 NiFi。在此之前，请停止现有的 NiFi 安装。 |                                                              |
| `nifi.flow.configuration.file=`如果您保留了默认值（），复制*流.xml.gz*从现有到新的 NiFi 基座安装联盟目录。`./conf/flow.xml.gz`如果存储流到外部位置，请更新属性值以指向该位置。 |                                                              |
| `nifi.flow.configuration.archive.dir=`如果您想要保留存档的流量副本，则与上述情况相同*.xml.gz。* |                                                              |
| `nifi.database.directory=`最佳实践建议您为每个存储库使用外部位置。将新 NiFi 指向同一外部数据库存储库位置。 |                                                              |
| `nifi.flowfile.repository.directory=`最佳实践建议您为每个存储库使用外部位置。将新 NiFi 指向同一外部流档存储库位置。**警告：**如果新 NiFi 无法访问流文件存储库，则可能会遇到数据丢失。 |                                                              |
| `nifi.content.repository.directory.default=`最佳实践建议您为每个存储库使用外部位置。将新 NiFi 指向同一外部内容存储库位置。您现有的 NiFi 可能定义了多个内容存储库。确保使用完全相同的属性名称，并指向相应的匹配内容回购位置。例如：`nifi.content.repository.directory.content1=` `nifi.content.repository.directory.content2=`**警告：**如果新 NiFi 无法访问内容库，则可能会遇到数据丢失。**警告：**如果属性名称错误或属性指向错误的内容存储库，则可能会遇到数据丢失。 |                                                              |
| `nifi.provenance.repository.directory.default=`最佳实践建议您为每个存储库使用外部位置。将新 NiFi 指向同一外部来源存储库位置。您现有的 NiFi 可能定义了多个内容存储库。确保使用完全相同的属性名称，并指向相应的匹配来源回购位置。例如：`nifi.provenance.repository.directory.provenance1=` `nifi.provenance.repository.directory.provenance2=`**注意：**如果来源存储未正确移动或属性未正确更新，则可能无法查询旧事件。 |                                                              |
| *国家管理.xml*                                               | 对于状态提供商，请验证本地目录的位置。`local-provider`如果您保留了默认位置（），请将完整目录树复制到新的 NiFi。如果您要复制此目录，则应停止现有的 NiFi，因为它可能会在运行时不断写入此目录。`./state/local`配置最佳实践建议您将状态移动到外部目录，以便以后更容易升级。`/opt/nifi/configuration-resources/` |
| 对于 NiFi 集群，ZooKeeper的"连接字符串"属性应设置为与现有 NiFi 安装相同的外部ZooKeeper。`cluster-provider` |                                                              |
| 对于 NiFi 集群，请确保ZooKeeper的"根节点"属性与现有 NiFi 中使用的值完全匹配。`cluster-provider` |                                                              |
| 如果您还设置了新的外部ZooKeeper，请参阅[ZooKeeper迁移器](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#zookeeper_migrator)部分，了解如何将ZooKeeper信息从一个集群移动到另一个集群并迁移ZooKeeper节点所有权的说明。 |                                                              |

|      | 仔细检查拼写错误的所有配置属性。 |
| ---- | -------------------------------- |
|      |                                  |

#### 迁移具有敏感属性的流量

当在*nifi.属性*中设置值时，指定的密钥用于加密流中的敏感属性（例如组件中的密码字段）。如果密钥需要更改，NiFi 工具包中的加密配置工具可以迁移敏感属性密钥并更新*流量.xml.gz。*具体来说，加密配置：`nifi.sensitive.props.key`

1. 读取现有*流量.xml.gz*并使用当前密钥解密敏感值。
2. 用指定的新密钥加密所有敏感值。
3. 更新*nifi.属性*和*流.xml.gz*文件或创建新版本的文件。

例如，假设版本 1.9.2 是现有的 NiFi 实例，并且将敏感属性键设置为 。目标是将 1.9.2*流量.xml.gz*移动到 1.10.0 实例，并具有新的敏感属性密钥： .运行以下加密配置命令将使用原始敏感属性键从 1.9.2 中读取*流.xml.gz*和*nifi.属性*文件，并在 1.10.0 中用新密码加密的敏感属性编写新版本：`password``new_password`

```
$ ./nifi-toolkit-1.10.0/bin/encrypt-config.sh -f /path/to/nifi/nifi-1.9.2/conf/flow.xml.gz -g /path/to/nifi/nifi-1.10.0/conf/flow.xml.gz -s new_password -n /path/to/nifi/nifi-1.9.2/conf/nifi.properties -o /path/to/nifi/nifi-1.10.0/conf/nifi.properties -x
```

哪里：

- `-f`指定源*流.xml.gz* （nifi-1.9.2）
- `-g`指定目的地*流量.xml.gz* （nifi-1.10.0）
- `-s`指定新的敏感属性键 （`new_password`)
- `-n`指定源*nifi.属性*（nifi-1.9.2）
- `-o`指定目的地*nifi.属性*（nifi-1.10.0）
- `-x`告诉加密配置只处理敏感属性

有关更多信息，请参阅 NiFi 工具包指南中的[加密配置](http://nifi.apache.org/docs/nifi-docs/html/toolkit-guide.html#encrypt_config_tool)工具部分。

#### 更新敏感属性密钥

从版本 1.14.0 开始，NiFi 要求在*nifi.属性*中具有"nifi.敏感.props.props.key"值。

以下命令可用于读取现有*流.xml.gz配置，*并在*nifi. 属性*中设置新的敏感属性密钥：

```
$ ./bin/nifi.sh set-sensitive-properties-key <sensitivePropertiesKey>
```

新敏感属性键的最小要求长度为 12 个字符。

### 开始新NIFI

在您的新 NiFi 安装中：

1. 开始您的每个新的 NiFi 实例。
2. 验证：
   - 您的所有数据流已恢复到运行状态。某些处理器可能具有需要配置的新属性，在这种情况下，它们将被停止并标记为无效 （![Invalid](https://cdn.jsdelivr.net/gh/zshipu/images/202111011350246.png)).
   - 所有预期的控制器服务和报告任务都再次运行。解决任何标记为无效的控制器服务或报告任务 （![Invalid](https://cdn.jsdelivr.net/gh/zshipu/images/202111011350568.png)).
3. 确认您的新 NiFi 实例稳定且按预期工作后，可以删除旧的安装。

|      | 如果设置原始 NiFi 作为服务运行，请更新任何符号链接或服务脚本，指向新的 NiFi 版本可执行执行项。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

## 处理器位置

### 可用配置选项

NiFi 为处理器位置提供 3 个配置选项。即：

```
nifi.nar.library.directory
nifi.nar.library.directory.<custom>
nifi.nar.library.autoload.directory
```

|      | 使用这些选项设置的路径相对于 NiFi 家庭目录。例如，如果NiFi家庭目录是，而图书馆名录是，那么最终的路径是。`/var/lib/nifi``./lib``/var/lib/nifi/lib` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

该处理器用于提供 NiFi 处理器的默认位置。不建议将此用于自定义处理器，因为这些处理器可能会在 NiFi 升级过程中丢失。例如：`nifi.nar.library.directory`

```
nifi.nar.library.directory=./lib
```

允许管理员为 NiFi 提供多个树基路径来定位自定义处理器。每个唯一路径必须附加唯一属性标识符。例如：`nifi.nar.library.directory.<custom>`

```
nifi.nar.library.directory.myCustomLibs=./my-custom-nars/libnifi.nar.library.directory.otherCustomLibs=./other-custom-nars/lib
```

该功能由自动加载功能使用，NiFi 可以自动加载添加到配置路径的新处理器，而无需重新启动。例如：`nifi.nar.library.autoload.directory`

```
nifi.nar.library.autoload.directory=./autoload/lib
```

### 安装自定义处理器

本节描述了安装需要重新启动到 NiFi 的自定义处理器的原始过程。要使用自动加载功能，请参阅下面的[自动加载自定义处理器](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#autoloading-processors)部分。

首先，我们将为自定义处理器配置目录。有关这些[配置选项](http://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#processor-location-options)的更多信息，请参阅可用配置选项。

```
nifi.nar.library.directory.myCustomLibs=./my-custom-nars/lib
```

确保此目录存在，并且对 nifi 用户和组具有适当的权限。

现在，我们必须将我们的自定义处理器纳在配置的目录中。配置的目录相对于 NiFi 家庭目录：例如，让我们说，我们的NiFi家庭迪尔是，我们会把我们的定制处理器纳。`/var/lib/nifi``/var/lib/nifi/my-custom-nars/lib`

确保文件具有对 nifi 用户和组的适当权限。

重新启动 NiFi 和自定义处理器现在应在向您的流量添加新处理器时可用。

### 自动加载自定义处理器

本节描述了自定义处理器使用自动加载功能的过程。

要使用自动加载功能，必须配置该属性以指向所需的目录。默认情况下，此点为 。`nifi.nar.library.autoload.directory``./extensions`

例如：

```
nifi.nar.library.autoload.directory=./extensions
```

确保此目录存在，并且对 nifi 用户和组具有适当的权限。

现在，我们必须将我们的自定义处理器纳在配置的目录中。配置的目录相对于 NiFi 家庭目录：例如，让我们说，我们的NiFi家庭迪尔是，我们会把我们的定制处理器纳。`/var/lib/nifi``/var/lib/nifi/extensions`

确保文件具有对 nifi 用户和组的适当权限。

刷新浏览器页面，当在流量中添加新的处理器时，应提供自定义处理器。

### NAR 提供商

NiFi 支持从外部获取自动加载功能的 NAR 文件。这可以通过使用 NAR 提供商来实现。NAR 提供商充当外部数据存储和 NiFi 之间的连接器。

配置后，NAR 提供商会对可用 NAR 文件的外部源进行投票，并将它们提供给框架。然后，该框架获取新的 NAR 文件，并将它们复制到自动加载中。`nifi.nar.library.autoload.directory`

NAR 提供商可以通过添加包含适当实施类值的属性进行配置。某些实现可能需要进一步属性。这些是由实施定义，必须前缀。`nifi.nar.library.provider.<providerName>.implementation``nifi.nar.library.provider.<providerName>.`

这是任意的，并用于将多个属性关联在一起的单个提供商。多个提供商可能设置，具有不同的。目前，NiFi 支持基于 HDFS 的 NAR 提供商。`<providerName>``<providerName>`

#### HDFS NAR 提供商

此实现能够从 HDFS 文件系统下载 NAR 文件。

其价值必须是。供应商定义了以下其他属性：`nifi.nar.library.provider.<providerName>.implementation``org.apache.nifi.nar.hadoop.HDFSNarProvider`

| 名字             | 描述                                                       |
| :--------------- | :--------------------------------------------------------- |
| 资源             | HDFS 资源列表，按逗号分隔。                                |
| 来源.目录        | HDFS 内 NAR 文件的源目录。注意：提供商不会反复检查文件。   |
| 存储.位置        | 自选。如果设置在核心站点中定义的存储位置.xml将被此值覆盖。 |
| 克贝罗斯. 校长   | 自选。克贝罗斯校长认证为.                                  |
| 克贝罗斯. 基塔布 | 自选。与本金相关的克贝罗斯钥匙塔。                         |
| 克贝罗斯. 密码   | 自选。与本金相关的克贝罗斯密码。                           |

示例配置：

```
nifi.nar.library.provider.hdfs1.implementation=org.apache.nifi.nar.hadoop.HDFSNarProvider
nifi.nar.library.provider.hdfs1.resources=/etc/hadoop/core-site.xml
nifi.nar.library.provider.hdfs1.source.directory=/customNars
nifi.nar.library.provider.hdfs2.implementation=org.apache.nifi.nar.hadoop.HDFSNarProvider
nifi.nar.library.provider.hdfs2.resources=/etc/hadoop/core-site.xml
nifi.nar.library.provider.hdfs2.source.directory=/other/dir/for/customNars
```

