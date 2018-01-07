---
title: 当前时间
version: 1.0.0
signature: |
  moment();
  // From 2.14.0 onward, also supported
  moment([]);
  moment({});
---


要获得当前的日期和时间，只需不带参数地调用 `moment()`。

```javascript
var now = moment();
```

这与调用 `moment(new Date())` 基本相同。

**注意:** 从 **2.14.0** 版本开始， `moment([])` 和 `moment({})`  也返回当前时间。在 2.14.0 之前，它们被作用今天的默认值，那很随意的，所以它被改变了。
