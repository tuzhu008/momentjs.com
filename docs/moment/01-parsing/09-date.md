---
title: Date 对象
version: 1.0.0
signature: |
  moment(Date);
---

你可以使用一个已经存在的 `Date` 对象来创建一个 `Moment`。

```javascript
var day = new Date(2011, 9, 16);
var dayWrapper = moment(day);
```

这克隆了 `Date` 对象;对 `Date` 的进一步更改不会影响 `Moment`，反之亦然。
