---
title: Github、npm配置代理
date: 2020-08-23 19:37:11
categories: [配置]
tags: [代理,配置,npm,github,git]
---

鉴于一些网络环境的问题，有必要收藏一些代理的使用方法。

记录一些代理的配置方法

<!--more-->

## Github

### Github设置代理

```shell
# 全局
git config --global http.proxy 'socks5://username:password@server:port '
git config --global https.proxy 'socks5://username:password@server:port '

# 局部
git config --local http.proxy username:password@server:port
```

### 只对于github.com


```shell
git config --global http.https://github.com.proxy http://127.0.0.1:1080
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
```

### 取消代理

```shell
git config --global --unset http.https://github.com.proxy
```

### 查询是否使用代理：

- 查询全局代理

```shell
git config --global http.proxy
```

- 查询局部代理

```shell
git config --local http.proxy
```

## npm

### npm设置代理

```shell
npm config set proxy http://username:password@server:port 
npm confit set https-proxy http://username:password@server:port
```

### npm删除代理

```shell
npm config delete proxy
npm config delete https-proxy
```

### 如果代理不支持https的话需要修改npm存放package的网站地址。

```shell
npm config set registry "http://registry.npmjs.org/"
```



---

### npm相关配置

> npm获取配置有6种方式，优先级由高到底。
>
> 1. 命令行参数。 `--proxy http://server:port`即将proxy的值设为`http://server:port`。
> 2. 环境变量。 以`npm_config_`为前缀的环境变量将会被认为是npm的配置属性。如设置proxy可以加入这样的环境变量`npm_config_proxy=http://server:port`。
> 3. 用户配置文件。可以通过`npm config get userconfig`查看文件路径。如果是mac系统的话默认路径就是`$HOME/.npmrc`。
> 4. 全局配置文件。可以通过`npm config get globalconfig`查看文件路径。mac系统的默认路径是`/usr/local/etc/npmrc`。
> 5. 内置配置文件。安装npm的目录下的npmrc文件。
> 6. 默认配置。 npm本身有默认配置参数，如果以上5条都没设置，则npm会使用默认配置参数。
>
> 针对npm配置的命令行操作
>
> ```
>    npm config set <key> <value> [--global]
>    npm config get <key>
>    npm config delete <key>
>    npm config list
>    npm config edit
>    npm get <key>
>    npm set <key> <value> [--global]
> ```
>
> 在设置配置属性时属性值默认是被存储于用户配置文件中，如果加上`--global`，则被存储在全局配置文件中。
>
> 如果要查看npm的所有配置属性（包括默认配置），可以使用`npm config ls -l`。
>
> 如果要查看npm的各种配置的含义，可以使用`npm help config`。



