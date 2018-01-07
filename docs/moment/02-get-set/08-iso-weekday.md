---
title: 星期(ISO)
version: 2.1.0
signature: |
  moment().isoWeekday(Number);
  moment().isoWeekday(); // Number
---


获取或设置[ ISO 星期几]（https://en.wikipedia.org/wiki/ISO_week_date），其中 `1` 为星期一，`7` 为星期日。

与 `moment#day` 一样，如果超出范围，则会冒泡到其他星期。

```javascript
moment().isoWeekday(1); // Monday
moment().isoWeekday(7); // Sunday
```

一天的名字也被支持。 这是在当前的语言环境中被解析。

```javascript
moment().isoWeekday("Sunday");
moment().isoWeekday("Monday");
```
