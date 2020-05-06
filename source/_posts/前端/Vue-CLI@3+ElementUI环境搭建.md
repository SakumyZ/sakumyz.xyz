---
title: Vue-CLI@3+ElementUI环境搭建.md
date: 2020-01-20
author: SakumyZ
cover: true
categories: 前端
tags:
  - Vue,
  - ElementUI
---

# Vue-CLI@3+ElementUI 环境搭建

## Node.js

> JavaScript 运行时环境，使 JS 可以脱离浏览器运行

官网：https://nodejs.org/en/

## NPM

> Node Package Manager，是 Node.js 的包管理器，拥有大量的第三方包，可以类比 Python 的 PIP

## Vue

> 前端三大框架之一，MVVM 架构，组件化编程思想。本次项目拟定使用 Vue 对前端进行重构，出于快速搭建的原则，使用 Vue 的脚手架工具 Vue CLI 来进行项目的初始化

Vue 官网：https://cn.vuejs.org/

安装 `Vue CLI`

```bash
npm install -g @vue/cli
```

使用 Vue CLI 创建 Vue 项目

```bash
vue create my-app
```

> 注意：项目名内不能出现大写，否则无法创建项目

创建完项目后，根据终端 log 提示输入以下两行命令

```bash
cd demo
npm run serve
```

此时，将会在本地启动一个服务器，服务器启动成功后，根据 log 给的地址，则可打开项目 APP

![image-20200115002935433](C:\Users\AkSa\Desktop\imgs\image-20200115002935433.png)

出现以下画面则说明环境搭建成功

![image-20200115003057172](http://sakumyz.xyz/static/images/image-20200115003057172.png)

## Element UI

> 基于 Vue 的一个组件化 UI，方便快速出效果

官网：https://element.eleme.cn/#/zh-CN

### 使用 vue-cli@3

Element UI 为新版的 vue-cli 准备了相应的 [Element 插件](https://github.com/ElementUI/vue-cli-plugin-element)，可以用它们快速地搭建一个基于 Element 的项目。

```bash
vue add element
```

![image-20200119232939425](http://sakumyz.xyz/static/images/image-20200119232939425.png)

此处选择按需导入(Import on demand)。然后剩下的直接回车。安装完成后会有以下提示

![image-20200119233256122](http://sakumyz.xyz/static/images/image-20200119233256122.png)

可以在`src/plugins/element.js`文件中配置导入的组件

![image-20200119233359229](http://sakumyz.xyz/static/images/image-20200119233359229.png)

使用`npm run serve`启动服务器，将会看见主页有所修改

![image-20200119233758767](http://sakumyz.xyz/static/images/image-20200119233758767.png)

至此，Vue 加 Element UI 的基础环境就搭建完成了。

## Axios

> 用于快速书写 AJAX 请求

官网:http://axios-js.com/

安装：

```bash
npm install axios -S
```
