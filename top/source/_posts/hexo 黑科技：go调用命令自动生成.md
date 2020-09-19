---
title: hexo 黑科技：go调用命令自动生成
---

### [](#hexo)自动生成hexo博客静态文件
```
 package main

 import (

 	"log"

 	"os/exec"

 	"time"

 	"os"

 	"path/filepath"

 )

 // 此命令工具用于辅助hexo进行博客写作

 // 原理：

 // 1\. 根据source目录下的文件提交变化自动重新生成博客静态文件

 // 2\. 启动hexo服务器，端口为5000

 func  main() {

 	blogDir := filepath.Join(`W:\`, `gits`, `blog`)

 	//首先生成一次，然后取得当前的commitID

 	generateBlog(blogDir)

 	lastCommitID := getLastCommitID(blogDir)

 	//运行hexo本地服务器

 	go func() {

 		runBlog(blogDir)

 	}()

 	//不停地检查当前commitID是否与保存的是否一致，如不一致，则重新生成

 	for {

 		newCommitID := getLastCommitID(blogDir)

 		if newCommitID != lastCommitID {

 			generateBlog(blogDir)

 			lastCommitID = newCommitID

 		}

 		time.Sleep(10 * time.Second)

 	}

 }

 func  runBlog(blogDir  string) {

 	cmd := exec.Command(`hexo`, `server`, `-s`, `-p`, `5000`)

 	cmd.Dir = blogDir

 	cmd.Stdout = os.Stdout

 	cmd.Stderr = os.Stderr

 	err := cmd.Run()

 	if err != nil {

 		log.Fatal(err)

 	}

 }

 func  getLastCommitID(blogDir  string) string {

 	cmd := exec.Command(`git`, `rev-parse`, `HEAD`)

 	cmd.Dir = filepath.Join(blogDir, `source`)

 	out, err := cmd.Output()

 	if err != nil {

 		log.Fatal(err)

 	}

 	return string(out)

 }

 func  generateBlog(blogDir  string) {

 	cmd := exec.Command(`hexo`, `generate`)

 	cmd.Dir = blogDir

 	cmd.Stdout = os.Stdout

 	cmd.Stderr = os.Stderr

 	err := cmd.Run()

 	if err != nil {

 		log.Fatal(err)

 	}

 }

```

### [](#hexo-1)部署hexo博客

```
 package main

 import (

 	"path/filepath"

 	"os/exec"

 	"os"

 	"log"

 )

 // 此命令工具用于将hexo部署至服务器

 func  main() {

 	blogDir := filepath.Join(`W:\`, `gits`, `blog`)

 	deployBlog(blogDir)

 }

 func  deployBlog(blogDir  string) {

 	cmd := exec.Command(`hexo`, `deploy`)

 	cmd.Dir = blogDir

 	cmd.Stdout = os.Stdout

 	cmd.Stderr = os.Stderr

 	err := cmd.Run()

 	if err != nil {

 		log.Fatal(err)

 	}

 }
```

### [](#tomcat)杀Tomcat
```
 package main

 import (

 	"os/exec"

 	"log"

 	"bufio"

 	"strings"

 	"io"

 )

 // 此命令工具杀掉意外未死的tomcat进程

 // idea有时候意外退出，此时开发用的tomcat服务器还在运行

 func  main() {

 	cmd := exec.Command(`netstat`, `-ano`)

 	output, err := cmd.StdoutPipe()

 	if err != nil {

 		log.Fatal(err)

 	}

 	go func() {

 		cmd.Run()

 	}()

 	processOutput(output)

 }

 func  processOutput(output  io.ReadCloser) {

 	scanner := bufio.NewScanner(output)

 	for scanner.Scan() {

 		line := scanner.Text()

 		if hasTomcatPort(line) {

 			parts := strings.Fields(line)

 			tomcatPid := parts[len(parts) -1]

 			log.Println(tomcatPid)

 			killCmd := exec.Command(`taskkill`, `/F`, `/PID`, tomcatPid)

 			killCmd.Run()

 		}

 	}

 }

 func  hasTomcatPort(line  string) bool {

 	return strings.Contains(line, `LISTENING`) && (strings.Contains(line, `8080`) || strings.Contains(line, `1099`))

 }

```

### [](#heading)总结

Go语言很精练，用来写这些小工具很合适。同时也可以经常用Go写点小东西练练手，以免长时间不用忘记了Go的玩法。
