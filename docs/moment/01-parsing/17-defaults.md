---
title: 默认值
version: 2.2.1
signature: |
  moment("15", "hh")
---

您可以创建一个 moment 对象，只指定一些单元，其余的将默认为当前的日期、月或年，或 0 小时、分钟、秒和毫秒。

当什么都没有被传递的时候，默认为当前时间：
```javascript
moment();  // 当前日期和时间
```
当只有 hours, minutes, seconds 和 milliseconds 被传递的时候，默认为今天：
```javascript
moment(5, "HH");  // today, 5:00:00.000
moment({hour: 5});  // today, 5:00:00.000
moment({hour: 5, minute: 10});  // today, 5:10.00.000
moment({hour: 5, minute: 10, seconds: 20});  // today, 5:10.20.000
moment({hour: 5, minute: 10, seconds: 20, milliseconds: 300});  // today, 5:10.20.300
```

当仅号数和更小的单位被传递时，默认为当前月和年：
```javascript
moment(5, "DD");  // this month, 5th day-of-month
moment("4 05:06:07", "DD hh:mm:ss");  // this month, 4th day-of-month, 05:06:07.000
```
如果未指定年份，默认为今年：
```javascript
moment(3, "MM");  // this year, 3rd month (April)
moment("Apr 4 05:06:07", "MMM DD hh:mm:ss");  // this year, 4th April, 05:06:07.000
```
