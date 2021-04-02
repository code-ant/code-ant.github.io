---
title: Redis-随笔
date: 2021-04-02 17:58:02
categories: [Redis]
tags: [Redis, 数据库]
---

- Redis的基本数据类型

  <!--more-->

  - String

    - 基本操作

      SET——设置

      GET——获取值

      EXISTS——是否存在

      DEL——删除

      EXPIRE——设置过期，EXPIRE KEY SEC

      SETNX——SET+EXPIRE

      MSET——批量设置，MSET key1 value1 key2 value2

      MGET——批量获取，MGET key1 key2 key3

      INCR——对整数值原子性自增操作

      GETSET——设置一个值并返回原值

  - list

    - 基本操作

      LPUSH/RPUSH——向左右添加一个元素

      LRANGE——从LIST中取出一定范围的元素

      LINDEX——从list中取出制定下标的元素

      LPOP/RPOP——从左右节点弹出一个元素

  - hash

    - 基本操作

      HSET——设置hash

      HGETALL——获取全部元素

      HGET——获取指定key的值

      HMSET——批量设置

    - 渐进式rehash，节省时间

    - 扩容按照2倍进行扩容，如果在做持久化则尽量不去做扩容。达到一维数组长度5倍的时候会强制扩容。

  - set

    - 内部键值对是无序的、唯一的

    - 基本使用

      SADD创建

      SMEMBERS——读取所有元素

      SISMEMBER——查询是否存在

      SCARD——查询长度

      SPOP—— 弹出一个

  - zset-有序集合

    - 内部使用跳跃表实现

    - 基本操作

      ZRANGE——按照顺序排列

      ZREVRANGE——按照逆序输出

      ZCARD——统计长度

      ZSCORE——获取指定value的score

      ZRANK——获取排名

      ZRANGEBYSCORE——遍历指定区间的元素

      ZREM——删除一个value

- String的实现--简单动态字符串，SDS(Simple Dynamic String)

- SDS和C语言字符串的区别

  - 计数方式不一样

    - C语言O(n)，发现`‘\0`’停止计数

    - SDS的数据结构已经保存了字符串长度

      ```c
      struct sdshdr{
       int len;
       int free;
       char buf[];
      }
      ```

  - 杜绝缓冲区溢出

    - 通过`free`判断是否需要扩容

  - 减少修改字符串时的内存重新分配

    - 空间预分配
    - 惰性空间释放

  - 二进制安全

## 跳跃表

跳跃表的实现比较复杂，也是一个重点，需要刻意关注。

- 为什么使用跳跃表

  zset需要支持随机插入和删除，所以不宜使用数组来实现。相比于红黑树/平衡树，跳跃表的优势在于**性能**和**实现**。

  **性能**：高并发的情况下，树的rebalance可能涉及整个树。跳跃表只会涉及到局部。

  **实现**：在复杂度与红黑树相同的情况下，跳跃表实现起来更加简单，更直观。