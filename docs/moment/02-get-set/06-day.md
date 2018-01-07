---
title: 星期
version: 1.3.0
signature: |
  moment().day(Number|String);
  moment().day(); // Number
  moment().days(Number|String);
  moment().days(); // Number
---

获取或设置星期几。

此方法可用于设置星期几，星期天为 0，星期六为 6。

如果超出范围，则会冒泡到其他星期。

```javascript
moment().day(-7); // last Sunday (0 - 7)
moment().day(7); // next Sunday (0 + 7)
moment().day(10); // next Wednesday (3 + 7)
moment().day(24); // 3 Wednesdays from now (3 + 7 + 7 + 7)
```

**注意:** `Moment#date` 是每月的日期，而 `Moment#day` 是一周中一天。

在 **2.1.0** 种，也支持星期名称。这是在 moment 当前的语言环境中被解析。

```javascript
moment().day("Sunday");
moment().day("Monday");
```
