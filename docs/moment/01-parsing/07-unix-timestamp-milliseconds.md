---
title: Unix 时间戳 (毫秒)
version: 1.0.0
signature: |
  moment(Number);
---


类似于 `new Date(Number)`，您可以通过传递一个表示自 Unix Epoch (1970年1月1日 12AM UTC)以来的*毫秒数*的整数值来创建一个时刻。

```javascript
var day = moment(1318781876406);
```

<a href="https://www.ecma-international.org/ecma-262/6.0/#sec-time-values-and-time-range" target="_blank" > 注意: ECMAScript 称之为 "Time Value" </a>
