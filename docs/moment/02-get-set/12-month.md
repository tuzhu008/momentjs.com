---
title: 月
version: 1.0.0
signature: |
  moment().month(Number|String);
  moment().month(); // Number
  moment().months(Number|String);
  moment().months(); // Number
---

获取或设置月份。

接受 0 到 11 之间的数字。如果超出范围，则会冒泡到年份。

**Note:** 月份是 0 索引，所以 1 月份是 0。

**2.1.0** 中，一个月份的名字也被支持。 这是在当前的语言环境中解析。

```javascript
moment().month("January");
moment().month("Feb");
```

在版本 **2.1.0** 之前，如果一个 moment 改变了月份，并且新月没有足够的号数来维持当前的月份，那么将会溢出到下个月。

从版本 **2.1.0** 开始，更改为被限制在目标月份的末尾。

```javascript
// before 2.1.0
moment([2012, 0, 31]).month(1).format("YYYY-MM-DD"); // 2012-03-02
// after 2.1.0
moment([2012, 0, 31]).month(1).format("YYYY-MM-DD"); // 2012-02-29
```

**2.16.0** 弃用 ``moment().months()``。 使用 ``moment().month()`` 代替。
