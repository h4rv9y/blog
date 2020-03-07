---
title: Git 学习
date: 2019-04-03 20:49:17
categories: [Dev, Git]
tags:
  - git
  - 教程
toc: true
---

## git 是什么？

![git](Git-学习/git.jpg)

Git 是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。 Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
<!-- more -->

# 安装git

官网地址：https://git-scm.com/downloads

安装完成后，在开始菜单找到Git Bash或者直接在桌面Git Bash Here，进行设置用户名和密码

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱" 
```

# 创建本地版本库（仓库）

什么是版本库呢？版本库就是仓库，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，包括每个文件的修改、删除。

那么怎么新建这个仓库呢？

 首先，到一个你想要新建仓库的地方，右键使用Git Bash Here，使用如下指令

```bash
$ mkdir MyProject #这个命令是make directory的意思，创建一个名为MyProject的文件夹) 
$ cd MyProject 	  #这个命令是change directory的意思，进入到名为MyProject的文件夹)
$ pwd 			    #这个命令是print working directory的意思，打印输出目前所在的目录)
```

虽然你们也可以直接在资源管理器里直接右键新建文件夹然后进到里面再右键git bash here，这样也可以让bash进到这个目录里，但是讲解命令行的方法可以让你们快速认识到liunx的一些基础命令。常见的文件操作命令还有下面这些，有兴趣的可以之后了解。

ls、rmdir、mv、cp、rm

| 命令                        | 作用                                                         |
| --------------------------- | ------------------------------------------------------------ |
| rm                          | remove 的缩写，删除文件，删除目录的话要加上参数 -r ，例：rm -r ./MyProject |
| ls                          | 显示目录中的内容，la可以显示所有文件和详情信息               |
| cp <原文件/目录> <目标目录> | copy 的缩写，复制文件，复制目录需要加上-r参数，例：cp -r MyProject ~/Desktop 将 MyProject 文件夹移动至桌面 |
| mv <原文件/目录> <目标目录> | move 的缩写，将文件从原目录移至目标目录，也是改名字的指令，例：mv abc.txt cba.txt 将 abc 文件改名为 cba |
| rmdir                       | remove directory 的缩写，删除目录的意思                      |

 接下来要做的是通过git init命令把这个目录变成git可以管理的仓库

```bash
$ git init
Initialized empty Git repository in /你仓库的目录
```

它就会把仓库帮你建好，而且告诉你是一个空的仓库，而且目录下会多出一个.git的目录，这个目录是默认隐藏的。

你不一定需要在空目录下新建git仓库，选择一个已有工程也是可以的，但是初始化的步骤是都要做的。

# 将文件添加到仓库中

新建完仓库之后，你需要把文件放进git仓库里。第一步肯定是你把文件从别的地方放至这个仓库目录里，或者是在这个目录里新建文件，但做完这一步并没有完成。你还需要告诉git，这个文件是要添加到git仓库里的。

 如果你添加的是一个文件，如像一个叫file的文本文件，可以使用下面的指令将文件添加到仓库。

```bash
$ git add file.txt
```

执行完之后，没有任何显示，就代表添加成功了。

 如果你添加的是一个存在的工程，可以使用以下指令

```bash
$ git add .
```

它会将目录里面所有的文件添加进去。

 接下来要做的就是将刚刚添加的文件提交到git仓库

```bash
$ git commit -m "First commit."
[master（根提交） c47f0a6] First commit.
 37 files changed, 790 insertions(+)
```

commit后面的参数 -m 的意思是本次提交的说明，可以输入任意内容，最好输入一些有意义的内容，像是对程序的修改，这样你能够从历史记录里方便得找到改动的记录。

 该命令执行成功后会显示:

提交的分支：[master（根提交） c47f0a6]

提交的说明：First commit.

37 files changed, 790 insertions(+)，代表的是37个文件被改动，插入了790行内容。

(此处将前面的部分实机演示)

# 基本概念

## 什么是工作区？

工作区就是你电脑里能看到的目录，比如刚刚新建并初始化了git仓库的MyProject文件夹，这里面就是工作区。

## 什么是版本库？

工作区里有一个隐藏目录.git，这就是版本库。

# 添加远程库

已经在本地创建了一个git仓库之后，又想在github或者码云创建一个git仓库，并且让这两个仓库进行远程同步，这样既可以将GitHub上的仓库作为一个备份，亦可以让其他人通过该仓库进行协作。

## 首先自行注册GitHub或者码云账号。

## SSH Key设置

若在用户主目录下，看看有没有.ssh目录，如果有，可以跳过下一步，若没有执行以下语句

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```

然后无脑下一步。

```bash
enerating public/private rsa key pair.
Enter file in which to save the key (/Users/lwh/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/lwh/.ssh/id_rsa.
Your public key has been saved in /Users/lwh/.ssh/id_rsa.pub.
The key fingerprint is:
```

*Your public key has been saved in /Users/lwh/.ssh/id_rsa.pub.*

(可以看见ssh的公钥储存在了 /Users/lwh/.ssh/id_rsa.pub 这个目录下)

然后登陆GitHub或码云，将该文件下的内容添加至账号下。

(待完成)

## 新建远程仓库

(待完成)

## push到远程库的相关指令

```bash
//第一次提交
$ git remote add origin https://github.com/HAo99/test.git
$ git push -u origin master
枚举对象: 73, 完成.
对象计数中: 100% (73/73), 完成.
使用 12 个线程进行压缩
压缩对象中: 100% (52/52), 完成.
写入对象中: 100% (73/73), 123.02 KiB | 9.46 MiB/s, 完成.
总共 73 （差异 0），复用 0 （差异 0）
To https://github.com/HAo99/test.git
 * [new branch]      master -> master
分支 'master' 设置为跟踪来自 'origin' 的远程分支 'master'。

//以后提交
$ git push origin master
```

## 从远程库克隆

```bash
$ git clone git@github.com:HAo99/test.git
```

## 分支与多人协作

分支就是相当于两条时间线，两条时间线之间是互不干扰的，而且你可以在某个时间点将两条时间线合并。比如说你在开发当中，假设你的程序需要开发两个功能，一个查看通讯录和一个发短信的功能，你和你的同事做好了分工，你被分配到制作查看通讯录这个功能，你的同事分配到做发短信的功能，但在我们没有分支的情况下，我的工作会影响到别人的工作，当你的代码没有写完，你直接提交，不完整的代码会导致你的同事没办法工作。如果等代码全部写完再提交，就会存在丢失每天进度的风险。

有了分支之后，你可以和你的同事在不同的分支上工作，当这两个功能都完成的时候，就可以将两条分支合并。

## 创建分支

要使用分支首先要创建分支，git仓库默认的分支是master，分支即是一条时间线，时间线上包含了很多个时间点（就是每次commit的时候就是将add的内容提交到分支上，相当于一个时间点），创建了分支就相当于在创建分支这个时间点分叉出一条新的时间线。

```bash
$ git branch <分支名>
```

### 切换分支

通过下面这条命令即可切换至刚刚创建的分支。

```bash
$ git checkout <分支名>
```

### 创建+切换

这条指令可以将上面两条指令合成成一条，即是创建分支并将目前git的分支切换到新创建的分支。

```bash
$ git checkout -b <分支名>
```

### 查看分支

```bash
$ git branch
```

### 合并分支

像上面讲述的那样，当你功能完成之后，首先将目前的分支切换到你要合并到的分支(git checkout <分支名>)，使用下面这条指令将所指定的分支合并到目前所在的分支。

```bash
$ git merge <分支名>
```

### 删除分支

合并成功后便可以把分支删除掉，使用下面这条指令就可以了。

```bash
$ git branch -d <分支名>
```

### 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master 分支应该是非常稳定的，也就是仅仅用来发布新版本，平时不能在这上面干活。

干活应该在一个新建的 dev 分支上，也就是说 dev 分支是不稳定的，仅当 dev 分支到一种能发布的状态下，再将 dev 合并到 master 分支上进行发布。

你和你的小伙伴应该在 dev 分支上干活，每个人都可以创建自己的分支，时不时往dev分支上合并就可以了。

## 多人协作

### 推送分支

推送分支就是把该分支上的所有本地提交推送到远程仓库。推送时要指定本地分支，这样，git就会把该分支推送到远程库对应的远程分支上。

例如：

```bash
$ git push origin master
```

如果要推送至别的分支：

```bash
$ git push origin dev
```
