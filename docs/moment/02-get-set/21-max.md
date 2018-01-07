---
title: 最大值
version: 2.7.0
signature: |
  moment.max(Moment[,Moment...]);
  moment.max(Moment[]);
---

返回给定的 moment 实例中最大（最遥远的未来）的。

例如:
```javascript
var a = moment().subtract(1, 'day');
var b = moment().add(1, 'day');
moment.max(a, b);  // b

var friends = fetchFriends(); /* [{name: 'Dan', birthday: '11.12.1977'}, {name: 'Mary', birthday: '11.12.1986'}, {name: 'Stephan', birthday: '11.01.1993'}]*/
var friendsBirthDays = friends.map(function(friend){
    return moment(friend.birthday, 'DD.MM.YYYY');
});
moment.max(friendsBirthDays);  // '11.01.1993'
```
不带参数的该函数将使用当前的时间返回一个 moment 实例。

从版本 **2.10.5** 开始，如果其中一个参数是一个无效的 moment，那么结果就是无效的 moment。

```javascript
moment.max(moment(), moment.invalid()).isValid() === false
moment.max(moment.invalid(), moment()).isValid() === false
moment.max([moment(), moment.invalid()]).isValid() === false
moment.max([moment.invalid(), moment()]).isValid() === false
```
