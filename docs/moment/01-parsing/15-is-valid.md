---
title: 合法性校验
version: 1.7.0
signature: |
  moment().isValid();
---


Moment 应用比 `Date` 构造函数更严格的初始化规则。

```js
new Date(2013, 25, 14).toString(); // "Sat Feb 14 2015 00:00:00 GMT-0500 (EST)"
moment([2015, 25, 35]).format();   // 'Invalid date'
```

您可以使用 `moment#isValid` 来检查当前的日期是否为有效日期。您可以使用 `moment#parsingFlags` 检查 `#isValid` 使用的度量标准，它返回一个对象。

以下解析标记导致无效的日期：

 * `overflow`: 一个日期字段的溢出，例如一个月的第十三个月，第三十二天（或非闰年的二月二十九日），一年的第 367 天等等， `overflow` 包含无效单元单位的索引，用来匹配 `#invalidAt`（见下文）; `-1` 表示没有溢出。
 * `invalidMonth`: 无效的月份名称，例如 ```moment('Marbruary', 'MMMM');```。包含无效的月份字符串本身，否则为空。
 * `empty`: 一个输入字符串，它不包含任何可解析的内容，比如 `moment('this is nonsense');`，则为 `true` 。Boolean。
 * `nullInput`: 是否为 `null` 输入，就像 `moment(null);`。Boolean.
 * `invalidFormat`: 格式列表是否为空，如 `moment('2013-05-25', [])`. Boolean.
 * `userInvalidated`: 一个明确地创建为无效的日期, 如 `moment.invalid()`. Boolean.

 除上述之外，在 **2.13.0** 中，`meridiem` 和 `parsedDateParts` 标志一起工作，以确定日期的有效性。

 * `meridiem`: 指示 meridiem (AM/PM) 是否被解析，如果有的话。String。
 * `parsedDateParts`: 返回一个按照降序排列的被解析的日期部分的数组——即 parsedDateParts[0] === year。如果没有任何部分被提供，但 meridiem 有值，那么日期是无效的。Array。

此外，如果 Moment 在严格模式下被解析，那么这些标记必须是空的，以便 Moment 有效：

 * `unusedTokens`: 表示在输入字符串中找不到格式子串的数组
 * `unusedInput`: 输入子串的数组与格式字符串不匹配

**注意:** Moment 的有效性概念在 **2.2** 和 **2.3** 之间变得更为严格和一致。

此外，你还可以使用 `moment#invalidAt` 来确定日期的哪个单元溢出了。

```javascript
var m = moment("2011-10-10T10:20:90");
m.isValid(); // false
m.invalidAt(); // 5 for seconds
```

返回值具有以下含义：

<ol>
  <li>years</li>
  <li>months</li>
  <li>days</li>
  <li>hours</li>
  <li>minutes</li>
  <li>seconds</li>
  <li>milliseconds</li>
</ol>

**注意:** 如果出现多个错误单元，则返回第一个错误单元（例如，日期有效性可能取决于月份）。

无效的 Moments
===============

如果 moment 是无效的，则在浮点操作中表现得像一个 NaN。

以下所有情况都会产生无效的 moment：
* `invalid.add(unit, value)`
* `another.add(invalid)`
* `invalid.clone()`
* `invalid.diff(another)`
* `invalid.endOf(unit)`
* `invalid.max(another)`
* `another.max(invalid)`
* `invalid.min(another)`
* `another.min(invalid)`
* `invalid.set(unit, value)`
* `invalid.startOf(unit)`
* `invalid.subtract(unit, value)`

以下会产生 `'InvalidDate'` 的本地化版本:
* `invalid.format(anyFmt)` results in `'Invalid Date'` in the current locale
* `invalid.from(another)`
* `another.from(invalid)`
* `invalid.fromNow(suffix)`
* `invalid.to(another)`
* `another.to(invalid)`
* `invalid.toNow(suffix)`
* `invalid.toISOString()`
* `invalid.toString()`

以下返回 `false`:
* `invalid.isAfter(another)`
* `another.isAfter(invalid)`
* `invalid.isBefore(another)`
* `another.isBefore(invalid)`
* `invalid.isBetween(another, another)`
* `invalid.isSame(another)`
* `another.isSame(invalid)`
* `invalid.isSameOrAfter(another)`
* `another.isSameOrAfter(invalid)`
* `invalid.isSameOrBefore(another)`
* `another.isSameOrBefore(invalid)`

这些将返回带有一些结构的 `null` 或 `NaN`：
* `invalid.get(unit)` returns null, as all other named getters
* `invalid.toArray() === [NaN, NaN, NaN, NaN, NaN, NaN]`
* `invalid.toObject()` has all values set to `NaN`
* `invalid.toDate()` returns an invalid Date object
* `invalid.toJSON()` returns null
* `invalid.unix()` returns null
* `invalid.valueOf()` returns null
