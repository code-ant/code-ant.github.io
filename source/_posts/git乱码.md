---
title: Windows下使用Git出现中文乱码
date: 2020-02-13 00:25:01
categories: [开发环境]
tags: [idea,git,乱码,Windows]
---

> Windows下使用Git查看git log的时候出现乱码

- **现象**
  - `cmd` `powershell`都是乱码
  - idea的`Terminal`终端也显示乱码
  - `Git Bash`可以正常显示中文

<!--more-->

<img src=" http://images.wpt6.cn/20200214-1.jpg" alt="powershell使用Git中文乱码" style="zoom:80%;" />

<img src=" http://images.wpt6.cn/20200214-2.jpg" alt="cmd使用Git中文乱码" style="zoom:80%;" />

![Gitbash显示中文正常]( http://images.wpt6.cn/20200214-3.jpg )



- **解决方法**

  - 方法一：*推荐*

    设置一条`LESSCHARSET=UTF-8`的环境变量--系统变量

    <img src=" http://images.wpt6.cn/20200214-4.jpg" alt="设置系统变量" style="zoom:80%;" />

    设置完成，重新打开终端使用Git

  - 方法二：

    设置一条`LESSCHARSET=UTF-8`的环境变量--用户变量

    <img src=" http://images.wpt6.cn/20200214-5.jpg" alt="设置用户变量" style="zoom:80%;" />

    **注意：此时在idea中使用还是会出现中文乱码**

    - 原因：在idea中的`cmd` `powershell`只加载了系统变量并没有加载用户变量，需要在idea中重新设置一条`LESSCHARSET=UTF-8`的配置

    ![idea中添加配置]( http://images.wpt6.cn/20200214-6.jpg )

