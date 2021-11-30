---
title: "Redis命令"
date: "2021-11-25T10:25:25+08:00"
slug: "redis-command-string"
draft: false
---

## SET

SET key value [EX seconds | PX milliseconds | EXAT timestamp | PXAT milliseconds-timestamp | KEEPTTL] [NX | XX] [GET]

> 自版本1.0.0可用
> 时间复杂度：O(1)


向内存中设置一个key-value形式的键值对，更多的能力请参加可选项。

### 可选项
如我所示，SET命令支持多个可选项，可选项的不同，也会导致命令的效果不同。
* `EX seconds` : 给这个key设置过期时间，以秒为单位。

  ```bash
  ## 设置key-value键值对，并指定在10秒后过期
  redis> set key value ex 10
  "OK"
  ```

* `PX milliseconds` : 给这个key设置过期时间，以毫秒为单位。

  ```bash
  ## 设置key-value键值对，并指定在100毫秒后过期
  redis> set key value px 100
  "OK"
  ```

* `EXAT timestamp-seconds` :  设置一个以秒为单位的时间戳，key将会在这个指定的时间点失效。

  ```bash
  ## 设置key-value键值对，并指定在2021年12月12日0时0分1秒时过期
  redis> set key value EXAT 1639238401
  "OK"
  ```

* `PXAT timestamp-milliseconds` : 设置一个以毫秒为单位的时间戳，key将会在这个指定的时间点失效。同EXAT相比，PXAT能够将时间精确到毫秒值。

  ```bash
  ## 设置key-value键值对，并指定在2021年12月12日0时0分1秒时过期
  redis> set key value PXAT 1639238401000
  "OK"
  ```

* `NX` : key不存在，则设置成功；否则，设置失败。

  ```bash
  ## 使用NX可选项设置两次key-value键值对，第二次会设置失败
  redis> set key value NX
  "OK"
  redis> set key value2 NX
  (nil)
  ```

* `XX` ： key存在，则设置成功；否则，设置失败。

  ```bash
  ## 直接使用XX可选项设置key-value键值对，会设置失败；如果先设置一次，再使用XX可选项，则会设置成功
  redis> set key value XX
  (nil)
  redis> set key value
  "OK"
  redis> set key value2 XX
  "OK"
  ```

* `KEEPTTL`：继承当前key被覆盖前的过期时间。一般来说，如果执行set key value命令时，如果key已经存在，那么不管之前这个key是否存在过期时间，都会被覆盖掉。此时，如果需要仅仅修改value值而不影响过期时间，则需要KEEPTTL可选项。

  ```bash
  ## 先设置一个200秒后过期的key-value键值对，然后使用keepttl进行重新赋值，过期时间不变
  redis> set key value ex 200
  "OK"
  redis> set key value2 keepttl
  "OK"
  redis> ttl key
  (integer)190
  ```

* `GET`：返回当前key存储的旧值，如果key不存在，就返回nil。如果value不是string类型，将会返回error。

  ```bash
  ## get能够返回旧值，如果key不存在，将返回nil
  redis> set key value get
  (nil)
  redis> set key value2 get
  "value"
  ```
  
  注意：从SET命令的可选项可以看出，SET命令可以完成SETNX、SETEX、PSETEX、GETSET这几个命令的能力。因此，在未来的Redis版本中，这些命令可能会被弃用并删除。

### 返回值

* `OK`：如果SET命令被正确执行，将会被返回；
* `nil`：在使用NX或者XX可选项时，如果不满足条件，会返回nil；或者在使用GET可选项时，key不存在的情况下，也会返回nil；
* 旧值：在使用GET可选项时，将会返回旧值。

## SETEX

SETEX key seconds value

> 自版本2.0.0可用
> 时间复杂度：O(1)

ex是expire这个单词的缩写，可以将这个命令理解为：set and expire。中文含义就是在内存中设置一个key-value键值对，并指定在seconds秒之后失效。需要注意的是，setex是一个原子操作，这一特点对于缓存极其重要。

### 示例

```bash
## 设置一个key-value键值对，并在10秒后过期
redis> setex key 10 value
```

## SETNX

SETNX key value

> 自版本1.0.0可用
> 时间复杂度：O(1)

nx是not exists的简写，可以将这个命令理解为：set if not exists。中文含义就是在key不存在的情况下才set，如果key已经存在，那么什么操作都不会发生。这一特性对于分布式锁很重要。

### 返回值

这个命令的返回值只有两种情况：

* 1：set成功；
* 0：set失败；

### 示例

```bash
redis> setnx key value
(integer)1
redis> setnx key value2
(integer)0
```

