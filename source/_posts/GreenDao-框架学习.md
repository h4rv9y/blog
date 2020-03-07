---
title: GreenDao 框架学习
date: 2019-04-03 21:01:58
categories: [Dev, Android]
tags:
  - Green Dao
  - 教程
  - Android
toc: true
---

## GreenDao 是什么？

![img](GreenDao-框架学习/GreenDao_01.png)

GreenDao 是一个开源的Android ORM(对象/关系映射)，通过ORM，在我们数据库开发中节省了开发时间。这篇文章将会教会你如何配置目前最新版的 GreenDao 框架，且投入到开发工程中区。

<!-- more -->

# 相关资源

## GreenDao 的官方文档

- [官方网站](<http://greenrobot.org/greendao/>)
- [官方使用文档](<http://greenrobot.org/greendao/documentation/>)
- [GitHub地址](<https://github.com/greenrobot/greenDAO>)
- [SQLChipher for Android 官方说明地址](<https://www.zetetic.net/sqlcipher/sqlcipher-for-android/>)

## GreenDao的作用

通过GreenDao，我们可以快速的操作数据库，我们可以用简单的面向对象的API来储存、更新、删除和查询Java对象。

## 目前主流的框架

- OrmLite
- SugarORM
- LitePal
- GreenDao

## 为什么选择GreenDao？

1. 高性能：官方声称是目前主流框架中运行效率最高的

2. 文档数量多
3. 较为流行
4. 使用便捷
5. 支持数据库加密：SQLCipher，以确保用户数据安全

# 配置

## 导入相关插件

要在Android项目中使用GreenDao，您需要添加GreenDao Gradle插件并添加GreenDao库：

### 1. 导入插件

```groovy
// 在 Project 的 build.gradle 文件中添加
buildscript {
    repositories {
        jcenter()
        mavenCentral() // add repository
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.2'
        classpath 'org.greenrobot:greendao-gradle-plugin:3.2.2' // add plugin
    }
}
```

### 2. 配置相关依赖

```groovy
// 在 Moudle:app 的 build.gradle 文件中添加
apply plugin: 'com.android.application'
apply plugin: 'org.greenrobot.greendao' // apply plugin

dependencies {
    implementation 'org.greenrobot:greendao:3.2.2' // add library
}
```

<a name="to3"></a>

### 3. 配置数据库的相关信息

   此处是可选项，不配置的话默认会生成在 build 目录下。

```groovy
greendao {
    schemaVersion 1 //数据库版本号
    daoPackage 'com.aserbao.aserbaosandroid.functions.database.greenDao.db'
// 设置DaoMaster、DaoSession、Dao 包名
    targetGenDir 'src/main/java'				//设置DaoMaster、DaoSession、Dao目录
    generateTests false 						 		//设置为true以自动生成单元测试。
    targetGenDirTests 'src/main/java'	 //应存储生成的单元测试的基本目录。默认为 src / androidTest / java。
}
```

### 4. 创建储存对象实体类

使用GreenDao存储数据只需要在存储数据类前面声明@Enitity注解就能让GreenDao为其生成必要的代码

```java
@Entity
public class staff {
  @Id(autoincrement = true)
  private Long id;									//自动增长的id
  @Unique
  private String name;							//姓名
  private String sex;								//性别
  private String telPhone;					//电话号码
  private String address;						//住址
  private int age;									//年龄
  private int staffNum;							//工号
  //相应的 getter 和 setter 方法
}
```

### 5. 相关注解说明：

- 实体@Entity注解

> schema: 告知GreenDao当前实体属于哪个schema
>
> active: 标记一个实体处于活跃状态，活动实体有更新、删除和刷新方法
>
> nameInDb: 在数据库中使用的别名，默认使用的是实体的类名
>
> indexes: 定义索引，可以跨越多个列
>
> createInDb:标记创建数据库表

- 基础属性注解

> @Id: 主键 Long 型，可以通过@Id(autoincrement = true)设置自增长
>
> @Property: 设置一个非默认关系映射所对应的列名，默认是使用字段名，例如：@Property(nameInDb = "name")
>
> @NotNull: 设置数据库表当前列不能为空
>
> @Transient: 添加此标记后不会生成数据库表的列

- 索引注解

> @Index: 使用@Index作为一个属性来创建一个索引，通过name设置索引别名，也可以通过unique给索引添加约束
>
> @Unique: 向数据库添加了一个唯一的约束

- 关系注解

> @ToOne: 定义与另一个实体(一个实体对象)的关系
>
> @ToMany: 定于与多个实体对象的关系

当我们编写好实体类并添加自己需要的注解之后，点击 *Make Project* 或者 *Make Module 'app'* ，就会在项目的  build 目录下或者自己设定的目录下看到生成的三个类文件：

- DaoMaster
- DaoSession
- StaffDao

后面的数据库操作需要借助这三个类进行，同时在我们的实体中自动生成了各个属性的get、set方法

## 初始化GreenDao

安卓在Application中可以维持一个全局的会话，它的生命周期是从app开启到终止。我们希望数据库在应用打开的时候就被初始化，所以我们在Application进行数据库的初始化操作。

### 1. 重写Application类

先建立一个Application的子类，这里我写了一个BaseApplication的类，并继承了Application类，且重写了onCreate()方法，在里面添加了初始化数据库的相关语句。

```java
public class BaseApplication extends Application {
  	
  	private DaoSession daoSession;
	private DaoMaster daoMaster;
	private DaoMaster.DevOpenHelper helper;
	private SQLiteDatabase db;
  
  	@Override
  	public void onCreate(){
  		super.onCreate();
   		//调用初始化数据库方法
      	initGreenDaoDatabase();
  	}
  	/**
  	 * 初始化数据库
  	 */
  	public void initGreenDaoDatabase() {
      	//1. 创建数据库 People.db
  		helper = new DaoMaster.DevOpenHelper(this, "People.db");
      	//2. 获取可写数据库
  		db = helper.getWritableDatabase();
      	//3. 获取数据库对象
  		daoMaster = new DaoMaster(db);
      	//4. 获取dao对象管理者
  		daoSession = daoMaster.newSession();
  	}
  
    /**
     * 获取数据库的dao对象管理者
     * @return dao对象管理者
     */
  	public DaoSession getDaoSession() {
 		return daoSession;
	}
}
```

可以看见在上面的代码中，我还写了一个getDaoSession()的方法，是用于获取daoSession这个对象管理者，在后面对数据库操作有重要作用

### 2. 注册新的Application

新建完这个BaseApplication的类后，记得要在AndroidManifest.xml文件去注册一下，只要加一下下面标注的那一行代码即可

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.lwh.greendaotest1">

    <application
        android:name=".BaseApplication"      //！记住要加上这行代码 
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

初始化完成之后记得build一下项目，会发现设置的targetGenDir(<a href="#to3">前面配置数据库的目录</a>))的目录下生成三个类文件，这个是GreenDao自动生成的。说明数据库已经连接好了，我们接下来只需要进行数据库的增删改查操作就行咯。

## 使用

## CRUD 基础操作

### 1.增(Create)

- **insert(Staff entity)** 插入数据

- **insertOrReplace(Staff entity)** 数据存在则替换，不存在则插入

Staff 是上文所创建的 Staff 这个类，这里只要传入你要插入的你所定义的类的对象即可。

```java
//示例代码
public void addStaff () {
  	daoSession = ((BaseApplication) getApplication()).getDaoSession();
  	StaffDao staffDao = daoSession.getStaffDao();
  
  	Staff staff = new Staff();
  	staff.setName("张三");
  	staff.setSex("男");
  	staff.setTelPhone("13712345678");
  	staff.setAddress("广东省广州市花都区XX花园X栋XXX房");
  	staff.setAge(23);
  	staff.setStaffNo(1);
  	
  	staffDao.insert(staff);						//插入数据
  	//staffDao.insertOrReplase(staff);          //数据存在则替换，数据不存在则插入
}
```

### 2. 删(Delete)

- **deleteBykey(Long key)**  根据主键删除一条记录
- **delete(Staff entity)** 根据实体类删除一条信息，一般结合查询方法，查询出一条记录后删除。
- **deleteAll()** 删除所有记录

```java

```

### 3. 改(Update)

- **update(Staff entity)** 更新一条记录

```java
public void updateStaff(Staff staff) {
  	daoSession = ((BaseApplication) getApplication).getDaoSession();
  	StaffDao staffDao = daoSession.getStaffDao();
  	
  	staff.setName("李四");
  	staffDao.update(staff);
}
```

### 4. 查(Retrieve)

- **loadAll()** 查询所有数据
- **queryRaw()** 根据条件查询
- **queryBuilder()** 方便查询的创建，后面会有详解

```java
//loadAll()示例
public List queryAll() {
  	List<Staff> staffs = staffDao.loadAll(Staff.class);
  	return staffs;
}
```

```java
//queryRaw()示例
@Override
public List queryData(String str) {
  	List<Staff> staffs = staffDao.queryRaw(Staff.class, "where id = ?", str);
  	return staffs;
}
```

## QueryBuilder 详解

### QueryBuilder的使用方法
*未完待续*