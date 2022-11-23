---
title: fabricjs 自定义数据
author: SakumyZ
img: https://github.com/fabricjs/fabric.js/raw/master/lib/screenshot.png
date: 2022-11-23
categories: JavaScript
tags:
  - JavaScript
  - Canvas
---

# fabricjs 自定义数据

## 概述

通过 `name` 和 `data` 字段来进行自定义。

```ts
const rect: fabric.Rect = new fabric.Rect({
  top: 100,
  left: 0,
  width: 60,
  height: 70,
  fill: 'red',
  name: 'TEST',
  data: {
    id: 'ID_1'
  }
})

canvas.add(rect)
```

下面是其[类型定义](https://github.dev/DefinitelyTyped/DefinitelyTyped/blob/72d0fd1b3423facf8df2381c87a2d6df55816c18/types/fabric/fabric-impl.d.ts#L3129)

```ts
interface IObjectOptions {
  // ...
  /**
   * Not used by fabric, just for convenience
   */
  name?: string | undefined

  /**
   * Not used by fabric, just for convenience
   */
  data?: any
  // ...
}
```

从类型定义中，我们可以明确得看出来，`name`, 和 `data` 这两个属性，是 fabric 官方预留给用户做自定义扩展的。

## 示例

<iframe src="https://codesandbox.io/p/sandbox/fabric-demo-9f5lux?file=%2Fpages%2FcustomData.tsx&amp;selection=%5B%7B%22endColumn%22%3A1%2C%22endLineNumber%22%3A25%2C%22startColumn%22%3A1%2C%22startLineNumber%22%3A25%7D%5D" allow="fullscreen" allowfullscreen="" style="height:100%;width:100%; aspect-ratio: 16 / 9; "></iframe>

![](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/fabricCustomData.gif)
