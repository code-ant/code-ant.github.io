---
title: git使用笔记
date: 2020-08-04 21:33:21
categories: [开发工具]
tags: [git, GitHub]
---

记录一些常见的git命令吧

<!--more-->

- 创建分支

  `git branch branchName`

- 切换分支

  `git checkout targetBranch`

- 创建分支并切换到该分支

  `git checkout -b branchName`

- 拉取远程分支到本地

  `git checkout -b localbranch origin/remoteBranch`

  `git pull origin master`

- 推送本地分支到远程

  `git push origin localBranch`

- 删除本地分支

  `git branch -d localBranch`

- 删除远程分支

  `git push origin :branchToboDeleted`

