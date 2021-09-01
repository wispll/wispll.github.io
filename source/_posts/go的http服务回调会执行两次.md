---
title: go的http服务回调会执行两次
date: 2021-09-01 11:42:17
tags: http
categories: go
---

先来看下面的一段代码：

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", indexHandler)
	http.ListenAndServe(":8811", nil)
}

func indexHandler(w http.ResponseWriter, r *http.Request) {
	fmt.Println("index page")
}

```

当在浏览器输入localhost:8811的时候，命令行会输出


```bash
index page
index page 
```

会产生两次输出。

这是因为浏览器在访问一个地址的时候，会默认访问host/favicon.ico作为网站图标。
所以这其实是两个请求

- localhost:8811

- localhost:8811/favicon.ico

但/favicon.ico，我们是没有进行处理的。这就要看http模块内部的处理方式了。

```go
//启动了一个http服务
http.ListenAndServe(":8811", nil)

//这是函数的签名
// ListenAndServe listens on the TCP network address addr and then calls
// Serve with handler to handle requests on incoming connections.
// Accepted connections are configured to enable TCP keep-alives.
//
// The handler is typically nil, in which case the DefaultServeMux is used.
//
// ListenAndServe always returns a non-nil error.
func ListenAndServe(addr string, handler Handler) error {
	server := &Server{Addr: addr, Handler: handler}
	return server.ListenAndServe()
}

```

handler这个参数传入了nil，根据注释它会默认使用DefaultServeMux

DefaultServeMux对于不在的路径，会转交给"/"路径的handler处理。更详细的可以看看DefaultServeMux的定义和注释。

所以回调才会被执行了两次，当用`curl localhost:8811`访问时，回调就会正常的执行一次。


