---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： ListView
author: 知识铺
weight: -1
---

# ListView

列表展示, 类似于UITableView

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      color: Colors.white,
      home: Scaffold(
        appBar: AppBar(
          title: Text("Title"),
        ),
        body: MyHomePage(),
      )
    );
  }
}

class MyHomePage extends StatelessWidget {
  final TextStyle textStyle = TextStyle(
    fontSize: 20,
    color: Colors.green,
  );

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: Text("人的一切痛苦，本质上都是对自己无能的愤怒。", style: textStyle),
        ),
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: Text("人活在世界上，不可以有偏差；而且多少要费点劲儿，才能把自己保持到理性的轨道上。", style: textStyle),
        ),
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: Text("我活在世上，无非想要明白些道理，遇见些有趣的事。", style: textStyle),
        )
      ],
    );
  }
}
```

### ListTile

相当于UITableViewCell, 有一个图标或图片（Icon），有一个标题（Title），有一个子标题（Subtitle），还有尾部一个图标（Icon）  

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      color: Colors.white,
      home: Scaffold(
        appBar: AppBar(
          title: Text("Title"),
        ),
        body: MyHomePage(),
      )
    );
  }
}

class MyHomePage extends StatelessWidget {
  final TextStyle textStyle = TextStyle(
    fontSize: 20,
    color: Colors.green,
  );

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        ListTile(
          leading: Icon(Icons.people, size: 36,),
          title: Text("联系人"),
          subtitle: Text("联系人信息"),
          trailing: Icon(Icons.arrow_forward_ios),
        ),
        ListTile(
          leading: Icon(Icons.email, size: 36,),
          title: Text("邮箱"),
          subtitle: Text("邮箱地址信息"),
          trailing: Icon(Icons.arrow_forward_ios),
        ),
        ListTile(
          leading: Icon(Icons.message, size: 36,),
          title: Text("消息"),
          subtitle: Text("消息详情信息"),
          trailing: Icon(Icons.arrow_forward_ios),
        ),
        ListTile(
          leading: Icon(Icons.map, size: 36,),
          title: Text("地址"),
          subtitle: Text("地址详情信息"),
          trailing: Icon(Icons.arrow_forward_ios),
        )
      ],
    );
  }
}
```

### 水平方向滚动 

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      color: Colors.white,
      home: Scaffold(
        appBar: AppBar(
          title: Text("Title"),
        ),
        body: MyHomePage(),
      )
    );
  }
}

class MyHomePage extends StatelessWidget {
  final TextStyle textStyle = TextStyle(
    fontSize: 20,
    color: Colors.green,
  );

  @override
  Widget build(BuildContext context) {
    return ListView(
      scrollDirection: Axis.horizontal,
      itemExtent: 200, // 宽度
      children: <Widget>[
        Container(color: Colors.red),
        Container(color: Colors.green),
        Container(color: Colors.blue, width: 300), // 以itemExtent为限制大小, 仍然是200
        Container(color: Colors.purple, width: 200),
        Container(color: Colors.orange, width: 200),
      ],
    );
  }
}
```

### ListView.builder 提高性能 
通过构造函数中的children传入所有的子Widget有一个问题：默认会创建出所有的子Widget。
但是对于用户来说，一次性构建出所有的Widget并不会有什么差异，但是对于我们的程序来说会产生性能问题，而且会增加首屏的渲染时间。
我们可以使用ListView.build来构建子Widget，提高性能   

重要参数:  

- itemBuilder：列表项创建的方法。当列表滚动到对应位置的时候，ListView会自动调用该方法来创建对应的子Widget。类型是IndexedWidgetBuilder，是一个函数类型
- itemCount：表示列表项的数量，如果为空，则表示ListView为无限列表  

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      color: Colors.white,
      home: Scaffold(
        appBar: AppBar(
          title: Text("Title"),
        ),
        body: MyHomePage(),
      )
    );
  }
}

class MyHomePage extends StatelessWidget {
  final TextStyle textStyle = TextStyle(
    fontSize: 20,
    color: Colors.green,
  );

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: 60,
      itemExtent: 64.0,
      itemBuilder: (BuildContext context, int index) {
          return ListTile(
            title: Text("标题$index"),
            subtitle: Text("详情内容$index"),
          );
      },
    );
  }
}
```

### ListView.builder 加载动态数据  

```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:hello/Anchor.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      color: Colors.white,
      home: Scaffold(
        appBar: AppBar(
          title: Text("Title"),
        ),
        body: MyHomePage(),
      )
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return MyHomePageState();
  }
}

class MyHomePageState extends State<MyHomePage> {
  List<Anchor> anchors = [];

  // 在初始化状态的方法中加载数据
  @override
  void initState() {

    getAnchors().then((anchors) {
      setState(() {
        this.anchors = anchors;
      });
    });

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: this.anchors.length,
      itemBuilder: (BuildContext context, int index) {
        return Padding(
          padding: EdgeInsets.all(8),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start, // 左对齐
            children: <Widget>[
              Image.network(
                anchors[index].imageUrl,
                fit: BoxFit.fitWidth,
                width: MediaQuery.of(context).size.width,
              ),
              SizedBox(height: 8,),
              Text(anchors[index].nickName, style: TextStyle(fontSize: 20),),
              SizedBox(height: 5,),
              Text(anchors[index].roomName),
            ],
          ),
        );
      },
    );
  }

  Future<List<Anchor>> getAnchors() async {
    String jsonString = await rootBundle.loadString("resources/json/json.txt");
    final jsonResult = json.decode(jsonString);
    List<Anchor> anchors = new List();
    for (Map<String, dynamic> map in jsonResult) {
      anchors.add(Anchor.withMap(map));
    }
    print("------------> ${anchors.length}");
    return anchors;
  }
}
```

### ListView.separated 分割线  

```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:hello/Anchor.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      color: Colors.white,
      home: Scaffold(
        appBar: AppBar(
          title: Text("Title"),
        ),
        body: MyHomePage(),
      )
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return MyHomePageState();
  }
}

class MyHomePageState extends State<MyHomePage> {
  List<Anchor> anchors = [];

  // 在初始化状态的方法中加载数据
  @override
  void initState() {

    getAnchors().then((anchors) {
      setState(() {
        this.anchors = anchors;
      });
    });

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return ListView.separated(
      separatorBuilder: (BuildContext context, int index) {
        // return index % 2 == 0 ? Divider(color: Colors.red) : Divider(color: Colors.green);
        return index % 2 == 0 ? Icon(Icons.arrow_drop_down) : Icon(Icons.arrow_downward);
      },
      itemCount: this.anchors.length,
      itemBuilder: (BuildContext context, int index) {
        return Padding(
          padding: EdgeInsets.all(8),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: <Widget>[
              Image.network(
                anchors[index].imageUrl,
                fit: BoxFit.fitWidth,
                width: MediaQuery.of(context).size.width,
              ),
              SizedBox(height: 8,),
              Text(anchors[index].nickName, style: TextStyle(fontSize: 20),),
              SizedBox(height: 5,),
              Text(anchors[index].roomName),
            ],
          ),
        );
      },
    );
  }

  Future<List<Anchor>> getAnchors() async {
    String jsonString = await rootBundle.loadString("resources/json/json.txt");
    final jsonResult = json.decode(jsonString);
    List<Anchor> anchors = new List();
    for (Map<String, dynamic> map in jsonResult) {
      anchors.add(Anchor.withMap(map));
    }
    print("------------> ${anchors.length}");
    return anchors;
  }
}
```

