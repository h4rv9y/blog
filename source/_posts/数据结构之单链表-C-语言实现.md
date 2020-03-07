---
title: 数据结构之单链表 C 语言实现
date: 2019-11-29 01:03:26
categories: [Dev, Data Structure]
tags:
    - Data Structures
    - 顺序表
    - Linked List
toc: true
---
## 单链表的定义

```c
typedef int dataType;
typedef struct node* Pointer
struct node {
  dataType data;
  Pointer next;
};
typedef Pointer LKList;
```

## 单链表的基本运算

先来看看我们要实现的一些基本方法

```c
LKList initList();                                  // 初始化链表
int getSize(LKList head);	                        // 求表长
int add(LKList head, dataType e, int index);        // 在指定索引处插入结点元素
int get(LKList head, dataType *result, int index);	// 获取指定位置索引元素
int set(LKList head, dataType e, int index);		// 设置指定位置索引元素
int remove(LKList head, int index);					// 删除指定索引的结点元素
```

在本文中，单链表使用的是头插法来进行实现的，且使用了一个假的头结 (dummyHead) 点来简化代码实现，即 dummyHead 的下一个结点才为首结点。

### 初始化

```c
LKList initList()
{
	LKList head = NULL;
  head = (LKList) malloc(sizeof(node));
  head->next = NULL;
  return head;
}
```

### 求表长

```c
int getSize(LKList head)
{
  Pointer prev = head;
	int count = 0;
  while (prev->next != NULL)
  {
    ++ count;
    prev = prev->next;
  }
  return count;
}
```

### 插入结点

```c
int add(LKList head, dataType e, int index)
{
  Pointer prev = head;
  for (int i = 0; i < index; ++i)
  {
    prev = prev->next;
    if (prev == NULL)
    {
      printf("插入失败，索引无效！");
      return -1;
    }
	}
  Pointer newNode = (Pointer) malloc(sizeof(node));
  newNode->next = prev->next;
  prev->next = newNode;
}
```

### 获取结点

```c
int get(LKList head, dataType *result, int index)
{
  Pointer cur = head->next;
  for (int i = 0; i < index; ++i)
  {
    cur = cur->next;
    if (cur == NULL)
    {
      printf("获取结点失败，索引无效！");
      return -1;
    }
  }
  *result = cur->data;
  return 1;
}
```

### 设置结点

```c
int set(LKList head, dataType e, int index)
{
	Pointer cur = head->next;
  for (int i = 0; i < index; ++i)
  {
    cur = cur->next;
    if (cur == NULL)
    {
      printf("设置结点失败，索引无效!");
      return -1;
		}
	}
  cur->data = e;
  return 1;
}
```

### 删除结点

```c
int remove(LKList head, int index)
{
  Pointer prev = head;
  for (int i = 0; i < index; ++i)
  {
    prev = prev->next;
    if (prev == NULL)
    {
      printf("删除失败，索引无效！");
      return -1;
    }
	}
  Pointer tmp = prev->next;
  prev->next = tmp->next;
  free(tmp);
  return 1;
}
```

## 单链表一些方便的运算

```c
int getFirst(LKList head, dataType *result)
{
  return get(head, result, 0);
}
int getLast(LKList head, dataType *result)
{
  return get(head, result, getSize(head));
}
int setFirst(LKList head, dataTye e)
{
  return set(head, e, 0);
}
int setLast(Lklist head, dataType e)
{
  return set(head, e, getSize(head));
}
```

getLast() 和 setLast() 效率有点低，调用 getSize() 已经遍历了一遍链表，但 get() 方法中又遍历了一次，操作有点多余，下面将其改善一下：

```c
int getLast(LKList head, dataType *result)
{
  Pointer cur = head->next;
  if (cur == NULL)
  {
    printf("获取失败，顺序表为空！");
    return -1;
  }
  while (cur->next != NULL)
  {
    cur = cur->next;
	}
  *result = cur->data;
  return 1;
}

int setLast(LKList head, dataType e)
{
  Pointer cur = head->next;
  if (cur == NULL)
  {
    printf("设置失败，顺序表为空！");
    return -1;
  }
  while (cur->next != NULL)
  {
    cur = cur->next;
	}
  cur->data = e;
  return 1;
}
```

其实还可以在结构体外边再维护一个 size 变量，这样可以提高 getSize() 函数的效率，只是牺牲一个 int 大小的空间，这样做的话 getLast() 和 setLast() 也可以使用上面那种简单的写法，效率是一样的，提高了代码复用率。