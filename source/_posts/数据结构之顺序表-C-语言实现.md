---
title: 数据结构之顺序表 C 语言实现
date: 2019-11-29 00:59:48
categories: [Dev, Data Structure]
tags:
    - Data Structures
    - 顺序表
    - Sequential List
toc: true
---
## 顺序表的定义

```c
typedef int dataType;
const int capacity = 100;
typedef struct {
  dataType data[capacity];
  int size;
} SQList;
```

- 第一行中，用于给 dataType 定义成 int 类型，如果想将顺序表改成存储其他类型的元素，可将 int 改成其他类型。
- 第二行中，capacity 常量用于定义数组的容量，也就是顺序表的容量，因为数组在定义时就要确定其大小，且不能够动态改变。
- 第三行的结构体中，data[] 即为顺序表的容器，用于存储结点元素，size 用于表示顺序表目前所存储的元素个数，且将该结构体起了个 SQList (Sequential List) 的别名。

## 顺序表中的基本运算

首先来看看我们要实现的一些基本函数：

```c
int add(SQList *sqlist, dataType e, int index);		// 增加结点到指定索引
int get(SQList *sqlist, dataType *e, int index); 	// 获取指定索引处的结点元素的值
int set(SQList *sqlist, dataType e, int index);		// 设置指定索引处的结点元素的值
int remove(SQList *sqlist, int index);				// 删除指定位置的结点
```

基本上就是增删改查。

### 增加结点

首先先来看看增加结点的代码实现：

```c
int add(SQList *sqlist, dataType e, int index)
{
  // 首先先判断索引是否合法
  if (index > sqlist->size || index < 0)
  {
    printf("增加结点失败，指定索引超出范围！");
    return -1;
  }
  // 其次判断顺序表结构中数组是否已满
  if (size == capacity)
  {
    printf("增加结点失败，顺序表已满");
    return -1;
  }
  // 下面是增加结点的功能实现
  // 1. 先将从指定索引处开始的元素向后移动一位，以提供一个位置插入元素
  for (int i = size; i > index; --i)
  {
    sqlist->data[i] = sqlist->data[i - 1];
  }
  // 2. 将用户传入的元素赋值给指定位置
  sqlist->data[i] = e;
  // 3. 维护顺序表中的 size 变量
  ++ sqlist->size;
  return 1;
}
```

### 获取结点

获取结点是顺序表中基本运算最简单的之一，只需要做相应的判断，直接将指定索引处的值取出即可，这也是顺序表的一个优点，获取指定位置的元素效率非常的快。以下是代码实现：

```c
int get(SQList *sqlist, dataType *e, int index)
{
  // 首先先判断索引是否合法
  if (index >= sqlist->size || index < 0)
  {
    printf("获取结点失败，指定索引超出范围！");
    return -1;
  }
  // 将指定索引处的值通过指针传递给变量
  *e = sqlist->data[index];
  return 1;
}
```

### 设置结点

设置结点的算法跟获取结点的算法类似，也是非常简单，执行效率也是非常快。以下是代码实现：

```c
int set(SQList *sqlist, dataType e, int index)
{
  // 首先判断索引是否合法
  if (index >= sqlist->size || index < 0)
  {
    printf("设置结点失败，指定索引超出范围！");
    return -1;
  }
  // 将指定位置处的值设置为用户传入的值
  sqlist->data[index] = e;
  return 1;
}
```

### 删除结点

```c
int remove(SQList *sqlist, int index)
{
  // 首先判断索引是否合法
  if (index >= sqlist->size || index < 0)
  {
    printf("删除结点失败，指定索引超出范围！");
    return -1;
  }
  // 下面是删除结点的实现
  // 1. 将从索引处后面一个结点开始依次向前覆盖
  for (int i = index; i < sqlist->size - 1; ++i)
  {
    sqlist->data[i] = sqlist->data[i + 1];
  }
  // 2. 维护顺序表中的 size 变量
  -- sqlist->size;
  return 1;
}
```

## 跟顺序表有关的其他运算

### 根据元素定位结点

````c
int locate(SQList *sqlist, dataType e)
{
  // 遍历顺序表中的每个元素，且与用户传入的值进行比对
  for (int i = 0; i < sqlist->size; ++i)
  {
    if (sqlist->data[i] == e)
    {
      // 成功定位到结点，返回所在索引
      return i;
    }
	}
  // 找不到该元素，返回 -1 表示定位失败
  return -1;
}
````

### 反转顺序表中的元素

```c
void reverse(SQList *sqlist) {
  dataType tmp;
  // 两个索引在顺序表的两端，交换一次后向中间移动，直到相遇，即完成反转
  for (int i = 0, j = sqlist->size - 1; i < j; ++i, --j) {
    // 交换两个结点的元素
    tmp = l->data[i];
    sqlist->data[i] = sqlist->data[j];
    sqlist->data[j] = tmp;
  }
}
```

