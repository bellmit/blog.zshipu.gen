---
title: 关键词库-Go 语言高效分词, 支持英文、中文、日文等
author: 知识铺
date: 2021-09-27 14:03:10+08:00

tags: [分词]
---



Go 语言高效分词, 支持英文、中文、日文等

词典用双数组trie（Double-Array Trie）实现， 分词器算法为基于词频的最短路径加动态规划。

支持普通和搜索引擎两种分词模式，支持用户词典、词性标注，可运行JSON RPC服务。

分词速度单线程9MB/s，goroutines并发42MB/s（8核Macbook Pro）。

## 安装/更新

```
go get -u github.com/go-ego/gse
```

## Build-tools

```
go get -u github.com/go-ego/re
```

### re gse

To create a new gse application

```
$ re gse my-gse
```

### re run

To run the application we just created, you can navigate to the application folder and execute:

```
$ cd my-gse && re run
```

### 使用

```go
package main

import (
    "fmt"

    "github.com/go-ego/gse"
)

func main() {
    // 载入词典
    var segmenter gse.Segmenter
    segmenter.LoadDict()
    // segmenter.LoadDict("your gopath"+"/src/github.com/go-ego/gse/data/dict/dictionary.txt")

    // 分词
    text := []byte("中华人民共和国中央人民政府")
    segments := segmenter.Segment(text)

    // 处理分词结果
    // 支持普通模式和搜索模式两种分词，见代码中 ToString 函数的注释。
    fmt.Println(gse.ToString(segments, false)) 

    text1 := []byte("深圳地王大厦")
    segments1 := seg.Segment([]byte(text1))
    fmt.Println(gse.ToString(segments1, false)) 
}
```

项目地址: https://github.com/go-ego/gse

