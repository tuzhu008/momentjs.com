---
title: 对象
version: 2.2.1
signature: |
  moment({unit: value, ...});
---


```javascript
moment({ hour:15, minute:10 });
moment({ y    :2010, M     :3, d   :5, h    :15, m      :10, s      :3, ms          :123});
moment({ year :2010, month :3, day :5, hour :15, minute :10, second :3, millisecond :123});
moment({ years:2010, months:3, days:5, hours:15, minutes:10, seconds:3, milliseconds:123});
moment({ years:2010, months:3, date:5, hours:15, minutes:10, seconds:3, milliseconds:123});
moment({ years:'2010', months:'3', date:'5', hours:'15', minutes:'10', seconds:'3', milliseconds:'123'});  // from 2.11.0
```

您可以通过指定对象中的某些单元来创建一个 moment。

省略单元默认为 0 或当前日期、月和年。

`day` 和 `date` 键都代表 day-of-the-month。

`date` 被添加进 **2.8.4**。

**2.11.0**. 从 **2.11.0** 开始，字符串（如最后一行所示）值被支持。

注意，像 `moment(Array)`  和  `new Date(year, month, date)`，月份的起始索引为 0
