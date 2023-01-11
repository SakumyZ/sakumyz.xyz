---
title: 从环境变量中获取 package.json 中的配置
tags: [Engineering]
categories: Engineering
author: SakumyZ
createTime: 2023-01-11 10:40:46
modifiedTime: 2023-01-11 10:40:46
img: https://res.cloudinary.com/practicaldev/image/fetch/s--rgyGxhx7--/c_imagga_scale,f_auto,fl_progressive,h_500,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9vu045q1s799899xj17a.png
---

# 从环境变量中获取 package.json 中的配置

开始前需要知道一点，通过 在 package.json 中定义的 script 启动时，npm 将会帮我们自动将其中的配置注入前缀为 `npm_package_` 的环境变量。

eg:

```json
{ "name": "foo", "version": "1.2.5" }
```

那么在环境变量中就会注入

```js
npm_package_name: 'foo'
npm_package_version: '1.2.5'
```

官网原文：

> The package.json fields are tacked onto the `npm_package_` prefix. So, for instance, if you had `{"name":"foo", "version":"1.2.5"}` in your package.json file, then your package scripts would have the `npm_package_name` environment variable set to "foo", and the `npm_package_version` set to "1.2.5". You can access these variables in your code with `process.env.npm_package_name` and `process.env.npm_package_version`, and so on for other fields.

详细内容可以参照：[scripts | npm Docs (npmjs.com)](https://docs.npmjs.com/cli/v6/using-npm/scripts#packagejson-vars)
