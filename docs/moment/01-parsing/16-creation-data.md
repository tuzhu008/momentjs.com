---
title: 创建数据
version: 2.11.0
signature: |
  moment().creationData();
---

一个 moment 对象被创建之后，所有的输入都可以通过 `creationData()` 方法来访问：

<!-- skip-example -->
```javascript
moment("2013-01-02", "YYYY-MM-DD", true).creationData() === {
    input: "2013-01-02",
    format: "YYYY-MM-DD",
    locale: Locale obj,
    isUTC: false,
    strict: true
}
```
