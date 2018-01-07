---
title: 解析
---


Moment.js 为 `Date` 对象创建了一个包装器，而不是修改原生的 `Date.prototype`。要获得这个包装器对象，只需使用一个受支持的输入类型调用 `moment()`。

`Moment` 的原型是通过 `moment.fn` 暴露出来的。如果你想添加你自己的函数，那就是你放置它们的地方。

为了便于参考，`Moment.prototype` 上的任何方法都将在文档中作为 `moment#method` 被引用。因此 `Moment.prototype.format` == `moment.fn.format` == `moment#format`。
