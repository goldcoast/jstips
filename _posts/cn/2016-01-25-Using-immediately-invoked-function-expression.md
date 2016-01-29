---
layout: post

title: 使用立即执行函数表达式
tip-number: 25
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.

categories:
    - cn
---

## #25 - 使用立即执行函数表达式

> by [@rishantagarwal](https://github.com/rishantagarwal)


"Iffy" ( IIFE - immediately invoked function expression) 即立即执行函数表达式, 它在Javascript中有很重要的用途。

```javascript

(function() {
 // Do something​
 }
)()

```

上面代码是个典型匿名函数表达式，它会马上执行，在Javascript的一些特定场景中这是一种重要的用法。

用括号将里面的匿名函数转换成一个函数表达式或者说变量表达式，这样我们就有一个没有命名的函数表达式而不用再到全局作用域或其它什么地方定义匿名函数了。

同样的，我们也可以创建一个带函数名的立即执行函数：

```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction(); // Output --> Nothing for today !!​
```

更多详情，请打开下面的链接 -  
1. [Link 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax)  
2. [Link 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/)  

演示:
[jsPerf](http://jsperf.com/iife-with-call)

