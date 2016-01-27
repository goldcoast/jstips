---
layout: post

title: 转换为number类型的快速方法
tip-number: 23
tip-username: sonnyt
tip-username-profile: http://twitter.com/sonnyt
tip-tldr: 字符串转为数值是极为常见的需求，其中简单且高效的实现方式可能就是使用'+'(加号)操作符了。

categories:
    - en
---

## #23 - 转换为number类型的方法

> by [@sonnyt](https://twitter.com/sonnyt)


字符串转为数值是极为常见的需求，其中简单且高效([jspref](https://jsperf.com/number-vs-parseint-vs-plus/29))的实现方式可能就是使用`+`(加号)操作符了。

```javascript
var one = '1';

var numberOne = +one; // Number 1
```

当然也可以使用`-`(减号)操作符，不同的是转换的结果将是负数。

```javascript
var one = '1';

var negativeNumberOne = -one; // Number -1
```