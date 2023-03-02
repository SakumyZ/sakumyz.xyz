---
title: GitLab 配置 SSH Key
tags: [Ohters, Gitlab]
categories: [Ohters, Gitlab]
parent: Ohters
author: SakumyZ
createTime: 2023-03-02 15:12:59
modifiedTime: 2023-03-02 15:12:59
img: https://www.almtoolbox.com/blog/wp-content/uploads/2018/02/gitlab-logo-purple.jpg
---

# GitLab 配置 SSH Key

## 生成 RSA 公钥和私钥

```shell
$ ssh-keygen -t rsa -C 'your-email'
```

这里的邮箱是需要填写 `gitlab` 用户的登录邮箱

一路回车后

Windows 系统会在路径 `%HOMEPATH%/.ssh`下生成 `id_rsa.pub` 和 `id_rsa` 两个文件
Linux 会在 `~/.ssh` 下生成

我们打开 `id_rsa.pub` 文件，复制其中的内容

## 在 Gitlib 中添加公钥生成 SSH Key

打开 gitlab 的设置

Profile Settings --> SSH Keys (英文)
偏好设置 --> SSH 密钥 （中文）

将刚才复制好的密钥粘贴在下图位置中

![添加SSH](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/gitlab-ssh-1.png)

添加完 SSH Key 之后，以后 clone 项目或者是切换仓库地址时，应当使用 SSH 的形式进行 clone

![以SSH的方式进行clone](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/gitlab-ssh-2.png)

## 注意

如果之前是使用的 HTTP 方式 clone 的代码，即使添加了 SSH Key，已经在本地 clone 的项目页不会通过 SSH 进行交互，需要将远程仓库的地址切换为 SSH 地址

```shell
$ git remote set-url origin 'ssh://git@git.XXXXXXXX.git'
```
