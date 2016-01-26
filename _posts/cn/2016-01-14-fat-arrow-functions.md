---
layout: post

title: Fat Arrow Functions
tip-number: 14
tip-username: pklinger
tip-username-profile: https://github.com/pklinger/
tip-tldr: Introduced as a new feature in ES6, fat arrow functions may come as a handy tool to write more code in fewer lines

categories:
    - en
---


## #14 - ES6的胖箭头函数

> 13/01/2016 by [@pklinger](https://github.com/pklinger/)

作为ES6的一个新功能，胖箭头(fat arrow)函数或许是个能让我们写更少的代码却能完成更多工作的便捷工具。这个名字源于其语法符号'=>'。胖当然是相较于瘦箭头'->'而言 :) 。一些同学可能已经知道这类功能是借签于其它几种不同的编程语言，如Haskell的'lambada表达式'它们分别表示各自的'匿名函数'. 之所以称为匿名函数是因为这些箭头函数并没有函数描述名称。

### 有什么益处？

- 语法层面：代码更简洁（LOC），不用再没完没了的敲'function'了
- 语义层面：关联当前上下文的this关键字

### 简单的例子

下面两段代码功能相同，比较一下，相信你很快就能理解箭头函数的作用。

```javascript
// general syntax for fat arrow functions
param => expression

// 也可以写在括号内
// 使用括号时，在括号内可以写多个参数
(param1 [, param2]) => expression


// using functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// using fat arrow
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

正如你所见，箭头函数在这种情况下可节省你敲括号,'function'和'return'等关键字的时间。建议就是不论什么情况下总是用括号括住参数，因为括号里可以写多个参数，如`(x,y) => x+y`。这种写法可以让我们忽略它在不同场景下的不同的法，尽管上面的代码也可以写为：`x => x*x`。目前为止我们涉及的都在语法层面，它让代码更简洁，更易读。



### this绑定

使用胖箭头函数还有另一个益处。在JS中, `this`一直就是容易出错的地方。使用箭头函数，你再也不用担心`.bind(this)`或者设置`that=this`了，因为箭头函数会根据上下文环境自动选择`this`对象。看下面这个[例子](https://jsfiddle.net/pklinger/rw94oc11/)：

```javascript
// globally defined this.i
this.i = 100;

var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();

// 错误例子 
function CounterA() {
  // CounterA's `this` instance (!! gets ignored here)
  this.i = 0;
  setInterval(function () {
    // `this` 关联到全局对象，而不是CounterA
    // 因此i是由100开始，而不是0
    this.i++;
    document.getElementById("counterA").innerHTML = this.i;
  }, 500);
}

// 手动绑定 that = this
function CounterB() {
  this.i = 0;
  var that = this;
  setInterval(function() {
    that.i++;
    document.getElementById("counterB").innerHTML = that.i;
  }, 500);
}

// using .bind(this)
function CounterC() {
  this.i = 0;
  setInterval(function() {
    this.i++;
    document.getElementById("counterC").innerHTML = this.i;
  }.bind(this), 500);
}

// fat arrow function
function CounterD() {
  this.i = 0;
  setInterval(() => {
    this.i++;
    document.getElementById("counterD").innerHTML = this.i;
  }, 500);
}
```

更多箭头函数资料请查看[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)。如果要看不同语法选项请访问[此站点](http://jsrocks.org/2014/10/arrow-functions-and-their-scope/)。

译注：  
LOC: line of code


