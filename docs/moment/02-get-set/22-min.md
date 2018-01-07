---
title: 最小值
version: 2.7.0
signature: |
  moment.min(Moment[,Moment...]);
  moment.min(Moment[]);
---

返回给定的 moment 实例中最小（最遥远的过去）的。

例如
```javascript
var a = moment().subtract(1, 'day');
var b = moment().add(1, 'day');
moment.min(a, b);  // a
moment.min([a, b]); // a
```

不带参数的该函数将使用当前的时间返回一个 moment 实例。

从版本 **2.10.5** 开始，如果其中一个参数是一个无效的 moment，那么结果就是无效的 moment。

```javascript
moment.min(moment(), moment.invalid()).isValid() === false
moment.min(moment.invalid(), moment()).isValid() === false
moment.min([moment(), moment.invalid()]).isValid() === false
moment.min([moment.invalid(), moment()]).isValid() === false
```
