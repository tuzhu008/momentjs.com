---
title: 取值/赋值
---


Moment.js 使用重载的 getter 和 setter。 您可能熟悉这个模式，因为它在 jQuery 中使用。

不带参数调用这些方法就像一个 getter，用一个参数调用它们就像一个 setter。

这些映射到原生 `Date` 对象的相应函数。


```javascript
moment().seconds(30).valueOf() === new Date().setSeconds(30);
moment().seconds()   === new Date().getSeconds();
```

如果你在 [UTC 模式](#/manipulating/utc/) 种，他们将映射到 UTC 等价物。

```javascript
moment.utc().seconds(30).valueOf() === new Date().setUTCSeconds(30);
moment.utc().seconds()   === new Date().getUTCSeconds();
```

为了方便起见，单数和复数的方法名都存在于版本 **2.0.0** 中。

**注意:** 当这些方法被用作 setter 的时候，它们都会改变原始的 moment。

**Note:** 从 **2.19.0** 开始，传递 `NaN` 到任何 setter 将不会有任何操作。在 **2.19.0** 之前，它以一种错误的方式宣告 moment 是无效的。
