---
title: 关键词库-本地sqllit存储
author: 知识铺
date: 2021-09-27 13:03:10+08:00

tags: [sqllit]
---



## 本地存储

```go
package db

import (
	"database/sql"
	"fmt"
	_ "github.com/mattn/go-sqlite3"
	"log"
	"os"
)

var db *sql.DB

var err error

func init() {
	if isExist("./keybase.db") {
		db, err = sql.Open("sqlite3", "./keybase.db")
		if err != nil {
			log.Fatal(err)
		}
	}else{
		db, err = sql.Open("sqlite3", "./keybase.db")
		if err != nil {
			log.Fatal(err)
		}

		sqlStmt := `
		create table keywords (id integer PRIMARY KEY autoincrement,keyword text, url text);
		`
		_, err = db.Exec(sqlStmt)
		if err != nil {
			log.Printf("%q: %s\n", err, sqlStmt)
			return
		}

	}

}

func isExist(path string)(bool){
	_, err := os.Stat(path)
	if err != nil{
		if os.IsExist(err){
			return true
		}
		if os.IsNotExist(err){
			return false
		}
		fmt.Println(err)
		return false
	}
	return true
}

func AddKeyword(keyword,url string) {

	tx, err := db.Begin()
	if err != nil {
		log.Fatal(err)
	}
	stmt, err := tx.Prepare("insert into keywords(keyword, url) values(?, ?)")
	if err != nil {
		log.Fatal(err)
	}
	defer stmt.Close()
	_, err = stmt.Exec(keyword,  url)

	tx.Commit()

}
func QueryKey(keyword string) string {
	stmt, err := db.Prepare("select url from keywords where keyword = ?")
	if err != nil {
		log.Fatal(err)
		return ""
	}
	defer stmt.Close()
	var url string
	err = stmt.QueryRow(keyword).Scan(&url)
	if err != nil {
		log.Fatal(err)
		return ""
	}
	fmt.Println(url)
	return url
}

```



## 异常处理

异常捕获

```go

func Try(fun func(), handler func(interface{})) {

	defer func() {

		if err := recover(); err != nil {

			handler(err)

		}

	}()

	fun()

}



func AddKeyword(keyword,url string) {
	try.Try(func() {
		tx, err := db.Begin()
		if err != nil {
			log.Fatal(err)
		}
		stmt, err := tx.Prepare("insert into keywords(keyword, url) values(?, ?)")
		if err != nil {
			log.Fatal(err)
		}
		defer stmt.Close()
		_, err = stmt.Exec(keyword,  url)

		tx.Commit()

	}, func(i interface{}) {
		fmt.Println(i)
	})
	

}
```

