---
title: Markdown常用语法简介
date: 2018-05-12
author: SakumyZ
img: http://sakumyz.xyz/static/images/markdown.png
cover: true
categories: 语言
tags: Markdown
---

# Markdown 语法简介

## 标题样式

总共六级标题，建议在井号后加一个空格，这是最标准的 Markdown 语法。

代码展示：

```
* # 一级标题
* ## 二级标题
* ### 三级标题
* #### 四级标题
* ##### 五级标题
* ###### 六级标题
```

效果展示：

![markdown-title](http://sakumyz.xyz/static/images/markdown-title.png)

## 换行

只需在行末加两个空格键和一个回车键即可换行

## 分段

段落之间空一行即可。

## 文本样式

- 加粗：**加粗**
- 斜体：_斜体_
- 粗斜体：**_粗斜体_**
- 删除线：~~删除线~~
- 底纹：`底纹`

## 代码区

```
加粗：**加粗**
斜体：*斜体*
粗斜体：***粗斜体***
删除线：~~删除线~~
底纹：`底纹`
```

## 分割线

```markdwon
---
```

---

## 列表

- 无序列表： 在文本前加 「 _ 」 即可生成一个无序列表。在 「 _ 」 前加两个空格键或者一个 tab 键就可以产生一个子列表。
- 有序列表：在文本前加[1.]或者[a.]即可生成一个有序列表。

## 引用

只要在文本内容之前加 「 > （大于号）」 即可。
代码实现：

```
> The content that you want to reference
```

效果展示：

> This is reference

## 代码区

使用两对 3 个反单引号将代码框起来。
代码实现：

```
#include <stdio.h>
int main()
{
  printf("hello markdown!\n");
  return 0;
}
```

## 超链接

### 插入图片

！加上`[]`，`[]`里是图片的名字，然后再加上图片的连接用`()`括起来。
代码实现：

```
![picture_name](URL)
```

效果展示：
![markdown-logo](https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1526104893&di=378f9801cc74e848765e8acd62195065&src=http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/8881.jpg)

### 插入链接

和插入图片相比仅仅是少了一个感叹号。
代码实现：

```
[link_name](URL)
```

效果展示：
[markdown_tutorial](http://www.markdown.cn/)

## 表格

markdown 的表格是需要自己手动画下来的，稍微有点蠢，emmm，既然已经这么麻烦了，还是来最简单的一种方法。

### 表头和单元格

使用 | 来分隔不同的单元格，使用 - 来分隔表头和其他行：

### 对齐方式

- 左对齐：用 `：---` 代表左对齐
- 居中：用 `：---：` 代表居中
- 右对齐：用 `---:` 代表右对齐

代码实现：

```
|left|center|right|
|:---|:----:|----:|
| 111| 222  | 333 |
```

效果展示：

| left | center | right |
| :--- | :----: | ----: |
| 111  |  222   |   333 |

### 插入

同样的，在 markdown 表格里也能插入图片和链接，用法和上面一样，就不过多赘述了。

## 脚注

用 `[^1]` 作为脚注标号，然后再在合适的地方输入 `[^1]` 写注解，相当与课本里的注释。

代码实现：

```
something[^1]

[^1]:This is footnote
```

效果展示：

Footnotes[^1]

[^1]: This is a footnote

## 注释

同各种语言一样，注释是为了增加代码的可读性。markdown 的注释也是很简单的，只需要用 `< >` 括起来就可以了
