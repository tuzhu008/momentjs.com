---
title: 日期
version: 1.0.0
signature: |
  moment().date(Number);
  moment().date(); // Number
  moment().dates(Number);
  moment().dates(); // Number
---

获取或设置号数。

接受 1 到 31 的数字。如果超出范围，将冒泡到月。

**注意:** `Moment#date` 是每月的日期，而 `Moment#day` 是一周中一天。

**注意:** 如果你串联了多个操作来构造一个日期，你应该从年开始,然后月,然后天，等等。否则你可能会得到意想不到的结果,就像当 `day=31` 并且当前月只有 30 天(同样适用于原生 JavaScript 操纵 `Date`),返回的日期将在次月 1 日。

不好的写法: `moment().date(day).month(month).year(year)`

好的写法: `moment().year(year).month(month).date(day)`

**2.16.0** 弃用 ``moment().dates()``。使用 ``moment().date()`` 代替。
