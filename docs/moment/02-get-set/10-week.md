---
title: 第几周
version: 2.0.0
signature: |
  moment().week(Number);
  moment().week(); // Number
  moment().weeks(Number);
  moment().weeks(); // Number
---

获取或设置一年的一周。

由于不同的语言环境定义了不同的年份编号，Moment.js 添加了 `moment#week` 来获取/设置本地化的一年的一周。

一年中的一周会根据一周中的第一天（星期日，星期一等）以及哪一周是一年中的第一周而有所不同。

例如，在美国，周日是一周中的第一天。 1月1日的一周是今年的第一周。

在法国，星期一是一周中的第一天，而1月4日是本年的第一周。

`moment#week` 的输出将取决于 moment 的 [locale](#/i18n)。

设置一年中的周时，星期几保留。
