---
title: 同一台电脑为Git配置多个SSH Key
date: 2022-07-21 10:18:35
categories: [开发环境]
tags: [git, github, 多账号]
---

# 背景

1. 使用同一台电脑向不同的git平台提交代码

2. 使用同一台电脑向同一个git平台的不同账号提交代码

<!--more-->

# 解决方法

## 为多个平台配置SSH Key

以Github和Gitlab两个平台为例，同时为两个平台创建SSH Key

1. 生成Github的SSH-Key
   
   ```shell
   $ ssh-keygen -t rsa -C 'github_mail@domain.com' -f ~/.ssh/github_id_rsa
   ```

2. 生成Gitlab的SSH-Key
   
   ```shell
   $ ssh-keygen -t rsa -C 'gitlab_mail@domain.com' -f ~/.ssh/gitlab_id_rsa
   ```

3. 创建`config`文件管理多个Key
   
   在`~/.ssh`文件夹下新建一个`config`文件，如果有就直接在末尾追加内容
   
   ```shell
   $ cd ~/.ssh
   $ touch config
   ```
   
   在`config`文件中写入如下内容
   
   ```shell
   # github
   Host github.com
   HostName github.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/github_id_rsa
   # gitlab
   Host gitlab.some_url.com
   HostName gitlab.some_url.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/gitlab_id_rsa
   ```

4. 使用ssh命令测试
   
   ```shell
   $ ssh -T git@github.com
   $ ssh -T git@gitlab.com
   ```
   
   以GitHub为例，如果连接成功，会有如下返回内容
   
   `Hi code-ant! You've successfully authenticated, but GitHub does not provide shell access.`

## 为统一平台多个账户配置SSH Key

还有一些时候，我们在GitHub有多个账号，需要同时给两个账号创建SSH Key.

这种情况下的配置和上面为两个平台配置SSH Key步骤类似，主要区别集中在使用Host区分不同账号上面.

假设此时有两个GitHub账号，一个叫做`code-ant`，另一个叫做`nobodyKnowsMe`.

1. 为`code-ant`账号创建SSH Key
   
   ```shell
   $ ssh-keygen -t rsa -C 'code-ant@domain.com' -f ~/.ssh/code_ant_id_rsa
   ```

2. 为`nobodyKnowsMe`创建SSH Key
   
   ```shell
   $ sh-keygen -t rsa -C 'nobodyKnowsMe@domain.com' -f ~/.ssh/nobody_id_rsa
   ```

3. 创建`config`文件管理多个Key
   
   在`~/.ssh`文件夹下新建一个`config`文件，如果有就直接在末尾追加内容
   
   ```shell
   $ cd ~/.ssh
   $ touch config
   ```
   
   在`config`文件中写入如下内容
   
   ```shell
   # code-ant
   Host code-ant.github.com
   HostName github.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/code_ant_id_rsa
   # nobodyKnowsMe
   Host nobodyKnowsMe.github.com
   HostName github.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/nobody_id_rsa
   ```
   
   说明：git会根据`config`文件中的`Host`和`HostName`做替换

4. 使用ssh命令测试
   
   ```shell
   $ ssh -T git@code-ant.github.com
   $ ssh -T git@nobodyKnowsMe.gitlab.com
   ```
   
   以`code-ant`为例，如果连接成功，会有如下返回内容
   
   `Hi code-ant! You've successfully authenticated, but GitHub does not provide shell access.`

5. 使用git访问不同的账号
   
   使用`code-ant`账号拉取、提交代码
   
   `git clone git@code-ant.github.com/code-ant/XXX.git`
   
   使用`nobodyKnowsMe`账号拉取提交代码
   
   `git clone git@nobodyKnowsMe.github.com/nobodyKnowsMe/xxx.git`
