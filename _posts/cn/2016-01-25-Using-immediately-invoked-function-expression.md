---
layout: post

title: Using immediately invoked function expression 使用立即执行函数表达式
tip-number: 25
tip-username: rishantagarwal 
tip-username-profile: https://github.com/rishantagarwal
tip-tldr: Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.

categories:
    - en
---

Called as "Iffy" ( IIFE - immediately invoked function expression) is an anonymous function expression that is immediately invoked and has some important uses in Javascript.

"Iffy" ( IIFE - immediately invoked function expression) 即：立即执行函数表达式是一个匿名函数且它在Javascript中有很重要的用途。



```javascript

(function() {
 // Do something​
 }
)()

```

It is an anonymous function expression that is immediately invoked, and it has some particularly important uses in JavaScript.
上面就是个匿名函数表达式，它会立即执行，在Javascript的一些特定场景中这是一种重要的用法。

The pair of parenthesis surrounding the anonymous function turns the anonymous function into a function expression or variable expression. So instead of a simple anonymous function in the global scope, or wherever it was defined, we now have an unnamed function expression.
第一对括号将里面的匿名函数转换成了一个函数表达式或者说变量表达式。这样就不用在全局或其它什么地方定义一个匿名函数了。

Similarly, we can even create a named, immediately invoked function expression:
同样的，也可以创建一个带函数名的立即执行函数：
```javascript
(someNamedFunction = function(msg) {
	console.log(msg || "Nothing for today !!")
	}) (); // Output --> Nothing for today !!​
​
someNamedFunction("Javascript rocks !!"); // Output --> Javascript rocks !!
someNamedFunction(); // Output --> Nothing for today !!​
```

For more details, check the following URL's - 
1. [Link 1](https://blog.mariusschulz.com/2016/01/13/disassembling-javascripts-iife-syntax) 
2. [Link 2](http://javascriptissexy.com/12-simple-yet-powerful-javascript-tips/) 

Performance:
[jsPerf](http://jsperf.com/iife-with-call)