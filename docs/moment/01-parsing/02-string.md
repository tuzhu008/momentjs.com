---
title: 字符串
version: 1.0.0
signature: |
  moment(String);
---

当从一个字符串创建一个 moment 时，我们首先检查该字符串是否匹配已知的 [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) 格式，然后我们检查字符串是否匹配 [RFC 2822 Date time](https://tools.ietf.org/html/rfc2822#section-3.3)，如果没有找到已知的格式，则回退到 `new Date(string)`。


```javascript
var day = moment("1995-12-25");
```

**警告:** 浏览器对解析字符串的支持是[不一致](http://dygraphs.com/date-formats.html)的。由于没有规范支持哪种格式，在某些浏览器中使用的方法在其他浏览器中不起作用。

<!--
**Note:** This has been the source of a lot of confusion, because moments created via `Date` constructor don't support `isValid` and also work unreliably. So it would be soon deprecated. From version 2.6.0 there is a way to prevent Date constructor usage - just set `moment.createFromInputFallback` to an empty function.
-->

为了得到一致的结果，除了 ISO 8601 字符串之外，您应该使用 [String + Format](#/parsing/string-format/)。

#### 支持的 ISO 8601 字符串

一个 ISO 8601 字符串需要一个日期部分。

```
2013-02-08  # 一个日历日期部分
2013-W06-5  # 一个星期日期部分
2013-039    # 一个序号日期部分

20130208    # Basic (short) full date
2013W065    # Basic (short) week, weekday
2013W06     # Basic (short) week only
2013050     # Basic (short) ordinal date
```

还可以包括时间部分，使用空格或大写 T 将日期部分分隔开。

```
2013-02-08T09            # An hour time part separated by a T
2013-02-08 09            # An hour time part separated by a space
2013-02-08 09:30         # An hour and minute time part
2013-02-08 09:30:26      # An hour, minute, and second time part
2013-02-08 09:30:26.123  # An hour, minute, second, and millisecond time part
2013-02-08 24:00:00.000  # hour 24, minute, second, millisecond equal 0 means next day at midnight

20130208T080910,123      # Short date and time up to ms, separated by comma
20130208T080910.123      # Short date and time up to ms
20130208T080910          # Short date and time up to seconds
20130208T0809            # Short date and time up to minutes
20130208T08              # Short date and time, hours only
```

任何日期部分都可以有一个时间部分。

```
2013-02-08 09  # A calendar date part and hour time part
2013-W06-5 09  # A week date part and hour time part
2013-039 09    # An ordinal date part and hour time part
```

如果包含时间部分，UTC 的偏移也可以作为 `+-HH:mm`，`+-HHmm`，或 `Z` 被包含。

```
2013-02-08 09+07:00            # +-HH:mm
2013-02-08 09-0100             # +-HHmm
2013-02-08 09Z                 # Z
2013-02-08 09:30:26.123+07:00  # +-HH:mm
2013-02-08 09:30:26.123+07     # +-HH
```

**Note:** 在 **1.5.0** 版本中添加了自动跨浏览器 ISO-8601 支持。在 **2.3.0** 版本中增加了对周和序号格式的支持。

如果字符串不匹配上述格式的任何一种，并且不能用 `Date.parse` 解析。`moment#isValid` 将返回 `false`。


```javascript
moment("not a real date").isValid(); // false
```

#### The RFC 2822 date time format

在解析 RFC 2822 日期之前，将清除字符串，以删除任何注释和/或换行符。在这个格式中，额外的字符是合法的，但是不会添加任何东西来创建一个有效的 moment 实例。

在清理之后，字符串将在以下空格分隔的部分中进行验证，所有这些部分都使用英语:

```
6 Mar 17 21:22 UT
6 Mar 17 21:22:23 UT
6 Mar 2017 21:22:23 GMT
06 Mar 2017 21:22:23 Z
Mon 06 Mar 2017 21:22:23 z
Mon, 06 Mar 2017 21:22:23 +0000
```

1. 表示一周中的一天的三个字母后面可以跟一个逗号，这是可选的。
2. 号数 (1 或 2 个数字), 后面跟着是哪个字母的月份和 2 或 4 个数字的年份
3. 两个数字的小时和分钟使用冒号分隔，后面跟着可选的秒，如果提供了秒也用冒号分隔。
4. 时区或偏移量以下列格式之一:
  1. UT : +0000
  2. GMT : +0000
  3. EST | CST | MST | PST | EDT | CDT | MDT | PDT : US time zones*
  4. A - I | K - Z : Military time zones*
  5. Time offset +/-9999

 [*] 参见规范的 [section 4.3](https://tools.ietf.org/html/rfc2822#section-4.3) 获取更多细节。

解析器还确认了周几（day-of-week）(当包括在内)与日期一致。
