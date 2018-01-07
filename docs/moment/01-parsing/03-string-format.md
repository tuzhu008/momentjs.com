---
title: 字符串 + 格式
version: 1.0.0
signature: |
  moment(String, String);
  moment(String, String, String);
  moment(String, String, Boolean);
  moment(String, String, String, Boolean);
---

如果您知道输入字符串的格式，您可以使用它来解析 moment。

```javascript
moment("12-25-1995", "MM-DD-YYYY");
```

解析器忽略了非字母数字字符，因此下面两个都将返回相同的内容。

```javascript
moment("12-25-1995", "MM-DD-YYYY");
moment("12/25/1995", "MM-DD-YYYY");
```

解析符号类似于在 `moment#format` 中使用的格式化符号。

#### Year, month, and day tokens

| Input       |     示例          | 描述     |
| ----------- | ---------------- | ----------- |
| `YYYY`      | `2014`           | 4 or 2 digit year 年|
| `YY`        | `14`             | 2 digit year 年|
| `Y`         | `-25`            | Year with any number of digits and sign |
| `Q`         | `1..4`           | Quarter of year. Sets month to first month in quarter. 季度|
| `M MM`      | `1..12`          | Month number 月|
| `MMM MMMM`  | `Jan..December`  | Month name in locale set by `moment.locale()` |
| `D DD`      | `1..31`          | Day of month |
| `Do`        | `1st..31st`      | Day of month with ordinal |
| `DDD DDDD`  | `1..365`         | Day of year |
| `X`         | `1410715640.579` | Unix timestamp |
| `x`         | `1410715640579`  | Unix ms timestamp |

从 **2.10.5** 开始，`YYYY` 支持 2尾数的年份，并将其转为接近 2000 的年份（与 `YY` 相同）

`Y` 被添加进 **2.11.1**。它将匹配任何数字，有符号的或无符号的。它对于那些不是 4 位数或者是在公元前的年份来说是有用的。它可以用在任何一年。

#### Week year, week, and weekday tokens

对于这些，小写标记使用区域设置感知周开始日期，而大写标记使用 [ISO week date](https://en.wikipedia.org/wiki/ISO_week_date) 开始日期。

| Input       | Example          | Description |
| ----------- | ---------------- | ----------- |
| `gggg`      | `2014`           | Locale 4 digit week year |
| `gg`        | `14`             | Locale 2 digit week year |
| `w ww`      | `1..53`          | Locale week of year |
| `e`         | `0..6`           | Locale day of week |
| `ddd dddd`  | `Mon...Sunday`   | Day name in locale set by `moment.locale()` |
| `GGGG`      | `2014`           | ISO 4 digit week year |
| `GG`        | `14`             | ISO 2 digit week year |
| `W WW`      | `1..53`          | ISO week of year |
| `E`         | `1..7`           | ISO day of week |

#### Hour, minute, second, millisecond, and offset tokens

| Input          | Example  | Description |
| -------------- | -------- | ----------- |
| `H HH`         | `0..23`  | Hours (24 hour time) |
| `h hh`         | `1..12`  | Hours (12 hour time used with `a A`.) |
| `k kk`         | `1..24`  | Hours (24 hour time from 1 to 24) |
| `a A`          | `am pm`  | Post or ante meridiem (Note the one character `a p` are also considered valid) |
| `m mm`         | `0..59`  | Minutes |
| `s ss`         | `0..59`  | Seconds |
| `S SS SSS`     | `0..999` | Fractional seconds |
| `Z ZZ`         | `+12:00` | Offset from UTC as `+-HH:mm`, `+-HHmm`, or `Z` |

From version **2.10.5**: fractional second tokens length 4 up to 9 can parse
any number of digits, but will only consider the top 3 (milliseconds). Use if
you have the time printed with many fractional digits and want to consume the
input.

从版本 **2.10.5** ：部分的秒数符号长度 4 到 9 可以解析任意数量的数字，但只会考虑前 3（毫秒）。如果您有要打印的带着许多小数位的时间，并且想要消耗（consume）输入，请使用。

请注意，提供的 `S` 字符的数量仅在严格模式下解析时才有意义。在标准模式下，`S`, `SS`, `SSS`, `SSSS` 全部相同，并解释为秒的小数部分。 例如 `.12` 总是 120 毫秒，通过 `SS` 不会导致它被解释为 12 毫秒。

区域识别日期和时间格式也可以使用LT LTS L LL LLL LLLL。 除了已添加的“LTS”以外，它们被添加到版本** 2.2.1 **中
Note that the number of `S` characters provided is only relevant when parsing in strict mode.
In standard mode, `S`, `SS`, `SSS`, `SSSS` are all equivalent, and interpreted as fractions of a second.
For example, `.12` is always 120 milliseconds, passing `SS` will not cause it to be interpreted as 12 milliseconds.

使用 `LT LTS L LL LLL LLLL`， 语言环境感知日期和时间格式也是可用的，它们被添加到版本 **2.2.1** 中，除了在 **2.8.4** 被添加的 `LTS` 之外。

`Z ZZ` 被添加到版本 **1.2.0**.

`S SS SSS` 被添加到版本 **1.6.0**.

`X` 被添加到版本 **2.0.0**.

`k kk` 被添加到版本 **2.18.0**

除非您指定一个时区偏移，否则解析一个字符串将在当前时区创建一个日期。

```js
moment("2010-10-20 4:30",       "YYYY-MM-DD HH:mm");   // 被解析为 4:30 local time
moment("2010-10-20 4:30 +0000", "YYYY-MM-DD HH:mm Z"); // 被解析为 4:30 UTC
```

如果解析输入的结果 moment 不存在，那么 `moment#isValid` 将返回 false。

```js
moment("2010 13",           "YYYY MM").isValid();     // false (not a real month)
moment("2010 11 31",        "YYYY MM DD").isValid();  // false (not a real day)
moment("2010 2 29",         "YYYY MM DD").isValid();  // false (not a leap year)
moment("2010 notamonth 29", "YYYY MMM DD").isValid(); // false (not a real month name)
```

在 **2.0.0** 版本中，一个语言环境的键可以作为第三个参数传递给 `moment()` 和 `moment.utc()`。

```js
moment('2012 juillet', 'YYYY MMM', 'fr');
moment('2012 July',    'YYYY MMM', 'en');
```

Moment 的解析器是非常宽容的，这可能导致不需要的/不可预期的行为。

例如，以下行为可以被观察到:

```javascript
moment('2016 is a date', 'YYYY-MM-DD').isValid() //true, 2016 was matched
```

在 **2.13.0**  之前，解析器显示了以下行为。这已经被修正。

```javascript
moment('I am spartacus', 'h:hh A').isValid();     //true - the 'am' matches the 'A' flag.
```

在 **2.3.0** 版本中，您可以为最后一个参数指定一个布尔值，以便使用严格的解析。严格的解析要求格式和输入完全匹配，*包括分隔符*。

```javascript
moment('It is 2012-05-25', 'YYYY-MM-DD').isValid();       // true
moment('It is 2012-05-25', 'YYYY-MM-DD', true).isValid(); // false
moment('2012-05-25',       'YYYY-MM-DD', true).isValid(); // true
moment('2012.05.25',       'YYYY-MM-DD', true).isValid(); // false
```

您可以使用语言环境和严格性。

```javascript
moment('2012-10-14', 'YYYY-MM-DD', 'fr', true);
```

严格的解析通常是最好的解析选项。要获得更多关于选择严格的 vs 宽容解析的信息，请参阅<a href="/guides/#/parsing/">解析指南</a>。

#### 解析两位数的年份

默认情况下，假设 68 以上的两位数字年份是在 1900 的，而 68 或以下的假设是在 2000 年。 这可以通过替换 `moment.parseTwoDigitYear` 方法来改变。 这个方法唯一的参数是一个包含用户输入两位数年份的字符串，并且应该以整数形式返回年份。

```javascript
moment.parseTwoDigitYear = function(yearString) {
    return parseInt(yearString) + 2000;
}
```

#### 解析粘合的小时和分钟

从 **2.11.0** 开始，支持解析 `hmm`, `Hmm`, `hmmss` 和 `Hmmss`:

```javascript
moment("123", "hmm").format("HH:mm") === "01:23"
moment("1234", "hmm").format("HH:mm") === "12:34"
```
