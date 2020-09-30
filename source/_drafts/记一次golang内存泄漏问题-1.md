---
title: 记一次golang内存泄漏问题-1
tags:
  - Golang
  - 内存泄漏
categories:
  - [踩坑日志, Golang内存泄漏]
---

# 问题代码

``` golang
package main

import (
    "net/http"
    "fmt"
)

func main() {
	resp, err := http.Get("http://localhost:5000")
	if nil != err {
		fmt.Printf("request: %s", err.Error())
		return
	}
	defer resp.Body.Close()
	var body []byte
	_, err = resp.Body.Read(body)
	if nil != err {
		fmt.Printf("read body: %s", err.Error())
		return
	}
	fmt.Printf("request body: %s", string(body))
}
```
上面是一段我们系统中经过简化的Golang请求http服务的代码, 正常情况下, 这段代码不会出现问题, 可是实际部署到测试环境中进行压测时却出现了内存泄漏.

# 问题分析

## 使用PProf定位泄露代码段
d
## 原因分析
d