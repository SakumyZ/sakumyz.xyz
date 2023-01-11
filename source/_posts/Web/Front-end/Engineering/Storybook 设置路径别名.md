---
title: storybook 设置路径别名
tags: [Engineering, Storybook]
categories: Engineering
author: SakumyZ
createTime: 2023-01-11 15:25:01
modifiedTime: 2023-01-11 15:25:01
img: https://plusreturn.com/wp-content/uploads/2021/12/New-Project.png
---

# storybook 设置路径别名

找到项目根目录下的 `.storybook/main.js` 文件。

添加如下`webpackFinal`字段中的配置即可。

```js
const path = require('path')

module.exports = {
  stories: ['../src/**/*.stories.mdx', '../src/**/*.stories.@(js|jsx|ts|tsx)'],
  addons: [
    '@storybook/addon-links',
    '@storybook/addon-essentials',
    '@storybook/addon-interactions',
    '@storybook/preset-create-react-app'
  ],
  framework: '@storybook/react',
  core: {
    builder: '@storybook/builder-webpack5'
  },
  webpackFinal: async config => {
    config.resolve.alias = {
      ...config.resolve.alias,
      '@': path.resolve(__dirname, '../src/')
    }
    return config
  }
}
```

参考文章：[How to resolve a path alias in Storybook | +return (plusreturn.com)](https://plusreturn.com/blog/how-to-resolve-a-path-alias-in-storybook/)
