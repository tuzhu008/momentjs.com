---
title: 数组
version: 1.0.0
signature: |
  moment(Number[]);
---

你可以使用一个数字数组来创建 momnet，这些参数的镜像被传递给 [new Date()](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Date)。

`[year, month, day, hour, minute, second, millisecond]`

```javascript
moment([2010, 1, 14, 15, 25, 50, 125]); // February 14th, 3:25:50.125 PM
```

任何逝去的年份都是可选的，并会默认为尽可能低的数字

```javascript
moment([2010]);        // January 1st
moment([2010, 6]);     // July 1st
moment([2010, 6, 10]); // July 10th
```

使用数组的构造将在当前时区创建一个日期。要从 UTC 的数组中创建一个日期，请使用 `moment.utc(Number[])`。

```javascript
moment.utc([2010, 1, 14, 15, 25, 50, 125]);
```

**注意:** 因为这将镜像原生的 `Date` 参数，months, hours, minutes, seconds, 和 milliseconds 从 0 开始索引。Years 和 day（日期）索引为 1。

这往往是沮丧的原因，尤其是 months，所以请注意！

如果数组中表示的日期不存在，则 `moment#isValid` 将返回false。

```javascript
moment([2010, 12]).isValid();     // false (not a real month)
moment([2010, 10, 31]).isValid(); // false (not a real day)
moment([2010, 1, 29]).isValid();  // false (not a leap year)
```
