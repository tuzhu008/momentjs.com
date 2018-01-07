---
title: 取值
version: 2.2.1
signature: |
  moment().get('year');
  moment().get('month');  // 0 to 11
  moment().get('date');
  moment().get('hour');
  moment().get('minute');
  moment().get('second');
  moment().get('millisecond');
---


字符串 getter。 在一般情况下

```javascript
moment().get(unit) === moment()[unit]()
```

单位不区分大小写，支持复数和短格式：year (years,
y), month (months, M), date (dates, D), hour (hours, h), minute (minutes, m),
second (seconds, s), millisecond (milliseconds, ms)。
