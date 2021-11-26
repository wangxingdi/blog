---
title: Redis命令
date: 2021-11-25
draft: true
---

## String
### SET
SET key value [EX seconds | PX milliseconds | EXAT timestamp | PXAT milliseconds-timestamp | KEEPTTL] [NX | XX] [GET]

> 自版本1.0.0可用
> 时间复杂度：O(1)


向内存中设置一个key-value形式的键值对。如果这个key已经存在，不管它对应的value是哪种类型的数据，都将被覆盖。同时，如果被覆盖掉的value有过期时间，那么这个过期时间也将失效。

#### 可选项
如我所示，SET命令支持多个可选项，参数的不同，也会导致效果的不同。
* EX seconds : 以秒为单位，给这个key设置一个过期时间。
* PX milliseconds : 以毫秒为单位，给这个key设置一个过期时间。
* EXAT timestamp-seconds :  设置一个以秒为单位的时间戳，key将会在这个指定的时间点失效。
* PXAT timestamp-milliseconds : 设置一个以毫秒为单位的时间戳，key将会在这个指定的时间点失效。
* NX : 只有在key不存在的情况下才能设置成功。
* XX ： 只有在key存在的情况下才能设置成功。