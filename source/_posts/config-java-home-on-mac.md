---
title: 在OS X上配置JAVA_HOME环境变量
date: 2020-09-13 23:31:33
categories: [配置]
tags: [java,OS X,配置]
---

在Mac上配置Java开发环境的时候，遇到了一些问题，搜索一番下来之后，更困惑了，各类教程基本上是复制粘贴，而且还很老旧，或者按照Linux系列的系统进行配置，部分情况下配置无法生效，特意搜了一下官方文档，总结一下最新的配置方法。

<!--more-->

**系统环境**

系统版本：macOS Catalina 10.15.6

Shell：zsh

[官方链接](https://developer.apple.com/library/archive/qa/qa1170/_index.html)

> Many Java applications need to know the location of a `$JAVA_HOME` directory. The `$JAVA_HOME` on Mac OS X should be found using the `/usr/libexec/java_home` command line tool on Mac OS X 10.5 or later. On older Mac OS X versions where the tool does not exist, use the fixed path "`/Library/Java/Home`". The `/usr/libexec/java_home` tool dynamically finds the top Java version specified in Java Preferences for the current user. This path allows access to the `bin` subdirectory where command line tools such as `java`, `javac`, etc. exist as on other platforms. The tool `/usr/libexec/java_home` allows you to specify a particular CPU architecture and Java platform version when locating a `$JAVA_HOME`.
>
> Another advantage of dynamically finding this path, as opposed to hardcoding the fixed endpoint, is that it is updated when a new version of Java is downloaded via Software Update or installed with a newer version of Mac OS X. For this reason, it is important that developers do not install files in the JDKs inside of `/System`, since the changes will be lost with subsequent updates by newer versions of Java.
>
> To obtain the path to the currently executing `$JAVA_HOME`, use the `java.home` System property.

**developer.apple.com中明确指出了，10.5以后的系统版本使用`/usr/libexec/java_home`进行配置。**



看一下`/usr/libexec/java_home`究竟是个什么东西

![](http://images.wpt6.cn/blog/2020-09-13-23-57-38.png)

**为什么要使用/ usr / libexec / java_home？**
此`java_home`可以返回在Java首选项中为当前用户指定的Java版本。

例如：

![](http://images.wpt6.cn/blog/2020-09-14-00-05-42.png)

通过-V查看当前安装的所有Java的版本

可以使用java_home -v <JDK版本号>来进行切换

参考：[在 Mac OS 上管理多个 jdk 版本](https://www.jianshu.com/p/af79ae7f732c)

----

除去上面配置Java_HOME的一点，还有zsh和shell的区别，众多教程里面也没有注明，不加分辨，盲目复制会走不少弯路。

重要原因在于：macOS Catalina 默认的shell环境是zsh，zsh和shell的加载配置文件是不一样的，按照习惯，在`/etc/profile`或者`～/.bashrc`中添加环境变量信息会不起作用。

看一下`man zsh`的说明

> **STARTUP/SHUTDOWN** **FILES**
>
> ​    Commands are first read from **/etc/zshenv**; this cannot be overridden. Subsequent be-
>
> ​    haviour is modified by the **RCS** and **GLOBAL_RCS** options; the former affects all startup
>
> ​    files, while the second only affects global startup files (those shown here with an
>
> ​    path starting with a **/**). If one of the options is unset at any point, any subsequent
>
> ​    startup file(s) of the corresponding type will not be read. It is also possible for a
>
> ​    file in **$ZDOTDIR** to re-enable **GLOBAL_RCS**. Both **RCS** and **GLOBAL_RCS** are set by default.
>
> 
>
> ​    Commands are then read from **$ZDOTDIR/.zshenv**. If the shell is a login shell, commands
>
> ​    are read from **/etc/zprofile** and then **$ZDOTDIR/.zprofile**. Then, if the shell is inter-
>
> ​    active, commands are read from **/etc/zshrc** and then **$ZDOTDIR/.zshrc**. Finally, if the
>
> ​    shell is a login shell, **/etc/zlogin** and **$ZDOTDIR/.zlogin** are read.
>
> 
>
> ​    When a login shell exits, the files **$ZDOTDIR/.zlogout** and then **/etc/zlogout** are read.
>
> ​    This happens with either an explicit exit via the **exit** or **logout** commands, or an
>
> ​    implicit exit by reading end-of-file from the terminal. However, if the shell termi-
>
> ​    nates due to **exec**'ing another process, the logout files are not read. These are also
>
> ​    affected by the **RCS** and **GLOBAL_RCS** options. Note also that the **RCS** option affects the
>
> ​    saving of history files, i.e. if **RCS** is unset when the shell exits, no history file
>
> ​    will be saved.
>
> 
>
> ​    If **ZDOTDIR** is unset, **HOME** is used instead. Files listed above as being in **/etc** may be
>
> ​    in another directory, depending on the installation.
>
> 
>
> ​    As **/etc/zshenv** is run for all instances of zsh, it is important that it be kept as
>
> ​    small as possible. In particular, it is a good idea to put code that does not need to
>
> ​    be run for every single shell behind a test of the form `**if** **[[** **-o** **rcs** **]];** **then** **...**' so
>
> ​    that it will not be executed when zsh is invoked with the `**-f**' option.
>
> 
>
> ​    Any of these files may be pre-compiled with the **zcompile** builtin command (see zsh-
>
> ​    builtins(1)).  If a compiled file exists (named for the original file plus the **.zwc**
>
> ​    extension) and it is newer than the original file, the compiled file will be used
>
> ​    instead.
>
> 
>
> **FILES**
>
> ​    **$ZDOTDIR/.zshenv**
>
> ​    **$ZDOTDIR/.zprofile**
>
> ​    **$ZDOTDIR/.zshrc**
>
> ​    **$ZDOTDIR/.zlogin**
>
> ​    **$ZDOTDIR/.zlogout**
>
> ​    **${TMPPREFIX}\***  (default is /tmp/zsh*)
>
> ​    **/etc/zshenv**
>
> ​    **/etc/zprofile**
>
> ​    **/etc/zshrc**
>
> ​    **/etc/zlogin**
>
> ​    **/etc/zlogout**  (installation-specific - **/etc** is the default)

zsh使用的是这些配置文件，所以在上面说的两个bash使用的配置文件中添加环境变量，默认是不加载的。

所以

```shell
echo export JAVA_HOME=\$\(/usr/libexec/java_home\) >> ~/.zshenv
```

关于进一步详细设置，可以参考[如何在Mac OS X 10.9上设置JAVA_HOME环境变量？](https://qastack.cn/programming/22842743/how-to-set-java-home-environment-variable-on-mac-os-x-10-9)



关于zsh的配置文件的比较，可以参考[Moving to zsh, part 2: Configuration Files](https://scriptingosx.com/2019/06/moving-to-zsh-part-2-configuration-files/)和[zsh+tmux+OS X: 正确地设置 PATH](https://chenyufei.info/blog/2014-03-04/zsh-tmux-osx-set-correct-path/)这两篇博客。

