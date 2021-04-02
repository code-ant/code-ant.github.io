---
title: Java集合知识点整理
date: 2021-04-02 18:11:02
categories: [Java]
tags: [Java, 集合]
---

Java常见的关于集合框架的面试知识点整理。

<!--more-->

### List、Set、Map三者区别

- List：存储一组不唯一（可以有多个元素引用相同的对象）、有序的对象
- Set：不允许重复的集合。不会有多个元素引用相同的对象
- Map：使用键值对存储，Map会维护与Key有关联的值，两个Key可以引用相同的对象，但是Key不能重复，典型的Key是String类型，也可以是任意对象

### ArrayList与LinkedList区别

- 多线程安全：两者都是不同步的，无法保证线程安全
- 底层数据结构：`ArrayList`底层使用`Object`数组；`LinkedList`底层使用的是**双向链表**
- 插入删除与元素位置的关系：
  - `ArrayList`使用数组存储，插入和删除的时候时间复杂度受到元素位置影响。
  - `LinkedList`采用链表存储，插入删除不受其位置的影响，时间复杂度近似O(n)。
- 是否支持快速随机访问：`LinkedList`不支持，`ArrayList`支持。
- 内存占用：`ArrayList`的空间浪费体现在list列表的结尾一定会预留一定的容量空间。`LinkedList`的空间浪费在于每一个元素都要存储前驱和后继节点。

### ArrayList与Vector的区别

`Vector`类中的所有方法都是同步的。可以保证多线程安全，但是在单一线程访问Vector中，同步操作会浪费大量的时间。

`ArrayList`不是同步的，在多线程场景下不适用。

### ArrayList扩容机制

以无参形式构造`ArrayList`的时候，实际上是初始化赋值一个空数组，当真正添加第一个数组元素的操作时，数组扩容为10。ArrayList对象的创建类似单例模式中的懒汉式，延迟赋值针对内存优化。

[参考资料](https://snailclimb.gitee.io/javaguide/#/docs/java/collection/ArrayList源码+扩容机制分析)

### HashMap 和 Hashtable 的区别

1. **线程是否安全：** HashMap 是非线程安全的，HashTable 是线程安全的；HashTable 内部的方法基本都经过`synchronized` 修饰。（如果保证线程安全的话就使用 ConcurrentHashMap ）
2. **效率：** 因为线程安全的问题，HashMap 要比 HashTable 效率高一点。另外，HashTable 基本被淘汰，不要在代码中使用它；
3. **对Null key 和Null value的支持：** HashMap 中，null 可以作为键，这样的键只有一个，可以有一个或多个键所对应的值为 null。。但是在 HashTable 中 put 进的键值只要有一个 null，直接抛出 NullPointerException。
4. **初始容量大小和每次扩充容量大小的不同 ：** ①创建时如果不指定容量初始值，Hashtable 默认的初始大小为11，之后每次扩充，容量变为原来的2n+1。HashMap 默认的初始化大小为16。之后每次扩充，容量变为原来的2倍。②创建时如果给定了容量初始值，那么 Hashtable 会直接使用你给定的大小，而 HashMap 会将其扩充为2的幂次方大小（HashMap 中的`tableSizeFor()`方法保证，下面给出了源代码）。也就是说 HashMap 总是使用2的幂作为哈希表的大小,后面会介绍到为什么是2的幂次方。
5. **底层数据结构：** JDK1.8 以后的 HashMap 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树，以减少搜索时间。Hashtable 没有这样的机制。

### HashMap 和 HashSet区别

HashSet 底层就是基于 HashMap 实现的。（HashSet 的源码非常非常少，因为除了 `clone()`、`writeObject()`、`readObject()`是 HashSet 自己不得不实现之外，其他方法都是直接调用 HashMap 中的方法。

| HashMap                          | HashSet                                                      |
| :------------------------------- | :----------------------------------------------------------- |
| 实现了Map接口                    | 实现Set接口                                                  |
| 存储键值对                       | 仅存储对象                                                   |
| 调用 `put（）`向map中添加元素    | 调用 `add（）`方法向Set中添加元素                            |
| HashMap使用键（Key）计算Hashcode | HashSet使用成员对象来计算hashcode值，对于两个对象来说hashcode可能相同，所以equals()方法用来判断对象的相等性 |

### HashMap底层实现