---
layout: post

title: 用 === 替换 ==
tip-number: 24
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: `==`(或`!=`)操作符在一定情况下会先调用类型转换后再做比较，而`===`(或`!==`)将不执行任何类型转换，直接比较数值和类型，因此比`==`速度更快([jsPref](http://jsperf.com/strictcompare))。

categories:
    - cn
---

## #24 - 用 === 替换 ==

> by [@bhaskarmelkani](https://twitter.com/bhaskarmelkani)

`==`(或`!=`)操作符在一定情况下会先调用类型转换后再做比较，而`===`(或`!==`)将不执行任何类型转换，直接比较数值和类型，因此比`==`速度更快([jsPref](http://jsperf.com/strictcompare))。

```js
[10] ==  10      // is true
[10] === 10      // is false

'10' ==  10      // is true
'10' === 10      // is false

 []  ==  0       // is true
 []  === 0       // is false

 ''  ==  false   // is true but true == "a" is false
 ''  === false   // is false 

```
