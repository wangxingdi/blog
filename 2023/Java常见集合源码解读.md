---
title: Java常见集合源码解读
categories: 
  - Tech
tags: 
  - 
keywords: 
description: Java常见集合源码解读
date: 2023-04-12 12:29:12
abbrlink: 20230412
---

## Java常见集合源码解读

## Iterator接口

`iterator`接口，又称迭代器，是一个用于遍历集合元素的接口。这个接口定义了`hasNext`、`next`和`remove`三种方法。

一般来说，`iterator`统一了所有集合的遍历方式 ，例如对于一个`ArrayList`，我们可以这样遍历：

```java
for(int i=0;i<list.size();i++{
    int num = list.get(i);
}
```

但对于`HashSet`，我们这样写就无法通过编译，因为`Set`中并没有索引的概念。因此，各个集合只要在自己内部实现iterator接口并重写上述方法，即可采用统一的写法来进行遍历。

## Iterable

顶级接口，定义了`iterator`方法。

## Collection


