---
title: 星期(区域标准)
version: 2.1.0
signature: |
  moment().weekday(Number);
  moment().weekday(); // Number
---

根据区域获取或设置星期几。

如果区域设置将 Monday 指定为一周中的第一天，则 `moment().weekday(0)` 将为 Monday。
如果星期天是一周的第一天，那么“星期一（0）”将是星期天。

与 `moment#day` 一样，如果超出范围，则会泡到其他星期。


```javascript
// when Monday is the first day of the week
moment().weekday(-7); // last Monday
moment().weekday(7); // next Monday
// when Sunday is the first day of the week
moment().weekday(-7); // last Sunday
moment().weekday(7); // next Sunday
```
