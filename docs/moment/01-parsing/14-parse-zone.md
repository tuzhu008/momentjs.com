---
title: 时区
version: 2.3.0
signature: |
  moment.parseZone()
  moment.parseZone(String)
  moment.parseZone(String, String)
  moment.parseZone(String, [String])
  moment.parseZone(String, String, Boolean)
  moment.parseZone(String, String, String, Boolean)
---

moment 的字符串解析函数如 `moment(string)` 和 `moment.utc(string)`，接受 offset 信息（如果提供的话），但是将生成的 Moment 对象转换为本地时间或 UTC 时间。相比之下， `moment.parseZone()` 对字符串进行解析，但是将得到的 Moment 对象保持在一个固定偏移的时区，并且在字符串中提供了偏移量。

```javascript
moment.parseZone("2013-01-01T00:00:00-13:00").utcOffset(); // -780 ("-13:00" in total minutes)
moment.parseZone('2013 01 01 05 -13:00', 'YYYY MM DD HH ZZ').utcOffset(); // -780  ("-13:00" in total minutes)
moment.parseZone('2013-01-01-13:00', ['DD MM YYYY ZZ', 'YYYY MM DD ZZ']).utcOffset(); // -780  ("-13:00" in total minutes);
```

它还允许您通过地区和严格参数。

```javascript
moment.parseZone("2013 01 01 -13:00", 'YYYY MM DD ZZ', true).utcOffset(); // -780  ("-13:00" in total minutes)
moment.parseZone("2013-01-01-13:00", 'YYYY MM DD ZZ', true).utcOffset(); // NaN (doesn't pass the strictness check)
moment.parseZone("2013 01 01 -13:00", 'YYYY MM DD ZZ', 'fr', true).utcOffset(); // -780 (with locale and strictness argument)
moment.parseZone("2013 01 01 -13:00", ['DD MM YYYY ZZ', 'YYYY MM DD ZZ'], 'fr', true).utcOffset(); // -780 (with locale and strictness argument alongside an array of formats)
```

`moment.parseZone` 相当于解析字符串并使用 `moment#utcOffset` 来解析时区。

```javascript
var s = "2013-01-01T00:00:00-13:00";
moment(s).utcOffset(s);
```
