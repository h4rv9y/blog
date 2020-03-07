---
title: Android 学习之路 - (2) 搭建开发环境
date: 2019-05-11 01:00:35
categories: [Dev, Android]
tags:
	- Android
	- 学习之路
	- 教程
toc: true
---

![Banner_2](/Android-学习之路-2-搭建开发环境/Banner_2.png)
<!-- more -->
---

以上是前言

---

# 基础

经过上一章的枯燥内容的学习，想必你对安卓应该又有了更多的了解了吧。废话不多说，这一章我们便开始搭建我们自己的开发环境，投入到安卓学习当中去。

> 安卓开发目前有三种环境，
>
> 1. Eclipse + ADT + SDK; 
> 2. Android Studio; 
> 3. IntelliJ Idea + SDK
>
> 第一种是比较过时的开发环境，谷歌已经停止了ADT插件的支持，也就是说，基本在API21(Android 5.0)以后的版本都没了支持，基本上被淘汰了，目前渐渐过渡到第二种方法。
>
> 第二种方法是目前较为推荐的方法，本套教程也是使用这一套开发环境，你不需要装什么 ADT 、SDK，只要安一个 Android Studio 就行，部署起来特别方便。
>
> 第三种跟第二种大同小异，因为 Android Studio 本质上也是个 idea，idea 的部署方式基本上就是安个Android SDK 即可。
>
> 接下来的教程讲述第二种开发环境的搭建方法。

## 1. 安装 JDK

安卓是使用 Java 作为开发语言，所以首先第一步就要安装 JDK (Java Development Kit ：Java 开发工具包) 啦。

强烈建议使用 Java 8 来开发。

### Step 1 进入 JDK 8 的官方下载地址

[点击进入下载页面](<https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>)

> 如果地址失效可以通过进入甲骨文官网去寻找下载页面[点击进入官网](<https://www.oracle.com/index.html>)

### Step 2 下载合适的 JDK

首先点击红色箭头所指的单选框同意条款，然后选择自己平台的 JDK 安装包即可，我这里是 MacOS，所以我下的是Mac OS X x64的安装包。

![1557509530519](/Android-学习之路-2-搭建开发环境/1557509530519.jpg)

### Step 3 安装 JDK

1. 打开镜像

![屏幕快照2019-05-11上午1.45.45](/Android-学习之路-2-搭建开发环境/pic-2.png)

1. 打开安装器

![屏幕快照2019-05-11上午1.45.57](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午1.45.57.png)

3. 点击继续→安装

![屏幕快照2019-05-11上午1.46.03](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午1.46.03.png)

等待安装结束即可

### Step 4 配置环境变量

#### a. 首先要获取到 JDK 安装目录

##### 有两种方法，第一种（熟悉命令行操作的用这种）：

---

熟练版：

```bash
$ cd /Library/Java/JavaVirtualMachines
$ ls
$ cd jdk1.8.0_191.jdk(这里填的是你通过ls查看到的目录名)
$ pwd
```

则获取到所需路径。

---

新手版：



1. 按下 <code>Command</code> +<code>space</code> 打开聚焦搜索，输入 Terminal 打开终端(如果你使用的是其他终端就打开你要使用的终端，如 Iterm2)。

![屏幕快照2019-05-11上午1.52.55](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午1.52.55.png)

![屏幕快照2019-05-11上午1.53.32](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午1.53.32.png)

2. 进入安装目录

```bash
$ cd /Library/Java/JavaVirtualMachines
```

![屏幕快照2019-05-11上午2.08.05](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.08.05.png)

3. 查看安装的JDK的目录名

```bash
$ ls
```

![屏幕快照2019-05-11上午2.08.11](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.08.11.png)

4. 进入该目录

```bash
$ cd jdk1.8.0_191.jdk(这里填的是你通过ls查看到的目录名)
```

![屏幕快照2019-05-11上午2.08.24](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.08.24.png)

5. 输入 pwd 获取到路径

```bash
$ pwd
```

![屏幕快照2019-05-11上午2.08.33](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.08.33.png)

6. 将该路径复制

---

##### 第二种：

1. 打开 Finder，选择前往文件夹(或使用快捷键<code>Shift</code>+<code>Command</code>+<code>G</code>)

![屏幕快照2019-05-11上午2.14.31](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.14.31.png)

2. 输入路径/Library/Java/JavaVirtualMachines，点击前往。

![屏幕快照2019-05-11上午2.16.44](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.16.44.png)

3. 获取到安装的目录名

![屏幕快照2019-05-11上午2.16.49](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午2.16.49.png)

4. 则路径为：/Library/Java/JavaVirtualMachines/ + [你进入该目录获取到的jdk目录名]

   如：像我的目录即为 /Library/Java/JavaVirtualMachines/jdk1.8.0_191.jdk

#### b. 配置环境变量

1. 打开 终端，输入~(或cd ~)进入家目录

```bash
$ ~
```

2. 编辑 ~/.bash_profile

```bash
$ vim .bash_profile
```

若为空则直接添加这两行，(vim 编辑器，按i键即可进入插入模式)

```bash
export JAVA_HOME="[刚刚找到的目录]/Contents/Home"
export PATH="$PATH:[刚刚找到的目录]/Contents/Home/bin"

示例：
export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_191.jdk/Contents/Home"
export PATH="$PATH:/Library/Java/JavaVirtualMachines/jdk1.8.0_191/Contents/Home/bin"
```

若不为空，则在新的一行添加

```bash
export JAVA_HOME="[刚刚找到的目录]/Contents/Home"
```

在原有的PATH后面添加(用:分隔)

```bash
示例：
export PATH="/usr/local/opt/ncurses/bin:$PATH:[刚刚找到的目录]/Contents/Home/bin"
```

编辑完成后按<code>Esc</code>退出插入模式，并输入》<code>:wq</code>保存

3. 使用"source .bash_profile"使配置生效

```bash
$ source .bash_profile
```

4. 使用 java -version 测试是否成功配置

```bash
$ java -version
```

## 2. 安装 Android Studio

安装完 JDK，接下来要安装的就是我们要使用的 IDE。在 mac 下安装 Android Studio 可以说是十分简单了，跟其他普通的mac程序一样，只需要下载完后打开镜像，拖拽至应用程序目录即可。

### Step 1 下载安装程序

[点击进入下载页面](<https://developer.android.google.cn/studio>)

点击"Download Android Studio"，即可下载

![1557513967714](/Android-学习之路-2-搭建开发环境/1557513967714.jpg)

### Step 2 安装 Android Studio

打开镜像，将 Android Studio 拖拽至右边的应用程序目录当中去

![屏幕快照2019-05-11上午3.05.09](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.05.09.png)

### Step 3 安装 SDK

1. 首次打开会有以下提示，询问你是否要导入设置，直接选择OK即可。

![屏幕快照2019-05-11上午3.16.41](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.16.41.png)

2. 进行安装的时候可能会弹出以下对话框，这个需要自行想办法找镜像下载服务器代理，或配置科学上网。

![屏幕快照2019-05-11上午3.16.50](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.16.50.png)

3. 顺利进入后，会出现下面的画面，点击Next即可

![屏幕快照2019-05-11上午3.17.02](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.17.02.png)

4. 继续点击next

![屏幕快照2019-05-11上午3.17.11](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.17.11.png)

5. 选择你喜欢的UI配色。

![屏幕快照2019-05-11上午3.17.19](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.17.19.png)

6. 会弹出要你选择 SDK 的安装版本，选择你需要的即可
7. 显示安装内容，点击Finish，静待完成即可。

![屏幕快照2019-05-11上午3.17.34](/Android-学习之路-2-搭建开发环境/屏幕快照2019-05-11上午3.17.34.png)



*(本章完结)*