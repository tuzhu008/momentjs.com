---
title: ASP.NET JSON Date
version: 1.3.0
signature: |
  moment(String);
---

默认情况下，Microsoft Web API 以适当的 iso-8601 格式返回 JSON 日期，但更老的 ASP.NET 技术可以以 JSON 的格式返回日期，如 `/Date(1198908717056)/` 或 `/Date(1198908717056-0700)/`。

如果一个匹配该格式的字符串被传入，它将被正确解析。

```javascript
moment("/Date(1198908717056-0700)/"); // 2007-12-28T23:11:57.056-07:00
```
