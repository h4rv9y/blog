---
title: Spring IoC
date: 2020-03-16 15:05:33
categories: [Dev, Java]
tags:
    - Java
    - Spring
    - IoC
    - Handbook
    - 教程
toc: true
---

### ApplicationContext 的创建

1. 通过 ClassPathXmlApplicationContext 创建

`ClassPathXmlApplicationContext` 将从 **classpath** 中寻找指定的 XML 配置文件

- 若为 *maven* 项目，则放在 resource 文件夹下
- 若为普通 IDEA 项目，则放在项目根目录下

```java
public static void main(String[] args) {
    ApplicationContext ctx = 
        new ClassPathXmlApplicationContext("applicationContext.xml");
}
```

---

2. 通过 FileSystemXmlApplicationContext 创建

`FileSystemXmlApplicaitonContext` 将从文件系统中**根据文件路径**寻找 XML 配置文件

```java
public static void main(String[] args) {
    ApplicationContext ctx = 
        new FileSystemApplicationContext("/home/lwh/IdeaProject/sample-dev/application.xml")
}
```

3. 通过 Web 服务器实例化 ApplicationContext 容器
   - 先将 `spring-web` jar 包放在 **WEB-INF/lib** 目录下
   - 配置 **web.xml** 文件

```xml
<!-- web.xml 中追加以下代码 -->
<context-param>
    <!-- 加载 src 目录下的 applicationContext.xml 文件 -->
    <param-name>contextConfigLocation</param-name>
    <param-value>
        classpath:applicationContext.xml
    </param-value>
</context-param>
<!-- 指定以 ContextLoaderListener 方式启动 Spring 容器 -->
<listener>
    <listener-class>
        org.springframework.web.context.ContextLoaderListener
    </listener-class>
</listener>
```

### 依赖注入

示例类

```java
public class Person {
    private String name;
    private int age;
    private double height;
    
    public Person() {}
    public Person(String name, int age, double height) {
        this.name   = name;
        this.age    = age;
        this.height = height;
    }
    /* Getter and Setter methods */
}
```

---

1. 使用构造方法注入

```xml
<bean id="person" class="com.example.pojo.Person">
    <constructor-arg index="0"      value="John" />
    <constructor-arg name="age"     value="20" />
    <constructor-arg type="double"  value="1.75" />
</bean>
```

定位属性：

- `index`：使用构造方法参数的**索引**定位
- `name`：使用构造方法参数的**标识符**定位
- `type`：使用构造方法参数的**类型**按顺序定位

赋值属性：

- `value`：赋值静态**基本类型**
- `ref`：赋值对象类型，值只能为 **Spring Bean**

---

2. 使用属性注入

```xml
<bean id="person" class="com.example.pojo.Person">
    <property name="name"    value="John" />
    <property name="age"     value="20" />
    <property name="height"  value="1.75" /> 
</bean>
```

定位属性：

- `name`：根据**属性标识符**定位

赋值属性：

- `value`：赋值静态**基本类型**
- `ref`：赋值对象类型，值只能为 **Spring Bean**

>**`ref` 属性示例：**
>
>新增 IPhone 类
>
>```java
public IPhone extends Phone {}
>```
>
>向 Person 类新增 usingPhone 属性
>
>```java
public Person {
    // 新增的属性
    private Phone usingPhone;
    // Setter 方法
    public void setUsingPhone(Phone phone) {
        this.usingPhone = phone;
    }
}
>```
>
>在 XML 中配置注入
>
>```xml
<beam id"iPhone" class="com.example.pojo.IPhone" />
<bean id="person" class="com.example.pojo.Person">
    <property name="usingPhone" ref="iPhone" />
</bean>
>```
>
>这样 `person` bean 就会有一个 IPhone 实例注入到 usingPhone 属性中

### Bean 的实例化

1. 构造方法注入

*同上方依赖注入的第一点*

---

2. 静态工厂注入

静态工厂类：

```java
public class PersonStaticFactory {
    private static Person instance = new Person();
    public static Person getInstance() {
        return this.instance;
    }
}
```

Bean 配置：

```xml
<bean id="person" 
      class="com.example.factory.PersonStaticFactory" 
      factory-method="getInstance" />
```

- 指定 `class` 为**工厂类**
- 指定 `factory-method` 为**工厂类中获取实例的方法**

---

3. 实例工厂注入

实例工厂类：

```java
public class PersonInstanceFactory {
    public Person getInstance() {
        return new Person;
    }
}
```

Bean 配置：

```xml
<bean id="personInstanceFactory"
      class="com.example.factory.PersonInstanceFactory" />
<bean id="person"
      factory-bean="personInstanceFactory"
      factory-method="getInstance" />
```

- 先配置工厂类的 Bean
- 将目标 Bean 的 factory-bean 指定**刚配置的工厂 Bean**
- 将目标 Bean 的 factory-method 指定工厂类中**获取实例的方法**

### Bean 的作用域

1. Singleton 单例作用域

```xml
<bean id="person" 
      class="com.example.pojo.Person" 
      scope="singleton" />
<!-- 或 -->
<bean id="person" class="com.example.pojo.Person" />
```

> Spring IoC 容器的默认 Bean 作用域就为 **singleton**
>
> 当作用域为 Singleton 时，Spring IoC 容器仅生成和管理一个 Bean 实例，在使用 id 或者 name 获取 Bean 实例时，IoC 容器将返回共享的 Bean 实例

2. Prototype 作用域

```xml
<bean id="person"
      class="com.example.pojo.Person"
      scope="prototype" />
```

> 当作用域为 Prototype 时，Spring IoC 容器将为每次请求创建一个新的实例

### Bean XML 装配集合属性

示例类

```java
public class ComplexBean {
    private String[] users;
    private List<String> hobbyList;
    private Set<String> aliasSet;
    private Map<String, String> residenceMap;
    /* Getter and Setter methods */
}
```

---

1. 数组属性

```xml
<bean id="complexBean" class="com.example.pojo.ComplexBean">
    <property name="users">
        <array>
            <value>John</value>
            <value>Victor</value>
            <value>Brian</value>
        </array>
    </property>
</bean>
```

2. List 列表属性

```xml
<bean id="complexBean" class="com.example.pojo.ComplexBean">
    <property name="hobbyList">
        <list>
            <value>Singing</value>
            <value>Gaming</value>
            <value>Climbing</value>
        </list>
    </property>
</bean>
```

3. Set 集合属性

```xml
<bean id="complexBean" class="com.example.pojo.ComplexBean">
    <property name="aliasSet">
        <set>
            <value>Bob 100</value>
            <value>Bob 101</value>
            <value>Bob 102</value>
        </set>
    </property>
</bean>
```

4. Map 字典属性

```xml
<bean id="complexBean" class="com.example.pojo.ComplexBean">
    <property name="residenceMap">
        <map>同上依赖注入第一点
            <entry key="Guangzhou"  value="广州" />
            <entry key="Shanghai"   value="上海" />
            <entry key="Beijing"    value="北京" />
            <entry key="Shenzhen"   value="深圳" />
        </map>
    </property>
</bean>
```

> 以上四种类型，使用方式都是一致的，
>
> 先通过定位属性 `name` 定位
>
> 然后在 `property` 标签内定义各类型的标签，如 `list`、`array`、`map`、`set`
>
> 再在其对应标签通过 `value`、`ref`、`entry` 标签赋值
>
> 使用构造方法的方式进行装配也是一致的，可以通过 constructor-arg 的 `index`、`type`、`name` 属性进行定位

### Bean 通过注解装配

开启注解扫描

```xml
<context:component-scan 
    base-package="com.example"/>
```

1. @Component

该注解将标注的类添加进 **Spring IoC 容器**当中，若不指定名称，则 Bean 的名称自动改为**首字母小写**的类名

2. @Repository

该注解用于标注一个**数据访问层**的类（DAO），其功能与 @Component 相同

3. @Service

该注解用于标注一个**业务逻辑层**的类（Service），其功能与 @Component 相同

4. @Controller

该注解用于标注一个**控制层**的类（Controller），其功能与 @Component 相同

5. @Value

该注解用于**简单静态基本类型**的值注入到属性中

6. @Autowired

该注解用于自动将**类型相同**的 Bean 装配到标注属性

7. @Resource

该注解与 @Autowired 类似，区别在于该注解是根据**名称**来装配注入的，只有当找不到名称匹配的 Bean 时，才**使用类型相同**的 Bean 进行装配，该注解有两个属性：

- `name`：指定 Bean 实例的名称
- `type`：指定 Bean 实例的类型

8. @Qualifier

该注解需要配合 @Autowired 使用，当 @Autowired 需要按照名称来注入的时候需要该注解指定名称，该两者标签与 @Resource 有语义上的区别，前者是先通过 @Autowired 根据类型缩小范围，再通过 @Qualifier 匹配名称相同的 Bean，而后者是直接通过名称进行匹配

---

示例：

```java
@Component("person")
public class Person {
    @Value("Natalie")
    private String name;
    @Valie("18")
    private int age;
    @Value("1.67")
    private double height;
    
    @Autowired
    @Qualifier("iPhone")
    private Phone usingPhone;
    
    /* Getter and Setter method */
}
```

*Repository、Service、Controller 同理* 

### Bean 实例获取

根据 ApplicationContext 对象获取

```java
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx =
            new ClassPathXmlApplicationContext("applicationContext.xml");
        // 通过 Bean 的名称获取
        Person person = (Person) ctx.getBean("person");
    }
}
```