---
title: go包管理
date: 2021-08-09 15:51:42
tags: module
categories: go
---

## GOPATH

GOPATH是go使用的一个环境变量，代表的是go的工作目录，可用`go env`查看。
当使用`go build`，`go install`等命令时，会从GOPATH/src目录下寻找文件

下面是一个目录的例子，main.go引用a.go。

```code
└── src
    ├── a
    │   └── a.go
    └── hello
        └── main.go
```

使用`go install hello`命令后，会编译main.go和a.go，在GOPATH/bin目录下生成可执行文件。

```code
├── bin
│   └── hello
└── src
    ├── a
    │   └── a.go
    └── hello
        └── main.go
```

如果需要外部依赖，可通过`go get -u host/author/repository`获取。
源码会放在GOPATH/src/host/author/respository目录下。
如果该依赖提供可执行文件，会在GOPATH/bin目录下生成二进制可执行文件;
如果该依赖提供可链接库，则在GOPATH/pkg/host/author/下生成静态链接文件。

**这是go最原始的包管理方式。**

## vendor

vendor是go1.5提供的特性，可通过govendor工具进行包管理，地址<https://github.com/kardianos/govendor>。

通过`go get -u github.com/kardianos/govendor`命令进行下载。

在src目录下执行`../bin/govendor init`，会在GOPATH/src下生成vendor文件夹，里面的vendor.json用来记录依赖信息和版本。

```code
├── bin
│   ├── govendor
│   └── hello
└── src
    ├── a
    ├── github.com
    ├── hello
    └── vendor
```

`govendor list`查看依赖包的状态。

`govendor add`可以将依赖包转移到vendor目录下。

具体可查看`govendor --help`。

**1.11版本之后go提供了module功能。所以govendor已经没有再更新了，推荐使用module来管理项目。**

## go.mod

go1.11后有GO111MODULE环境变量，其有三个值。

- off 不支持module，使用vendor或GOPATH模式查找依赖

- on 使用module功能，通过go.mod查找依赖

- auto 当处于GOPATH目录之外表现为on；当处于GOPATH目录下表现为off，即使当前目录下存在go.mod文件

`go mod init module_name`会在当前目录下生成go.mod文件。
此后go工具链会接管go.mod，记录依赖信息。依赖包的代码存放在GOPATH/pkg中。

```bash
go mod init example.com/hello
go get github.com/amoghe/distillog
cat go.mod
module example.com/hello

go 1.16

require github.com/amoghe/distillog v0.0.0-20180726233512-ae382b35b717
```

