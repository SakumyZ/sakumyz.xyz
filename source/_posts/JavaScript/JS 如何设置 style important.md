---
title: JS 如何设置 style important
date: 2022-11-07
author: SakumyZ
categories: JavaScript
tags: JavaScript
---

# JS 如何设置 style important

## 1. 问题描述

我们有时需要使用 JS 去设置 DOM 元素的 style 值，但是有个问题，当我们想要设置属性值加上 `!important` 时，我们会发现，设置并不生效。

比如下面的例子，我们期望的是 **点击按钮后，蓝色的 box 变成红色**

```html
 
<div class="box"></div>
  <button class="btn" type="button">点我变色</button>
```

我们给 box 设置了 `important`, 所以只有当我们行内 style 的`important` 属性生效，才会变成红色。

```css
.box {
  width: 100px;
  height: 100px;
  background: blue !important;
}
```

![](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/20221107225111.png)
下面是我们通常的想法，点击时，设置 `style.backgroundColor`

```js
const box = document.querySelector('.box')
const btn = document.querySelector('.btn')

btn.addEventListener('click', () => {
  box.style.backgroundColor = 'red !important'
})
```

但是没有用

![jsSetImportant1](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/jsSetImportant1.gif)

## 2. 解决方案

### 2.1 原生 JS

使用 [CSSStyleDeclaration.setProperty()](https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleDeclaration/setProperty)

```js
style.setProperty(propertyName, value, priority)
```

**参数**

- *`propertyName`*  是一个  [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String) ，代表被更改的 CSS 属性。
- \_`value` (可选)  [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String) ，含有新的属性值。如果没有指定，则当作空字符串。
  - 注意：*`value`*  不能包含  `"!important"` --那个应该使用  *`priority`*  参数。
- \_`priority`(可选)  [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)  允许设置 "important" CSS 优先级。如果没有指定，则当作空字符串。

带入本例则代码如下:

```js
box.style.setProperty('background-color', 'red', 'important')
```

## 2.2 JQuery

```js
$('.box').css('cssText', 'color: red !important;')
```

`Jquery` 这种用法相当于原生的

```js
box.style.cssText = 'background-color: red !important'
```

可以达到同样的作用，但问题有一个，如果之前存在有行内的 style, 那么行内 style 将会被覆盖。

## 2.3 效果

![jsSetImportant2](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/jsSetImportant2.gif)
