---
layout: post

title: Even simpler way of using `indexOf` as a contains clause
tip-number: 15
tip-username: jhogoforbroke
tip-username-profile: https://twitter.com/jhogoforbroke
tip-tldr: JavaScript by default does not have a contains method. And for checking existence of a substring in a string or an item in an array you may do this.

categories:
    - en
---

## #15 - indexOf更简易的一种包含判断用法

> 15/01/2016 by [@jhogoforbroke](https://twitter.com/jhogoforbroke)

Javascript 没有原生的包含检测的方法。在实际编码中检测一个字符是否包含在一个字符串中，或一个元素是否包含于数组中你可能会用下面的做法：

```javascript
var someText = 'javascript rules';
if (someText.indexOf('javascript') !== -1) {
}

// or
if (someText.indexOf('javascript') >= 0) {
}
```

现在，让我们看下[Expressjs](https://github.com/strongloop/express)是怎么做的吧。

[examples/mvc/lib/boot.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/mvc/lib/boot.js#L26)

```javascript
for (var key in obj) {
  // "reserved" exports
  if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
```

[lib/utils.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/lib/utils.js#L93)

```javascript
exports.normalizeType = function(type){
  return ~type.indexOf('/')
    ? acceptParams(type)
    : { value: mime.lookup(type), params: {} };
};
```

[examples/web-service/index.js](https://github.com/strongloop/express/blob/2f8ac6726fa20ab5b4a05c112c886752868ac8ce/examples/web-service/index.js#L35)

```javascript
// key is invalid
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```

从上可见关键在于[位运算符号](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)~, "按位操作符操作数字的二进制形式，但是返回值依然是标准的JavaScript数值。"

按位非运算符'~'将 -1 转换为0，而在Javascript中0就是false，所以：

```javascript
var someText = 'text';
!!~someText.indexOf('tex'); //sometext contains tex - true
!~someText.indexOf('tex'); //sometext not contains tex - false
~someText.indexOf('asd'); //sometext contains asd - false
~someText.indexOf('ext'); //sometext contains ext - true
```

### String.prototype.includes()

在ES6中介绍了[includes()方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes), 您可以用来判断字符串是否包含另一个字符串:

```javascript
'something'.includes('thing'); // true
```

在ECMAScript 2016 (ES7)甚至可以用在数组上，就跟indexOf一样：

```javascript
!!~[1, 2, 3].indexOf(1); // true
[1, 2, 3].includes(1); // true
```

**不幸的是，支持它的只有Chrome、Firefox、Safari 9及以上版本和Edge。IE11或以前的版本都不支持。**
**所以，最好是在受控的环境下使用它。**

