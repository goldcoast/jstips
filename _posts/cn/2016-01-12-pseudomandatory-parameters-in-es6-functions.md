---
layout: post

title: Pseudomandatory parameters in ES6 functions
tip-number: 12
tip-username: Avraam Mavridis
tip-username-profile: https://github.com/AvraamMavridis
tip-tldr: In many programming languages the parameters of a function are by default mandatory and the developer has to explicitly define that a parameter is optional.

categories:
    - en
---


## #12 - ES6函数参数的默认值

> 12/01/2016 by [Avraam Mavridis](https://github.com/AvraamMavridis)

在许多编程语言中，函数的参数在默认情况下是必须传递的，除非开发人员明确定义参数是可选的。在Javascript中每个参数都是可选的，但是我们也可以借助ES6的默认参数值功能让参数传递行为更丰富，却并不干扰函数的主要功能。

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
```

代码解读：`_err`方法只做一件事，抛出一个异常。如果第一个参数值没有传递，则使用默认值，`_err`方法将被执行并抛出一个Error。 查看更多示例请点击[MDN(Mozilla's Developer Network)](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)。

译注：另参考了 [ECMAScript6入门](http://es6.ruanyifeng.com/#docs/function#函数参数的默认值)


