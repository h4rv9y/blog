---
title: IDEA 初始化 SSM 项目
date: 2020-03-03 13:34:01
categories: [Dev, Java]
tags:
    - Java
    - 教程
    - Maven
    - IDEA
    - SSM
    - Spring
    - MyBatis
toc: true
---
## IDEA 初始化 SSM 项目

### Step. 1 新建 Maven 项目

1. 创建项目

![idea](/IDEA-初始化-SSM-项目/idea64_9fWdwLkBIU.png)

2. 选择 Maven 工程，并选用 webapp 的模板

![](/IDEA-初始化-SSM-项目/idea64_djmmMMj3XX.png)

3. 填写项目的相关名称

![](/IDEA-初始化-SSM-项目/idea64_Kp0uLxx8fZ.png)

> ArtfactId 一般填写项目的名称即可
>
> GroupId 一般填写公司的域名

4. 配置 Maven

使用 IDEA 自带的 Maven 仓库

![](/IDEA-初始化-SSM-项目/idea64_KVKYqY1ryn.png)

或是选用使用本地安装的 Maven 仓库

![](/IDEA-初始化-SSM-项目/idea64_Pr12kaIArS.png)

> Maven 官方仓库的下载速度在国内并不理想，推荐通过配置 setting.xml 使用国内的阿里镜像来进行下载，详情可看另外一篇有关 Maven 镜像配置的文章

5. 等待 Maven 自动把插件下载完毕，项目新建的工作就完成了

![](/IDEA-初始化-SSM-项目/idea64_jwt6yHaOVj.png)

### Step. 2 配置项目目录结构

1. 打开项目的 Poject Structure

![](/IDEA-初始化-SSM-项目/idea64_t7KSUj5ErR.png)

2. 进入 Modules 选项卡

![](/IDEA-初始化-SSM-项目/idea64_AFa6IovMlR.png)

> 在目录下可通过 右键 New Folder... 来新建项目目录

3. 将项目目录配置成下图模样，并给目录打上标签

![](/IDEA-初始化-SSM-项目/idea64_tdIsxcCUyt.png)

> 目录的名字要与图上的一致，而且检查红框处是否出现错乱，需要跟图像上的一致

4. 点击 OK 后，此时 IDEA 右下角会提示 Maven 项目需要 Import，点击 `Import Changes` 按钮即可

![](/IDEA-初始化-SSM-项目/idea64_vNPsVePx7v.png)

> 如果不喜欢手动更新 Maven 的导入，也可以选择 `Enable Auto-Import`，在之前版本的 IDEA，自动导入会使得你在编写依赖的时候卡顿

接下来即可开始添加 SSM 的依赖

### Step. 3 依赖添加

1. 打开 src 目录下的 pom.xml 文件，可以发现里面有个 dependencies 的标签，这个标签是用来指定当前项目需要的依赖包

![](/IDEA-初始化-SSM-项目/idea64_8TW6xNmi4y.png)

可以发现，这个 Maven 模板自动引入了一个 junit 的依赖，通过这个依赖也可以看出单个依赖的引入格式

```xml
<dependency>
  <groupId>组名</groupId>
  <artifactId>项目名</artifactId>
  <version>版本号</version>
  <scope>作用范围</scope>
</dependency>
```

那我们如何能够获取到我们要引入的依赖的这些信息呢？

通过进入 maven 仓库的官方即可：https://mvnrepository.com/ (直接百度也可以搜索得到)

通过在该网站搜索 Spring 我们获得了以下这些内容

![](/IDEA-初始化-SSM-项目/msedge_iibB9JspQl.png)

点进我们需要的依赖里，如 spring core

![](/IDEA-初始化-SSM-项目/msedge_GksQTvBQFQ.png)

> 可以看到版本列表，和其所属的仓库，以及使用量，可以根据这些判断哪个版本较为稳定

点进你想要使用的版本

![](/IDEA-初始化-SSM-项目/msedge_G0xwF97n4w.png)

可以发现我们需要的 dependency 标签的内容，就在该页面上，直接点击一下文本框则会自动复制，粘贴到我们的 pom.xml 文件下的 dpendencies 标签里即可

![](/IDEA-初始化-SSM-项目/idea64_qULO4MWM0k.png)

同样，编写完后，应用引入依赖的时候要点一下右下角弹框的 Import Changes

2. 继续完成其他 SSM 依赖的添加

SSM 需要添加的依赖有：

- spring-core

  这是 Spring 框架的核心工具类，Spring 其他组件都要用到这个包里的类，是其他组件的基本核心

- spring-beans

  这是所有引用都要用到的，它包括了 Spring IoC 和 DI 操作的所有相关类

- spring-context

  为 Spring  核心提供了大量扩展

- spring-jdbc

  包含 Spring 对 JDBC 数据封装的所有类

- spring-tx

  为 JDBC、Hibernate、JDO、JPA 等提供的一致的声明式和编程式事务管理

- spring-web

  包含 Web 应用开发时，整合 Spring 框架所需的核心类

- spring-webmvc

  包含 Spring MVC 框架相关的所有类

- spring-test

  Spring test 对 Junit 等测试框架的简单封装

- javax.servlet-api

  开发 Servlet 必备

- mybatis

  数据持久层 Mybatis 框架的所有类

- mybatis-spring

  用于整合 Spring 与 Mybatis

- mysql-connect-java

  mysql 数据库的驱动类，如果使用的是其它数据库，需要下载其他数据库的驱动类

要注意的是，Spring 相关的依赖，版本需要保持一致

下面是添加完所有依赖的示例（版本可以不一致）

```xml
<properties>
    <spring.version>5.2.4.RELEASE</spring.version>
</properties>

<dependencies>
    <!-- 测试类 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- 日志类 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <!-- Spring -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-tx</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>${spring.version}</version>
        <scope>test</scope>
    </dependency>
    <!-- Servlet web -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
    </dependency>
    <!-- MyBatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.2</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.1</version>
    </dependency>
    <!-- 数据库驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>
</dependencies>
```

> 在 dependency 标签中，版本号之所以可以使用 ${spring.version}，使用因为其已经在 properties 标签下进行了定义，可以通过这种方法来保持 Spring 相关的依赖版本一致，减少后期若需要修改 版本的工作量

3. 点击 Import Changes，Maven 会自动将依赖的 jar 包下载到本地，并引入到项目当中去，若依赖已下载过，会直接使用本地的 jar 包，在新项目使用这些依赖就不需要重新下载了，速度很快

### Step. 4 配置 Tomcat

1. 在这里假定你已经安装了 Tomcat 应用在本地，若没有的话请看相关的 Tomcat 配置文章，或者百度完成
2. 点击 IDEA 右上角的 Add Configuration... 

![](/IDEA-初始化-SSM-项目/idea64_HerY9yqg7U.png)

3. 添加 Tomcat

![](/IDEA-初始化-SSM-项目/idea64_BMnpKEXmfg.png)

4. 给该配置起一个名字，若没有配置过 Tomcat 或没有被 IDEA 自动识别到，点击 ② 进行配置

![](/IDEA-初始化-SSM-项目/idea64_EYDdJs5JDf.png)

（以下为没有配置过 Tomcat 才需要的操作，若已完成，跳到下一步）

点击 ① 的加号，配置 Tomcat 地址

![](/IDEA-初始化-SSM-项目/idea64_TGl3BmN5hk.png)

指定一下 Tomcat 的目录，IDEA 会自动识别

![](/IDEA-初始化-SSM-项目/idea64_Nko6MZLYOD.png)

5. 给 Tomcat 部署 Artifact

![](/IDEA-初始化-SSM-项目/idea64_7ee2W5nyKG.png)

![](/IDEA-初始化-SSM-项目/idea64_VWCgOQh2IA.png)

6. 可以在如下配置一下该应用的 context，也就是 URL 的起始路径

![](/IDEA-初始化-SSM-项目/idea64_XRtL8Ehucg.png)

到这里，你就完成了 SSM 项目的创建，点击运行，等待一段时间后，即可看到默认的 Hello World! 页面

下面是一些框架相关的配置，测试我们的项目搭建情况

### Step.5 框架简单的基础配置及运行测试

下面使用一个简单的实例来检测项目配置的情况，需要对应的框架知识才能够看懂。

该项目除了上面提到要引入的包，这里还多引入了一个数据库连接池 c3p0，但是这个数据库连接池已经有更好的，如 HikariCP 和 Alibaba 的 Druid，但这里只是作为一个简单的示例，随便使用了一个

```xml
<dependency>
    <groupId>c3p0</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.1.2</version>
</dependency>
```

除此之外，为了能让 Controller 自动将对象转换成 JSON 格式，我们还需要引入一个 Jackson 的依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.10.2</version>
</dependency>
```

1. 建立对应的目录

![](/IDEA-初始化-SSM-项目/idea64_lJUgxDGF1Q.png)

2. 配置 Mybatis

在 resources 目录下，新建 mybatis-config.xml 配置文件，并向里面添加如下内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 配置全局属性 -->
    <settings>
        <!-- 使用jdbc的getGeneratedKeys获取数据库自增主键值 -->
        <setting name="useGeneratedKeys" value="true" />

        <!-- 使用列标签替换列别名 默认:true -->
        <setting name="useColumnLabel" value="true" />

        <!-- 开启驼峰命名转换:Table{create_time} -> Entity{createTime} -->
        <setting name="mapUnderscoreToCamelCase" value="true" />
    </settings>

</configuration>
```

3. 配置 logback

在 resources 目录下，新建 logback.xml 配置文件，并向里面添加如下内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true" scanPeriod="60 seconds" debug="false">
    <!-- 定义参数常量 -->
    <!-- TRACE<DEBUG<INFO<WARN<ERROR -->
    <!-- logger.trace("msg") logger.debug... -->
    <property name="log.level" value="debug" />
    <property name="log.maxHistory" value="30" />
    <property name="log.filePath" value="${catalina.base}/logs/webapps" />
    <property name="log.pattern"
              value="%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n" />
    <!-- 控制台设置 -->
    <appender name="consoleAppender" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
    </appender>
    <!-- DEBUG -->
    <appender name="debugAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 文件路径 -->
        <file>${log.filePath}/debug.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 文件名称 -->
            <fileNamePattern>${log.filePath}/debug/debug.%d{yyyy-MM-dd}.log.gz
            </fileNamePattern>
            <!-- 文件最大保存历史数量 -->
            <maxHistory>${log.maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>DEBUG</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>
    <!-- INFO -->
    <appender name="infoAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 文件路径 -->
        <file>${log.filePath}/info.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 文件名称 -->
            <fileNamePattern>${log.filePath}/info/info.%d{yyyy-MM-dd}.log.gz
            </fileNamePattern>
            <!-- 文件最大保存历史数量 -->
            <maxHistory>${log.maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>INFO</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>
    <!-- ERROR -->
    <appender name="errorAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 文件路径 -->
        <file>${log.filePath}/erorr.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 文件名称 -->
            <fileNamePattern>${log.filePath}/error/error.%d{yyyy-MM-dd}.log.gz
            </fileNamePattern>
            <!-- 文件最大保存历史数量 -->
            <maxHistory>${log.maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>
    <logger name="com.imooc.o2o" level="${log.level}" additivity="true">
        <appender-ref ref="debugAppender"/>
        <appender-ref ref="infoAppender"/>
        <appender-ref ref="errorAppender"/>
    </logger>
    <root level="info">
        <appender-ref ref="consoleAppender"/>
    </root>
</configuration>
```

4. 配置 Spring

在 resources 目录下，新建文件 jdbc.properties 用于配置 数据库连接

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/<数据库名称>?useUnicode=true&characterEncoding=utf8&serverTimezone=UTC
jdbc.username=<此处填写你的数据库用户名>
jdbc.password=<此处填写你的数据库密码>
```

在 resources/spring 目录下，配置 Spring

首先是数据库持久层 DAO：

spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 配置整合mybatis过程 -->
    <!-- 1.配置数据库相关参数properties的属性：${url} -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!-- 2.数据库连接池 -->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <!--配置连接池属性-->
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="user" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>

        <!-- c3p0连接池的私有属性 -->
        <property name="maxPoolSize" value="40"/>
        <property name="minPoolSize" value="10"/>
        <!-- 关闭连接后不自动commit -->
        <property name="autoCommitOnClose" value="false"/>
        <!-- 获取连接超时时间 -->
        <property name="checkoutTimeout" value="10000"/>
        <!-- 当获取连接失败重试次数 -->
        <property name="acquireRetryAttempts" value="2"/>
    </bean>

    <!-- 3.配置SqlSessionFactory对象 -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 注入数据库连接池 -->
        <property name="dataSource" ref="dataSource"/>
        <!-- 配置MyBaties全局配置文件:mybatis-config.xml -->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <!-- 扫描entity包 使用别名 -->
        <property name="typeAliasesPackage" value="org.example.ssm.sample.pojo"/>
        <!-- 扫描sql配置文件:mapper需要的xml文件 -->
        <property name="mapperLocations" value="classpath:mapper/*.xml"/>
    </bean>

    <!-- 4.配置扫描Dao接口包，动态实现Dao接口，注入到spring容器中 -->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!-- 注入sqlSessionFactory -->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
        <!-- 给出需要扫描Dao接口包 -->
        <property name="basePackage" value="org.example.ssm.sample.mapper"/>
    </bean>
</beans>
```

> 若直接使用这个配置，
>
> 1. 要注意把 `sqlSessionFactory` Bean 中的别名属性 `typeAliasesPackage` 改为你自己存放 POJO 目录的包名
> 2. 要注意把 MapperScannerConfigurer Bean 中的 `basePackage` 属性改为你自己存放 mapper 接口目录 的包名
> 3. Mapper 的 xml 文件要放在 resources 下的 mapper 文件夹下，否则自行修改 `sqlSessionFactory` Bean 中的 `mapperLocations` 属性

其次是 Service 层：

spring-service.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/tx
    http://www.springframework.org/schema/tx/spring-tx.xsd">
    <!-- 扫描service包下所有使用注解的类型 -->
    <context:component-scan base-package="org.example.ssm.sample.serivce" />

    <!-- 配置事务管理器 -->
    <bean id="transactionManager"
          class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!-- 注入数据库连接池 -->
        <property name="dataSource" ref="dataSource" />
    </bean>

    <!-- 配置基于注解的声明式事务 -->
    <tx:annotation-driven transaction-manager="transactionManager" />
</beans>
```

> 若直接使用这个配置。
>
> 要注意把 `context:component-scan` 标签下的 `base-package` 属性改为你存放 service 类的包名

接着是 Controller 层：

spring-controller.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/mvc
    http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd">
    <!-- 配置SpringMVC -->
    <!-- 1.开启SpringMVC注解模式 -->
    <mvc:annotation-driven />

    <!-- 2.静态资源默认servlet配置 (1)加入对静态资源的处理：js,gif,png (2)允许使用"/"做整体映射 -->
    <mvc:resources mapping="/resources/**" location="/resources/" />
    <mvc:default-servlet-handler />

    <!-- 3.定义视图解析器 -->
    <bean id="viewResolver"
          class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/html/"></property>
        <property name="suffix" value=".html"></property>
    </bean>

    <!-- 4.扫描web相关的bean -->
    <context:component-scan base-package="org.example.ssm.sample.controller" />

</beans>
```

> 若直接使用这个配置，
>
> 要注意把 `context:component-scan` 标签下的 `base-package` 属性改为你存放 controller 类的包名

接下来，为了要让 Spring MVC 框架能够读取到配置，而且 tomcat 的请求能够交给 Spring 框架处理，要进行如下配置

进入 webapp/WEB-INF 目录下，打开 web.xml 文件

```xml
<!DOCTYPE web-app PUBLIC
        "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
        "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1" metadata-complete="true">

    <display-name>Archetype Created Web Application</display-name>
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>index.html</welcome-file>
    </welcome-file-list>

    <servlet>
        <servlet-name>spring-dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring/spring-*.xml</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>spring-dispatcher</servlet-name>
        <!-- 默认匹配所有的请求 -->
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```

> 在其 init-param 中设置了将 resources/spring 目录下 spring- 开头的文件设置为配置文件
>
> 在 servlet-mapping 中将所有请求交给了 Spring Web 进行处理

5. 建立数据库

我们简单的用一个用户表来测试，下面是建表语句

```sql
create database ssm;
use ssm;
create table tb_user(
    id int auto_increment not null,
    username varchar(50) not null,
    password varchar(50) not null,
    primary key(`id`)
);
```

6. 自底向上开发应用

首先是模型层 POJO：

org.example.ssm.sample.pojo.User

```java
public class User {
	private Integer id;
    private String username;
    private String password;
    public User() {}
    // getter and setter
}
```

其次是 DAO 层，先从 Mapper 的接口开始：

org.example.ssm.samle.mapper.UserMapper

```java
public interface UserMapper {
	int addUser(User user);
    User queryByUsername(String username);
}
```

很简单，就两个接口，用于登录和注册，然后完成 xml 文件的编写：

resources/mapper/UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.example.ssm.sample.mapper.UserMapper">
    <insert id="addUser" parameterType="User">
        insert
        into tb_user(username, password)
        values (#{username}, #{password})
    </insert>
    <select id="queryByUsername" parameterType="String" resultType="User">
        select *
        from tb_user
        where username = #{username}
    </select>
</mapper>
```

接下来就到 Service 层了，因为这里业务比较简单，直接将 DAO 层的东西返回出去即可：

org.example.ssm.sample.service.UserService

```java
public interface UserService {
    int addUser(User user);
    User queryByUsername(String username);
}
```

org.example.ssm.sample.service.impl.UserServiceImpl

```java
@Service
public class UserServiceImpl extends UserService {
    
    @Autowired
    private UserMapper userMapper;
    
    @Override
    public int addUser(User user) {
        return userMapper.addUser(user);
    }

    @Override
    public User queryByUsername(String username) {
        return userMapper.queryByUsername(username);
    }
}
```

要记得加上 Service 注解，这样才能被 spring 扫描到。

然后最后就是 Controller 层了：

org.example.ssm.sample.controller.UserController

```java
@Controller
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/hello")
    @ResponseBody
    public String hello() {
        return "Hello";
    }

    @PostMapping("/login")
    @ResponseBody
    public Map<String, Object> login(String username, String password) {
        Map<String, Object> result = new HashMap<>();
        
        // 判空处理
        if (username == null || username.equals("")) {
            result.put("msg", "username 不能为空！");
            return result;
        }
        if (password == null || password.equals("")) {
            result.put("msg", "password 不能为空！");
            return result;
        }
        
        User user = userService.queryByUsername(username);
        
        if (password.equals(user.getPassword())) {
            result.put("status", "success");
            return result;
        }
        result.put("status", "wrong password");
        return result;
    }

    @PostMapping("/reg")
    @ResponseBody
    public Map<String, Object> reg(String username, String password) {
        Map<String, Object> result = new HashMap<>();

        // 判空处理
        if (username == null || username.equals("")) {
            result.put("msg", "username 不能为空！");
            return result;
        }
        if (password == null || password.equals("")) {
            result.put("msg", "password 不能为空！");
            return result;
        }
        
        // 构建对象
        User user = new User();
        user.setUsername(username);
        user.setPassword(password);
        
        int i = userService.addUser(user);
        if (i == 0) {
            result.put("status", "error");
            return result;
        }
        result.put("status", "success");
        return result;
    }
}
```

7. 测试应用

首先掏出神器 PostMan，或者如果没有 PostMan 可以使用 `curl` 命令进行测试

一共三个接口

- /hello 输出一段 hello 字符串  `curl http://localhost:8080/ssm_sample/hello`
- /reg 传入用户名和密码，注册账户`curl -d'username=emma＆password=123'-X POST http://localhost:8080/ssm_sample/reg`
- /login 传入用户名和密码，登录账户`curl -d'username=emma＆password=123'-X POST http://localhost:8080/ssm_sample/login`

![](/IDEA-初始化-SSM-项目/Postman_JwL5eolvoC.png)

![](/IDEA-初始化-SSM-项目/Postman_r0TcgsnGTn.png)

![](/IDEA-初始化-SSM-项目/Postman_cicaBUjqJm.png)

可以发现都能够成功运行

*本教程完结*