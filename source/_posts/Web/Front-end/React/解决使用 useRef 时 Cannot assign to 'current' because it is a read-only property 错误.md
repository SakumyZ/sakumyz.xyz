---
tags: [React]
parent: [React]
categories: [React]
author: SakumyZ
createTime: 2022-12-09 15:53:02
modifiedTime: 2022-12-09 15:53:02
img: https://res.cloudinary.com/practicaldev/image/fetch/s--eiFpHWP3--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/l7ci1s4hjn2yrmovjh0s.png
---

# 解决使用 useRef 时 Cannot assign to 'current' because it is a read-only property 错误

这个错误只发生在 使用 `useRef` 时，初始化数据指定的是 `null`，但是泛型类型总却没有指定 `null`，就会发生下述问题。更多见于 `Object` 类型的初始化。因为 `Object` 类型的数据，我们大都喜欢使用 `null`来进行初始化。就会发生以上的报错。

**比如下列例子:**

```tsx
import { useRef, useEffect } from 'react'

interface PersonProp {
  name: string
  age: number
}

const Demo = () => {
  const person = useRef<PersonProp>(null)

  useEffect(() => {
    person.current = { name: 'Tom', age: 18 }
  }, [])
}

export default Demo
```

![](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/20221209161902.png)

这个问题在于，当我们将 `null` 作为初始值传递到 `useRef` 中时，但是我们泛型约束中没有包括`null` 类型，则创建了一个不可变的`ref`对象。所以会报 `readonly` 错误。

想让其不报错，很简单，在类型声明时，将 `null` 加入，改为联合类型就行了。

```tsx
const person = useRef<PersonProp | null>(null)
```

![](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/20221209161927.png)
