---
title: Git 仓库初始提交
date: 2022-11-02
author: SakumyZ
categories: Git
tags: Git
---

# Git 仓库初始提交

> 就拿该知识库为例子。下面命令是 Gitee 生成的自动命令。
> 基本上适用于所有 git 仓库的初始提交，只需要替换 用户名以及邮箱
> 还有仓库的地址即可。

## Git 全局设置

```shell
git config --global user.name "SakumyZ"
git config --global user.email "sakumyz@gmail.com"
```

## 创建 git 仓库:

```shell
mkdir knowledge-base
cd knowledge-base
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/SakumyZ/knowledge-base.git
git push -u origin "master"
```

## 已有仓库?

```shell
cd existing_git_repo
git remote add origin https://gitee.com/SakumyZ/knowledge-base.git
git push -u origin "master"
```
