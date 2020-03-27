---
title: 使用命令行打开Ubuntu的护眼模式（Night Light）
date: 2020-03-28 01:49:30
categories: [奇淫技巧]
tags: [Linux, Ubuntu, CLI]
---

### 使用命令行打开Ubuntu的Night Mode

- Ubuntu上的护眼模式（Night Light）

  Ubuntu的护眼模式很香，但是不是很好用，如果使用图形界面需要在设置中打开，对于懒癌晚期的患者不是很友好

  <!--more-->

- 解决方法

  - 终端中用命令打开

    ```shell
    # 打开
    gsettings set org.gnome.settings-daemon.plugins.color night-light-enabled true
    # 关闭
    gsettings set org.gnome.settings-daemon.plugins.color night-light-enabled false
    ```

    用了两分钟，体验极差，记不住，太长了，需要继续优化

  - 优化方案

    想到了`alias`，可以通过`alias`别名优化

    - bash的`alias`不支持参数，需要用到function

    **大致思路**

    将`alias`的内容定义成一个函数，由函数处理参数，然后调用函数

    ```shell
    function nightMode() {
    	……
    	……
    }
    $ nightMode <true|false>
    ```

  - 最终实现

    在当前用户的`home`目录下修改`.bashrc`文件，末尾追加

    ```shell
    # turnon or turnoff nightlight
    alias nightmode='nightmode() { gsettings set org.gnome.settings-daemon.plugins.color night-light-enabled $1;}; nightmode'
    ```

  - 使用方法

    当前用户任意位置打开终端输入`nightmode true`或者`nightmode false`打开或者关闭护眼模式

- END