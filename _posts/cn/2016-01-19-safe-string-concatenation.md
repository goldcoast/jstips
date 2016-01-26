---
layout: post

title: Safe string concatenation
tip-number: 19
tip-username: gogainda
tip-username-profile: https://twitter.com/gogainda
tip-tldr: Suppose you have a couple of variables with unknown types and you want to concatenate them in a string. To be sure that the arithmetical operation is not be applied during concatenation, use concat

categories:
    - en
---


## #19 - 安全的连接字符串方法

> 19/01/2016 by [@gogainda](https://twitter.com/gogainda)

假设你有多个未知类型的变量，并且你要将他们连接成一个字符串。为确保在连接的过程中不会将算术运算符连接进去，可以使用`concat`方法：

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = ''.concat(one, two, three); //"123"
```

这个方法可以确保结果是你预期的。相比之下，如果使用‘+’连接则可能会出现非预期结果：

```javascript
var one = 1;
var two = 2;
var three = '3';

var result = one + two + three; //"33" instead of "123"
```

从性能上讲，使用[连接符号(+)](http://www.sitepoint.com/javascript-fast-string-concatenation/)和使用`concat`基本相同。

从[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat)上可以了解到更多`concat`的资料。

