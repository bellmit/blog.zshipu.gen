---
categories:
- flutter
tags:
- flutter,flutter技术
keywords: 知识铺,flutter
date: 2020-09-13T14:14:04+08:00
title: flutter 初起步： Run Mode
author: 知识铺
weight: -1
---

# Run Mode

可以设置App的Run Mode, 有Debug, Release, Profile三种方式  

在Android Studio上: 

Run > Debug | Release | Profile

也可以:  

Run > Edit Configuration > 在Additional arguments中添加 `--debug`或`--release`或`--profile`

----------------------------

在VS Code上可以:  
打开 launch.json 文件并设置flutterMode 为 profile: 

```
"configurations": [
    {
        "name": "Flutter",
        "request": "launch",
        "type": "dart",
        "flutterMode": "profile" # 测试完后记得把它改回去！
    }
]
```

----------------------------

也可以用命令启动:  

```
flutter run --profile //开发运行的app不卡顿
flutter run --release //开发运行的app卡顿
```

----------------------------
注: Release mode is not supported for emulators. Release模式不支持模拟器

