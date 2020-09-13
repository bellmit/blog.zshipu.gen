
title: 在 Flutter 项目中使用 MQTT
author: 知识铺
date: 2020-09-13 18:27:58
tags: flutter
---
  

# 在 Flutter 项目中使用 MQTT

2020-07-20

 [MQTT 客户端 SDK](https://zshipu.com/t?url=/blog/category/mqtt-client-sdk)

[Flutter](https://zshipu.com/t?url=https://flutter.dev/)是 Google 的 UI 工具包，用于从单个代码库构建美观、本地编译的移动、Web 和桌面应用程序。Flutter 提供了一组丰富的组件和接口，开发人员可以快速为 Flutter 添加本机扩展。同时，Flutter 还使用本机引擎来呈现视图。毫无疑问，它可以为用户提供良好的体验。

[MQTT](https://zshipu.com/t?url=https://www.emqx.io/mqtt)是基于**发布/订阅模型的轻量级 IoT**通信协议。它可以在严格限制的设备硬件和高延迟/低带宽网络上实现稳定的传输。由于它简单易用，支持QoS，并且数据包体积小，它占据了物联网协议的一半市场。

本文主要介绍如何在 Flutter 项目中使用 MQTT 实现客户端与 MQTT 代理之间的连接、订阅、取消订阅、发送和接收消息等功能。

## 项目初始化

### 创建项目

创建新项目，可参考以下链接：

*   [设置编辑器](https://zshipu.com/t?url=https://flutter.dev/docs/get-started/editor?tab=androidstudio)
*   [安卓工作室和 IntelliJ](https://zshipu.com/t?url=https://flutter.dev/docs/development/tools/android-studio)

### 安装依赖项

<font _mstmutation="1" _msthash="1169727" _msttexthash="37287419">将依赖项添加到文件中</font>```pubspec.yaml```

 dependencies: 
  mqtt_client: ^7.2.1

安装依赖项：

 flutter pub get

进口

 import 'package:mqtt_client/mqtt_client.dart';

## 使用 MQTT

### 连接到 MQTT 代理

本文将使用由[EMQ X云](https://zshipu.com/t?url=https://www.emqx.io/products/broker)操作和维护的MQTT代理。EMQ X云是[EMQ发布的MQTT物联网](https://zshipu.com/t?url=https://cloud.emqx.io/)[云服务平台](https://zshipu.com/t?url=https://www.emqx.io/)，它通过一对一的运行和维护以及独特的隔离环境，为访问**MQTT 5.0**提供服务。

*   经纪人： **broker.emqx.io**
*   TCP 端口： **1883**
*   网络搜索端口： **8083**

#### 连接示例

 Future<MqttServerClient> connect() async {
  MqttServerClient client =
      MqttServerClient.withPort('broker.emqx.io', 'flutter_client', 1883);
  client.logging(on: true);
  client.onConnected = onConnected;
  client.onDisconnected = onDisconnected;
  client.onUnsubscribed = onUnsubscribed;
  client.onSubscribed = onSubscribed;
  client.onSubscribeFail = onSubscribeFail;
  client.pongCallback = pong;

  final connMessage = MqttConnectMessage()
      .authenticateAs('username', 'password')
      .keepAliveFor(60)
      .withWillTopic('willtopic')
      .withWillMessage('Will message')
      .startClean()
      .withWillQos(MqttQos.atLeastOnce);
  client.connectionMessage = connMessage;
  try {
    await client.connect();
  } catch (e) {
    print('Exception: $e');
    client.disconnect();
  }

  client.updates.listen((List<MqttReceivedMessage<MqttMessage>> c) {
    final MqttPublishMessage message = c[0].payload;
    final payload =
    MqttPublishPayload.bytesToStringAsString(message.payload.message);

    print('Received message:$payload from topic: ${c[0].topic}>');
  });

  return client;
}

#### 回调方法的描述

 // connection succeeded
void onConnected() {
  print('Connected');
}

// unconnected
void onDisconnected() {
  print('Disconnected');
}

// subscribe to topic succeeded
void onSubscribed(String topic) {
  print('Subscribed topic: $topic');
}

// subscribe to topic failed
void onSubscribeFail(String topic) {
  print('Failed to subscribe $topic');
}

// unsubscribe succeeded
void onUnsubscribed(String topic) {
  print('Unsubscribed topic: $topic');
}

// PING response received
void pong() {
  print('Ping response client callback invoked');
}

```MqttConnectMessage```<font _mstmutation="1" _msthash="1172769" _msttexthash="212272489">：设置连接选项，包括超时设置、身份验证、最后愿望消息等。</font>

```client.updates.listen```<font _mstmutation="1" _msthash="1173380" _msttexthash="76790597">：用于监视订阅主题的消息到达</font>

#### 证书连接示例

 /// Security context
SecurityContext context = new SecurityContext()
  ..useCertificateChain('path/to/my_cert.pem')
  ..usePrivateKey('path/to/my_key.pem', password: 'key_password')
  ..setClientAuthorities('path/to/client.crt', password: 'password');
client.secure = true;
client.securityContext = context;

### 其他 MQTT 操作

#### 订阅主题

 client.subscribe("topic/test", MqttQos.atLeastOnce)

#### 发布消息

 const pubTopic = 'topic/test';
final builder = MqttClientPayloadBuilder();
builder.addString('Hello MQTT');
client.publishMessage(pubTopic, MqttQos.atLeastOnce, builder.payload);

#### 取消 订阅

 client.unsubscribe('topic/test');

#### 断开

 client.disconnect();

## 测试

我们为这个项目编写一个简单的 UI 接口，并使用[MQTT 5.0 客户端工具 - MQTT X](https://zshipu.com/t?url=https://mqttx.app/cn/)执行以下测试：

*   连接

*   订阅

*   发布

*   取消 订阅

*   断开

应用程序的接口：

![画板1x.png](https://static.emqx.net/images/4aeb38a0dc6b0329164a91fc38e572cc.png)

使用 MQTT X 作为另一个客户端发送和接收消息：

![mqttx_flutter.png](https://static.emqx.net/images/b46731e7278ad148a0bfe3cc0890138b.png)

我们可以看到整个过程的日志

![log.png](https://static.emqx.net/images/97230919d8c8eddd3c88003e67c9ad1b.png)

## 总结

到目前为止，我们已经完成了使用 Flutter 在 Android 平台中构建 MQTT 应用程序，实现客户端和 MQTT 代理之间的连接，订阅、取消订阅、发布和接收消息等。

通过统一编程语言和功能跨平台，Flutter 使开发强大的移动应用程序变得容易。这可能是未来开发移动应用程序的最恰当解决方案。使用 Flutter、MQTT 协议[和 MQTT 云](https://zshipu.com/t?url=https://cloud.emqx.io/)服务，我们可以开发更有趣的应用程序。
