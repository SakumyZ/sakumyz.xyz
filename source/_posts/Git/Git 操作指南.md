---
title: Git 操作指南
date: 2022-11-02
author: SakumyZ
img: https://www.freecodecamp.org/news/content/images/size/w300/2021/10/github-on-the-hunt-for-a-new-diversity-lead-developers-techworld-github-universe-png-800_450.png
categories: Git
tags: Git
---

# Git 操作指南

## 1. 配置

```shell
git config --global credential.helper store // 保存账户密码？
git config --global user.name "myname"  // 配置用户名
git config --global user.email "myname@mymail.com"  //配置邮箱

git remote -v //查看当前git仓库地址
git remote set-url origin http://XXX/XXX.git(新git仓库地址) //更换git仓库地址

```

**PS:** 当 `user.name` 和 `user.email` 都是对的时候，可在 git 网页查看 ① 上传者的头像，② 可通过点击上传者头像跳转到该上传者的主页。

## 2. 基本命令

```shell
git init  // 初始化本地仓库

git remote add origin code@github.git  //绑定本地和远程仓库

git clone <url> // 拉取指定地址URL的代码

git pull   // 拉取远程仓库的变化来同步本地的状态
git pull orign <branch> // 拉取代码至指定分支，拉取完毕后需要 push

git add <file>// 确认本地仓库的变化到本地缓存区
git add . // 将本地仓库的所有变化文件加入到本地缓存区
git status   // 确定本地缓存区的状态

git commit  // 确认本地缓存区的内容，可以准备push
git push   // 提交本地仓库到远程仓库

git mv <oldName> <newName> 修改文件名（主要用于新旧名称只有大小写区别时）
```

## 3. 日志查看

`git log` 命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的

可以试试加 `--pretty=oneline` 参数。

```shell
// 显示运行命令日志
git reflog

查看指定作者的 log

git log --author="<authorName>"

# eg: git log --author="sakumyz"
```

## 4. 分支管理

首先新建分支

```shell
git branch <branch>
git branch -b <branch-name> // 新建并切换分支
```

示例

```shell
git checkout -b dev
Switched to a new branch 'dev'
```

然后，用 `git branch` 命令查看当前分支：

```shell
git branch  // 查看当前分支
git branch -a // 列出所有本地分支和远程分支

$ git branch
* dev
  master
```

`git branch` 命令会列出所有分支，当前分支前面会标一个 `*` 号。

然后，我们就可以在 dev 分支上进行提交。

切换分支

```shell
git checkout <branch> // 切换到指定分支，并更新工作区
git checkout -b <branch> // 新建一个分支，并切换到该分支
```

不过现在 git 推荐使用新命令 `git switch <branch>`

分支合并

合并某分支到当前分支：`git merge <name>`

## 5. 版本回退

```shell
// 回到上一版本
git reset --hard HEAD^

// 回到指定版本
git reset --hard <commit-id>
```

版本号没必要写全，前几位就可以了，Git 会自动去找。当然也不能只写前一两位，因为 Git 可能会找到多个版本号，就无法确定是哪一个了。

## 6. 冲突合并

当 pull 或 push 代码时可能会存在冲突的问题。此时会提示你哪个文件产生了冲突。

✨ **解决思路：**

如果产生冲突的文件修改比较少，或者无关紧要，可以直接 revert 修改，但如果修改地方很多则先将本地的修改进行 commit，然后再进行 push 或者 pull 的操作，此时会产生冲突合并提示，按照要求进行合并就可以了。

## 7. 保存和恢复工作进度

应用场景：切换分支时不想提交正在修改的文件

```shell
$ git stash                   // 保存当前的工作进度。会分别对暂存区和工作区的状态进行保存
Saved working directory and index state WIP on dev: 6224937 add merge
HEAD is now at 6224937 add merge

$ git stash save "message"    // git stash 的完整命令，"message" 填写备份注释

$ git stash list              // 显示进度列表
stash@{0}: WIP on dev: 6224937 add merge

$ git stash apply stash@{0}   // 恢复工作区@{0}

$ git stash drop stash@{0}    // 删除工作区的备份@{0}

$ git stash pop stash@{0}     // 恢复工作区@{0}，并删除该工作区的备份

$ git stash clear             // 删除所有存储的进度
```
