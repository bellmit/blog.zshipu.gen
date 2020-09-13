title: dart await和async
author: 知识铺
date: 2020-09-13 13:53:36
tags:
---

# await和async

[参考这里](https://juejin.im/post/5d7f5e7c6fb9a06b0c089920) 

`await和async`可以让我们用`同步的代码格式`，去实现`异步的调用过程` , 通常一个async的函数会返回一个Future  

Future可以做到不阻塞我们的线程，让线程继续执行，并且在完成某个操作时改变自己的状态，并且回调then或者errorCatch回调。通过async的函数可以方便的生成Future对象  

```
// 需要注意:
// 1. await关键字必须存在于async函数中, `await` can only be used in `async` or `async*` methods.
// 2. 使用async标记的函数，必须返回一个Future对象
// 也就是说: 方法使用async修饰, 内部使用await同步, 返回Future对象
Future getNetworkData() async {
  var result = await Future.delayed(Duration(seconds: 3), () {
    return "net work data";
  });
  return "请求到的数据: " + result;
}

void test() {
  print("main function start");
  print(getNetworkData().then((value) {
    print(value);
  }));
  print("main function end");
}
```

输出:  

```
main function start
Instance of 'Future<Null>'
main function end
请求到的数据: net work data
```

### 读取json案例  

```json
[
    {
        "nick_name": "小明",
        "room_name": "101",
        "image_url": "http://www.xxx.yyy/12.png"
    }, 
    {
        "nick_name": "小红",
        "room_name": "102",
        "image_url": "http://www.wer.yyy/123.png"
    }, 
    {
        "nick_name": "小张",
        "room_name": "103",
        "image_url": "http://www.wer.yyy/123.png"
    }
]
```

```
import 'dart:convert';

import 'package:flutter/services.dart';

class Anchor {
  String nickName;
  String roomName;
  String imgUrl;

  Anchor({this.nickName, this.roomName, this.imgUrl});
  // Anchor(this.nickName, this.roomName, this.imgUrl);

  Anchor.fromMap(Map<String, dynamic> parsedMap) {
    this.nickName = parsedMap['nick_name'];
    this.roomName = parsedMap['room_name'];
    this.imgUrl = parsedMap['image_url'];
  }

  static Future<List<Anchor>> getAnchors() async {
    // 1.读取json文件
    // 注意Flutter中导入资源需要做一些配置: https://blog.csdn.net/nicolelili1/article/details/90577241
    String jsonString = await rootBundle.loadString("resource/anchors.json");
    print(jsonString);
    final jsonResult = json.decode(jsonString);
    List<Anchor> anchors = new List();
    for (Map<String, dynamic> map in jsonResult) {
      anchors.add(Anchor.fromMap(map));
    }
    return anchors;
  }
}

void test() {
  Anchor.getAnchors().then((value) {
    for (Anchor anchor in value) {
      print("${anchor.nickName}");
    }
  });
}
```

