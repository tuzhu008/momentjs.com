---
title: 克隆
version: 1.2.0
signature: |
  moment(Moment);
---


所有的 moment 都是可变的。如果你想克隆一个 moment，您可以隐式地或显式地进行。

在 一个 moment 上调用 `moment()` 将克隆它。

```javascript
var a = moment([2012]);
var b = moment(a);
a.year(2000);
b.year(); // 2012
```

此外，你可以调用  `moment#clone` 来克隆一个 moment。

```javascript
var a = moment([2012]);
var b = a.clone();
a.year(2000);
b.year(); // 2012
```
