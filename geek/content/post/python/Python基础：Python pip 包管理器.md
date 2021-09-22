
---
title: Python基础：Python pip 包管理器
author: 知识铺
date: 2020-10-25 19:49:50+08:00
tags: [python]
---
# Python Pip



## 什么是 PIP？

PIP 是 Python 包的包管理器，或者如果您喜欢，也可以是模块。

**注：**如果您有 Python 版本 3.4 或更晚，则默认情况下包括 PIP。

* * *

## 什么是Package？

包包含模块所需的所有文件。

模块是 Python 代码库，您可以在项目中包含。

* * *

## 检查 PIP 是否已安装

将命令行导航到 Python 的脚本目录的位置，然后键入以下内容：

### 例子

检查 PIP 版本：

 C:\Users\_Your Name_\AppData\Local\Programs\Python\Python36-32\Scripts>pip --version

* * *

## 安装 PIP

<font _mstmutation="1" _msthash="104104" _msttexthash="167920610">如果您没有安装 PIP，可以从此页面下载并安装它[：https://pypi.org/project/pip/](https://zshipu.com/t?url=https://pypi.org/project/pip/)</font>

* * *

## 下载包

下载包非常简单。

打开命令行界面，告诉 PIP 下载您想要的包。

将命令行导航到 Python 的脚本目录的位置，然后键入以下内容：

### 例子

下载名为"骆驼壳"的包：

 C:\Users\_Your Name_\AppData\Local\Programs\Python\Python36-32\Scripts>pip install camelcase

现在，您已经下载并安装了第一个软件包！

* * *

* * *

## 使用包

安装包后，即可使用。

将"骆驼箱"包导入您的项目中。

### 例子

导入并使用"骆驼壳"：
```
 import camelcase

c = camelcase.CamelCase()

txt = "hello world"

print(c.hump(txt))

```

* * *

## 查找包

在 10 月[https://pypi.org/。](https://zshipu.com/t?url=https://pypi.org/)

* * *

## 删除包

<font _mstmutation="1" _msthash="105443" _msttexthash="34617063">使用 命令删除包：</font>```uninstall```

### 例子

卸载名为"骆驼壳"的包：

 C:\Users\_Your Name_\AppData\Local\Programs\Python\Python36-32\Scripts>pip uninstall camelcase

PIP 包管理器将要求您确认是否要删除骆驼壳包：

 Uninstalling camelcase-02.1:
  Would remove:
    c:\users\_Your Name_\appdata\local\programs\python\python36-32\lib\site-packages\camecase-0.2-py3.6.egg-info
    c:\users\_Your Name_\appdata\local\programs\python\python36-32\lib\site-packages\camecase\*
Proceed (y/n)?

<font _mstmutation="1" _msthash="104455" _msttexthash="30074044">按压，将删除包。</font>```y```

* * *

## 列表包

<font _mstmutation="1" _msthash="105235" _msttexthash="88881832">使用 命令列出系统上安装的所有包：</font>```list```

### 例子

列出已安装的包：

 C:\Users\_Your Name_\AppData\Local\Programs\Python\Python36-32\Scripts>pip list

结果：

 Package         Version
-----------------------
camelcase       0.2
mysql-connector 2.1.6
pip             18.1
pymongo         3.6.1
setuptools      39.0.1

* * *


