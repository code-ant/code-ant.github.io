---
title: 【每日一题】交替打印FooBar
date: 2020-01-29 11:30:50
categories: [每日一题,LeetCode]
tags: [多线程,LeetCode]
---

> 继续划水

### 【LeetCode】1115. 交替打印FooBar

我们提供一个类：

两个不同的线程将会共用一个 FooBar 实例。其中一个线程将会调用 foo() 方法，另一个线程将会调用 bar() 方法。

请设计修改程序，以确保 "foobar" 被输出 n 次。

<!--more-->

```java
class FooBar {
  public void foo() {
    for (int i = 0; i < n; i++) {
      print("foo");
    }
  }

  public void bar() {
    for (int i = 0; i < n; i++) {
      print("bar");
    }
  }
}
```

 

示例 1:

`输入: n = 1`
`输出: "foobar"`
`解释: 这里有两个线程被异步启动。其中一个调用 foo() 方法, 另一个调用 bar() 方法，"foobar" 将被输出一次。`

示例 2:

`输入: n = 2`
`输出: "foobarfoobar"`
`解释: "foobar" 将被输出两次。`

### 题解

```java
class FooBar {
    private int n;
    public FooBar(int n) {
        this.n = n;
    }
    boolean flag = false;   // f-foo, t-bar
    public synchronized void foo(Runnable printFoo) throws InterruptedException {
        for (int i = 0; i < n; i++) {
            // printFoo.run() outputs "foo". Do not change or remove this line.
            while( flag) wait();
            printFoo.run();
            flag = true;
            notifyAll();
        }
    }
    public synchronized void bar(Runnable printBar) throws InterruptedException {
        for (int i = 0; i < n; i++) {
            // printBar.run() outputs "bar". Do not change or remove this line.
            while( !flag) wait();
            printBar.run();
            flag = false;
            notifyAll();
        }
    }
}
```

