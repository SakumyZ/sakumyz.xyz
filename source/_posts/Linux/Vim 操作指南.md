---
title: Vim 操作指南
date: 2022-11-02
author: SakumyZ
categories: Linux
tags:
  - Linux
  - Vim
---

# Vim 操作指南

## 移动

1.  单词间移动--移动到单词开头 `w`
2.  单词间移动--移动到单词结尾 `e`

## 页面移动

1.  将屏幕置为中间 `zz`
2.  上翻页 `Ctrl + u`
3.  下翻页 `Ctrl + f`

## Visual 模式

1.  普通选择 按 `v` 进入
2.  行选择   按 `V` 进入
3.  块选择   按 `Ctrl + v` 进入

## 快速删除

1.  退格 `Ctrl + h` (Insert)
2.  剪切一个字符 `x` (Normal)
3.  删除上一个单词 `Ctrl + w`
4.  删除当前单词 `dw`
5.  删除一行 `Ctrl + u` (Insert)
6.  删除一行 `dd` (Normal)
7.  删除引号 间的字符 `dt + 引号`
8.  删除到行首 `d0`
9.  删除到行尾 `d$`
10. `数字 + d` 例如 4x 删除 4 个字符，4d 删除 4 行

## 快速修改

1.  替换选中文本 `r`
2.  `cw` 修改一个单词，并快速进入插入模式
3.  替换选中文本并进入 Insert 模式 `s`

## 快速切换 Normal 和 Insert

1.  ESC
2.  Ctrl + [
3.  快速跳转到上次编辑的模式 `gi`

## 搜索

1.  `f{char}`再按; 可以选择下一个 按, 可以选择上一个
2.  快速移动到行首 `0 ^` (非空白)
3.  快速移动到行尾 `$ g_` (非空白)

## 替换

将全文的 self 替换为 this

```vim
s/self/this/g
```

讲 1-6 行的 self 替换为 this

```vim
1,6 s/self/this
```

统计字符串出现的次数

```vim
1,6 s/self/n
```

## 宏

按 `q{name}` 开始录制宏进行操作
进行操作
按 `q` 结束录制

使用 `@{name}`进行回放
