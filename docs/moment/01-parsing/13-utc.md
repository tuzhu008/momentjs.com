---
title: UTC
version: 1.5.0
signature: |
  moment.utc();
  moment.utc(Number);
  moment.utc(Number[]);
  moment.utc(String);
  moment.utc(String, String);
  moment.utc(String, String[]);
  moment.utc(String, String, String);
  moment.utc(String, String, Boolean);
  moment.utc(String, String, String, Boolean);
  moment.utc(Moment);
  moment.utc(Date);
---

默认情况下，moment 以本地事件进行解析和显示。

如果你想以 UTC 解析和显示 moment，你可以使用 `moment.utc()` 来代替 `moment()`。

这就给我们带来了 Moment.js UTC 模式的一个有趣的特性。

在 UTC 模式下，所有显示方法将以 UTC 时间显示，而不是本地时间。

```javascript
moment().format();     // 2013-02-04T10:35:24-08:00
moment.utc().format(); // 2013-02-04T18:35:24+00:00
```

另外，在 UTC 模式中，所有 getter 和 setter 将在内部使用 `Date#getUTC*` 和 `Date#setUTC*` 方法，而不是日期 `Date#get*` 和 `Date#set*` 方法。

```javascript
moment.utc().seconds(30).valueOf() === new Date().setUTCSeconds(30);
moment.utc().seconds()   === new Date().getUTCSeconds();
```

值得注意的是，尽管显示器上的显示不同，但它们都是同一时刻。

```javascript
var a = moment();
var b = moment.utc();
a.format();  // 2013-02-04T10:35:24-08:00
b.format();  // 2013-02-04T18:35:24+00:00
a.valueOf(); // 1360002924000
b.valueOf(); // 1360002924000
```

任何使用 `moment.utc()` 创建的 moment 都将处在 UTC 模式中，而使用 `moment()` 创建的则不是。

要切换 UTC 与 本地时间，你可以使用 [moment#utc](#/manipulating/utc/) 或 [moment#local](#/manipulating/local/)。

```javascript
var a = moment.utc([2011, 0, 1, 8]);
a.hours(); // 8 UTC
a.local();
a.hours(); // 0 PST
```
