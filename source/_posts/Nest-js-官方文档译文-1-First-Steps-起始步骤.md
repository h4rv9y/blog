---
title: Nest.js 官方文档译文 (1) First Steps 起始步骤
date: 2020-03-19 19:11:38
categories: [Dev, Node.js]
tags:
    - Node.js
    - Nest.js
    - Nest.js 官方文档
toc: true
---
## First steps 起始步骤

在这系列文章中，你可以学习到 Nest 的基础核心用法。为了让你熟悉 Nest 应用程序的基础组件，在下面的内容，我们会编写一个简单的 CRUD 应用程序，并且这个程序覆盖了大部分生产环境中会用到的特性

### 语言

我们非常喜欢 TypeScript ，但其前提是——我们喜欢 Node.js，因为其使得 Nest 能够兼容 TypeScript 和纯 JavaScript

Nest 利用了很多最新的语言特性，如果你使用纯 JavaScript 的话，你需要一个 Babel 编译器

一般我们会使用 TypeScript 作为示例的语言，但你也可以通过点击代码右上角的按钮将代码片段切换到普通 JavaScript 语法

### 需要

请确定你的系统已经安装 Node.js (>= 10.13.0)

### 安装

使用 Nest CLI 来建立一个新项目是十分简单的，如果你安装了 npm，你可以使用以下命令创建 Nest 项目

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

在该目录下会创建一个项目文件夹，里面包括了一些样例代码和 node modules，在里面的 `src/` 目录会生成一些核心文件

```
src
|
+--app.controller.ts
+--app.module.ts
+--main.ts
```

下面是这些核心文件的概要：

| 文件              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| app.controller.ts | 包含一个路由的 Controller 模板                               |
| app.module.ts     | 应用程序的根模块                                             |
| main.ts           | 应用程序的入口文件，通过使用 `NestFactory` 函数来创建 Nest 应用程序实例 |

`main.ts` 包括了一个用于启动程序的异步函数：

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

想要创建一个 Nest 应用程序实例，只需要使用其核心类 `NestFactory` ，`NestFactory` 暴露了一些静态方法，可以让你创建应用程序实例。`create()` 方法会返回一个实现了 `INestApplication` 接口的应用程序对象，该对象包含了一系列的方法，后面的篇章我们会详细讲述它们

在上面的 `main.ts` 示例当中，我们简单地启动了我们的 HTTP 监听器，使得我们的应用程序可以接收 HTTP 请求

> 注意到我们的项目通过 Nest CLI 脚手架创建了一个初始的项目结构，这鼓励开发者保持我们建立的框架结构，保持每个模块放在其专用的目录

### 平台

Nest 致力创建一个平台无关的框架，平台独立性使创建可重用的逻辑部分成为可能，开发人员可以在多种不同类型的应用程序中利用这些逻辑部分

在技术上，一旦创建了一个适配器，Nest 可以运行在任何 Node HTTP 框架。目前有两个 HTTP 平台已经被支持，分别是 express 和 fastify，你可以选择一个最适合你的

| 平台             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| platform-express | Express 是一个知名的极简主义的 Web 框架，是一个经过测验、可用于生产的库，通过社区实现了大量资源。默认使用 `@nestjs/platform-express` 包。许多用户使用 Express 都能获得很好的服务，并且无需采取任何措施即可启用它 |
| platform-fastify | Fastify 是一个高性能且低开销的框架，致力于提供最高的效率与速度 |

无论你使用哪个平台，它会暴露自身的应用接口，分别是 `NestExpressApplication` 和 `NestFastifyApplication` 

当你把类型传递到 `NestFactory.create()` 方法时，如下面的示例。`app` 对象将会仅可用于指定的平台。注意，你不需要指定特定的类型，除非你真的需要进入底层平台 API

```typescript
const app = await NestFactory.create<NestExpressApplication>(AppModule);
```

### 运行应用程序

一旦安装进程完成，通过运行下面的命令即可启动应用程序，并监听 HTTP 请求

```bash
$ npm run start
```

HTTP 服务器监听的端口时定义在 `src/main.ts` 文件当中，当你的应用程序成功运行之后，你可以打开你的浏览器，并导航至 `http://localhost:3000` , 即可看到 `Hello World!` 信息



> 原文地址：https://docs.nestjs.com/first-steps
> 译者：[HAo99](https://blog.hao99.club)

