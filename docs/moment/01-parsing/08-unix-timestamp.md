---
title: Unix 时间戳 (秒)
version: 1.6.0
signature: |
  moment.unix(Number)
---

要从一个时间戳 (从 Unix Epoch 开始的 *秒数*)创建 moment，请使用 `moment.unix(Number)`。

```javascript
var day = moment.unix(1318781876);
```

这将实现为 `moment(timestamp * 1000)`， so partial seconds in the input timestamp are included.（在输入时间戳中包含了部分秒。）

```javascript
var day = moment.unix(1318781876.721);
```

**注意:** 尽管 Unix 时间戳是基于 UTC 的，但是这个函数在*本地*模式中创建了一个 moment 对象。如果您需要 UTC，那么随后调用 `.utc()`, 如:

```javascript
var day = moment.unix(1318781876).utc();
```
