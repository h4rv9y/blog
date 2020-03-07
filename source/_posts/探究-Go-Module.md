---
title: 探究 Go Module
date: 2019-10-27 01:51:22
categories: [Dev, Golang]
tags:
	- Golang

toc: true
---

![banner](探究-Go-Module/banner.jpg)
<!-- more -->

# 探究 Go Module

Go 1.11 和 1.12 已经包含了对 Go Module 的初步支持，截止到本文已经 Golang 已经发布了 1.13 版本，是时候将这个玩意用上了。

Go Module 是 Golang 官方出的一种新的版本依赖管理系统，它使得 Golang 的包管理比以前更加清晰直观，且易于操作。笔者试用了一下，踩完前面的坑之后，发现这种新的模式还是相当好用的。本文将对 Go Module 的基础操作做介绍，顺便教你们绕一下其中的一些坑。

## 如何使用 Modules？

1. 首先 Modules 功能是在 go 1.11 版本出现的，所以你需要将你的 go 版本升级到 1.11 以上，现在 1.13 已经出了，建议是直接使用新版。
2. Go Module 是有一个环境变量来控制它的开关，当然在新版里它默认是一个<code>auto</code>值，也可以不用调节

### GO111MODULE

如何去设置该变量呢，首先打开系统的环境配置文件：

```bash
➜ vim ~/.zshrc
```

> MacOS 系统下的环境变量的配置文件有
> 系统级：
> /etc/profile
> /etc/paths
> Bash 系：
> ~/.bash_profile
> ~/.bash_login
> ~/.bashrc
> Zsh 系：
> ~/.zshrc

在后面加上

```bash
# 开启 Go Module
export GO111MODULE=auto
```

<code>G111MODULE</code>其实有三个值，分别是：<code>off</code>,<code>on</code>和<code>auto</code>(默认)。

其三者的区别为：

- <code>off</code>：将不支持 module 功能，寻找依赖包将会沿用旧版本那种通过 vendor 目录或者 GOPATH 模式来查找。

- <code>on</code>：将会强制使用 module 功能，不会再去 GOPATH 目录下查找相关包。

- <code>auto</code>：这是 go 的默认值，go 命令将会根据当前目录来决定是否启用 module 功能。
  - 若当前目录在 $GOPATH/src 下，则会使用以前的 GOPATH 模式。
  - 若当前目录不在 $GOPARH/src 内，且该目录包含 go.mod 文件，则会启用 module 模式。

>当 Go Module 功能启用时，依赖包的存放位置变更为 `$GOPATH/pkg`，允许同一个 package 多个版本并存，且多个项目可以共享缓存的 module。

设置完成之后敲下<code>Esc</code>，按下<code>:wq</code>保存并退出。

想要命令立即生效，还需要在终端输入：

```bash
➜ source ~/.zshrc
```

### 设置代理

在使用 Go Module 前，笔者在这里强烈建议先配置一下 Golang 的代理，因为在国内下载谷歌服务器的文件实在是太难了，慢还不说，最怕下都下不动。

使用方式也十分简单，如果是 macOS 的话直接运行下面的命令即可

```bash
# 配置 GOPROXY 环境变量
export GOPROXY=https://goproxy.io
# 建议使用下面这个代理节点 Updated in 2020/02/11
export GOPROXY=https://goproxy.cn
```

或者你也可以像本文上面设置 GO111MODULE 环境变量一样，添加在它的后面，当然记得要 source 一下。

> GOPROXY 代理的官网地址：https://goproxy.io/zh/

### go mod 命令

go mod 命令便是 Go Module 模式中最关键的命令，开启了Go Module，将使用该命令来管理 Golang 的包。

有以下命令

| 命令     | 说明                             |
| -------- | -------------------------------- |
| download | 下载依赖包                       |
| edit     | 编辑 go.mod                      |
| graph    | 打印模块视图                     |
| init     | 在当前目录初始化成 module        |
| tidy     | 拉取缺少的模块，移除不需要的模块 |
| vendor   | 将依赖复制到 vendor 目录下       |
| verify   | 验证依赖是否正确                 |
| why      | 解释为什么需要依赖               |

## 项目实战

### 示例 一：创建一个新项目

首先是先在非 $GOPATH/src 的目录下创建自己的工程目录，笔者这里就将其新建在 ~/GoProject/ 目录下。

```bash
➜ ~ mkdir GoProject
➜ ~ cd GoProject
➜ ~/GoProject mkdir demo
➜ ~/GoProject cd demo
```

然后使用<code>go mode init</code>命令，将当前目录变为一个 Go Module，且目录会生成一个 go.mod 和一个 go.sum 的文件。

```bash
➜ ~/GoProject/demo go mod init demo
go: creating new go.mod: module demo
```

一条命令即可将项目变成一个 Go Module，就是这么简单。

go.mod 文件一旦创建后，接下来，它的内容将会被 go toolchain 全面掌控，你在该目录使用例如 go get、go build、go mod 等命令时，它都会自动维护 go.mod 文件。

简单举个例子，你现在需要 xorm 的依赖，你就像以前一样，使用如下命令

```bash
➜ ~/GoProject/demo go get github.com/go-xorm/xorm
```

它不会将依赖像以前一样下载到 \$GOPATH/src 目录下，它会下载到 \$GOPATH/pkg 目录下，且允许多个版本并存，多个 Go Module 可以互相缓存该目录下的依赖。

然后在 go.mod 文件下，你会发现你的 xorm 依赖已经自动添加到文件当中去了。

```
module demo

go 1.13

require (
	github.com/go-xorm/xorm v0.7.10
)
```

然后在该目录下进行编码，你会发现你的依赖已经可以正常使用了。

### 示例二：从已有的工程转换为 Go Module

操作其实十分简单，首先还是像上个示例一样，进到工程目录初始化工程。

```bash
➜ go mod init demo2
```

go.mod 和 go.sum 文件就会被生成，然后只需要执行：

```bash
➜ go run main.go
go: finding github.com/go-sql-driver/mysql v1.4.1
go: finding github.com/kataras/golog v0.0.9
...省略数行
```

此时，go 会自动去查找代码中需要的依赖，并且将其下载下来，而且其依赖也会显示在 go.mod 文件当中。

**注意了，讲一下这里的坑**

有些工程这么操作完之后发现代码炸了，跑不起来，这是为什么呢？使用 go module 进行 go get 的时候和之前 \$GOPATH 模式 go get 下载依赖的方式是不一样的。

- 如果是旧方式，使用 go get 命令是从 github 上爬最新的 commit 将其下载下来。
- 而如果是 Go Module 的方式的话，使用 go get 命令是首先从 github 上爬最新的 release。

笔者使用的一个 jwt 的第三方依赖的作者，他在 16 年发了一个 release，然后他的最新 commit 是在 18 年，使用go get 下载下来的 release 自然是没法用了，代码直接全部爆红，那么怎么解决呢？

其实 go get 依赖后面是可以添加版本号的，具体的命令如下

```bash
➜ go get [依赖地址]@[依赖版本号]
```

但是这里又需要输入版本号，不是 release 才有版本号吗？ commit 的版本号又是啥？别急，别忘了 commit 还有一条长长的 id，将其作为版本号即可(笔者在网上到处翻阅博文都没找到这一点，自己试出来的)

```bash
➜ go get github.com/SermoDigital/jose@803625baeddc3526d01d321b5066029f53eafc81
```

笔者像上面这样就拉到了对应 commit 的依赖(一个第三方的 jwt 实现)。

## 关于 go.mod 文件

go.mod 提供了<code>module</code>、<code>require</code>、<code>replace</code>和<code>exclude</code>四个命令：

- `module` 语句指定包的名字（路径）
- `require` 语句指定的依赖项模块
- `replace` 语句可以替换依赖项模块
- `exclude` 语句可以忽略依赖项模块

`module` 和 `require` 在上面示例中都有体现，下面讲讲 `replace` 语句

### 使用 replace 替换无法直接获取的 package

由于某些已知的原因，并不是所有的 package 都能成功下载，比如：golang.org 下的包（通过上文设置代理其实可以解决）。

这些包可以通过在 go.mod 文件中使用 replace 指令替换成 github 上对应的仓库，比如：

```
replace (
	golang.org/x/crypto v0.0.0-20190313024323-a1f597ede03a => github.com/golang/crypto v0.0.0-20190313024323-a1f597ede03a
)
```

*(本文完结)*
