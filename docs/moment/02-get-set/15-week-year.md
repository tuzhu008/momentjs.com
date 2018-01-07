---
title: 周-年(区域标准)
version: 2.1.0
signature: |
  moment().weekYear(Number);
  moment().weekYear(); // Number
---


根据地区的情况，获取或设置 week-year。

因为第一周的第一天并不总是在每年的第一天，有时 week-year 会和月年不同。

例如，在美国，包含 1月1日的一周总是第一周。在美国，周也从周日开始。如果 1月1日是星期一，12月31日将属于 1月1日，因此与 1月1日相同。12月30日和 12月31日所在的年份不同。
