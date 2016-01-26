---
layout: post

title: Check if a property is in a Object
tip-number: 10
tip-username: loverajoel
tip-username-profile: https://www.twitter.com/loverajoel
tip-tldr: These are ways to check if a property is present in an object.

categories:
    - en
---

## #10 - 对象属性检测

> 10/01/2016 by [@loverajoel](https://www.twitter.com/loverajoel)

当你必须检查属性是否存在于一个对象时，你可能正在做这样的事情:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject['name']) { ... }
```

这没问题(其实会有问题，当name是一个数字0时返回false。请参考下文的讨论链接)，但你需要知道还有另外两个原生方法也可以完成这个工作：`in`运算符和`Object.hasOwnProperty`方法，所有继承自Object的对象都拥有这两个方法。

来看下他们最大的区别：

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf 继承自原型链接
'valueOf' in myObject; // true
```

两者最大的不同在于属性层级检测的深度。换言之`hasOwnProperty`方法只在属性为对象直接拥有时才返回true, 而`in`运算符并不区分属性是对象创建还是继承自原型链。

再看一个示例：

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

有兴趣可以[点这](https://jsbin.com/tecoqa/edit?js,console)(jsbin)直接测试上面代码。

同样也推荐[阅读](https://github.com/loverajoel/jstips/issues/62)这篇关于检测已知对象属性的常见误区的贴子。



