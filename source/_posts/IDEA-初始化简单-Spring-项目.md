---
title: IDEA  初始化简单 Spring 项目
date: 2020-03-03 19:48:26
categories: [Dev, Java]
tags:
    - Java
    - 教程
    - Maven
    - Spring
    - IDEA
toc: true
---

## IDEA 初始化简单 Spring 项目

### Step. 1 新建项目

![](/IDEA-初始化简单-Spring-项目/idea64_ZV8tmf5wN9.png)

### Step. 2 选择类型为 Maven 项目

![](/IDEA-初始化简单-Spring-项目/idea64_dq1qQOc9hg.png)

### Step. 3 填写项目名称

![](/IDEA-初始化简单-Spring-项目/idea64_clfkosrO9v.png)

> ArtfactId 一般填写项目的名称即可
>
> GroupId 一般填写公司的域名

### Step. 4 设置 Maven 仓库

你可以使用 IDEA 自带的 Maven 仓库

![](/IDEA-初始化简单-Spring-项目/idea64_KVKYqY1ryn.png)

或者如果你本地安装了 Maven，可选择本地的 Maven 仓库

![](/IDEA-初始化简单-Spring-项目/idea64_Pr12kaIArS.png)

> Maven 官方仓库的下载速度在国内并不理想，推荐通过配置 setting.xml 使用国内的阿里镜像来进行下载，详情可看另外一篇有关 Maven 镜像配置的文章

### Step. 5 简单的 Maven 项目新建完成

![](/IDEA-初始化简单-Spring-项目/idea64_RgNDIxmVTG.png)

### Step. 6  添加依赖

在项目根目录下有个 pom.xml 文件，这个是 Maven 与项目相关的主要配置文件

我们可以在 project 标签里 version 标签后面编写一个 dependencies 标签

```xml
<dependencies>

</dependencies>
```

在这个 dependencies 里面即可以添加我们的依赖啦，Maven 中单个依赖的格式是这样的：

```xml
<dependency>
  <groupId>组名</groupId>
  <artifactId>项目名</artifactId>
  <version>版本号</version>
  <scope>作用范围</scope>
</dependency>
```

那么我们要怎么样才能够获得这些信息，添加我们需要的依赖呢？

答案是去到 Maven 仓库的官网去查：https://mvnrepository.com/ （直接百度也能找到这个网站）

通过在这个网站搜索 spring 我们搜索到下面这些内容：

![](/IDEA-初始化简单-Spring-项目/msedge_iibB9JspQl.png)

点进我们需要的依赖里，如 spring core

![](/IDEA-初始化简单-Spring-项目/msedge_GksQTvBQFQ.png)

> 可以看到版本列表，和其所属的仓库，以及使用量，可以根据这些判断哪个版本较为稳定

点进你想要使用的版本

![](/IDEA-初始化简单-Spring-项目/msedge_G0xwF97n4w.png)

可以发现我们需要的 dependency 标签的内容，就在该页面上，直接点击一下文本框则会自动复制，粘贴到我们的 pom.xml 文件下的 dpendencies 标签里即可

> Spring 相关的依赖有：
>
> - spring-core: Spring 框架的核心类库
> - spring-context: Spring 框架的一些扩展类
> - spring-beans: Spring 框架 Ioc/DI 操作的类库
> - spring-aop: Spring 框架面向切面编程的支持
> - spring-expression: SpEL 支持

把 Spring 相关的依赖添加完之后是如下这个样子：

![](/IDEA-初始化简单-Spring-项目/idea64_W5tNsOTvAs.png)

>Spring 依赖中的版本可以选择与我这里的不一样，但要保证 Spring 各个依赖中的版本要保持是同一个版本
>
>这张图还多引入了一个 Junit 的依赖，这是一个单元测试用的类库

编写完后，应用引入依赖的时候要点一下右下角弹框的 Import Changes

![](/IDEA-初始化简单-Spring-项目/idea64_vNPsVePx7v.png)

此时 Maven 就会自动在云端仓库去寻找相关的 Jar 包进行下载，下载过一次之后，以后再需要用到这些依赖的时候，Maven 会直接从本地仓库引入，不需要重新下载

### Step. 7 简单测试

这里随意编写一个利用 Spring IoC 容器的小Demo

1. 首先我们先编写一个要被调用的目标类，我们用它来输出一段 Hello

这里我们再 src/main/java 目录下新建个包 org.example.spring.demo

在这包下我们新建一个类 HelloService

```java
public HelloService {
	public void sayHello() {
        System.out.println("Hello!");
    }
}
```

2. 接着我们使用 xml 配置的方式将这个类添加到 Spring IoC 容器当中去

在 src/main/resources 目录下新建一个 applicationContext.xml 文件

将我们刚写的类配置为一个bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="helloService" class="org.example.spring.demo.HelloService"/>

</beans>
```

> bean 标签中的文档定义可以在 spring 官网的文档中找到
>
> https://docs.spring.io/spring/docs/5.2.4.RELEASE/spring-framework-reference/core.html#spring-core
>
> bean 的 id 属性一般写法是将目标类的类名首字母小写，其他保持一致
>
> bean 的 class 属性要写上刚创建类的全限定名称

3. 接下来在 org.example.spring.demo 包下创建一个 Main 类，用于启动我们的程序，我在这里将从容器获取对象的操作也写在 main 方法里

```java
public class Main {

    public static void main(String[] args) {

        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        // 通过 Bean 的 Id 从 Spring IoC 容器中获取到对象
        HelloWorldService helloWorldService = (HelloWorldService) context.getBean("helloService");

        // 调用对象的 sayHello() 方法，输出字符串
        helloWorldService.sayHello();
    }
}
```

运行程序可得：

![](/IDEA-初始化简单-Spring-项目/idea64_RZwKued7hM.png)

可见我们的项目成功运行了起来，接下来进行愉快的学习吧~

*本教程完结*