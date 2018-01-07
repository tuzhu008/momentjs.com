---
title: 字符串 + 多个格式
version: 1.0.0
signature: |
  moment(String, String[], String, Boolean);
---


如果您不知道输入字符串的确切格式，但知道它可能是其中的一种，则可以使用一组格式。

这与 [String + Format](#/parsing/string-format/) 相同，只是它会尝试将输入与多种格式匹配。

```js
moment("12-25-1995", ["MM-DD-YYYY", "YYYY-MM-DD"]);
```

  从 **2.3.0** 开始，Moment 使用一些简单的启发式来确定使用哪种格式。为了：

 * 优先格式化导致 [有效](#/parsing/is-valid/) 日期越过无效的日期。
 * 优先格式化解析更多字符串的格式，而不是使用更少的格式，即有限进行更严格的解析。
 * 优先格式化数组中较早的。

```js
moment("29-06-1995", ["MM-DD-YYYY", "DD-MM", "DD-MM-YYYY"]); // uses the last format
moment("05-06-1995", ["MM-DD-YYYY", "DD-MM-YYYY"]);          // uses the first format
```

您还可以指定一个地区和严格的参数。它们与单一格式的情况相同。

```js
moment("29-06-1995", ["MM-DD-YYYY", "DD-MM-YYYY"], 'fr');       // uses 'fr' locale
moment("29-06-1995", ["MM-DD-YYYY", "DD-MM-YYYY"], true);       // uses strict parsing
moment("05-06-1995", ["MM-DD-YYYY", "DD-MM-YYYY"], 'fr', true); // uses 'fr' locale and strict parsing
```

**注意:** 解析多种格式比解析单一格式要慢得多。如果您可以避免它，那么解析单一格式的速度要快得多。
