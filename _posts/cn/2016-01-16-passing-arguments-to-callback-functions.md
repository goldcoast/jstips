---
layout: post

title: Passing arguments to callback functions
tip-number: 16
tip-username: minhazav
tip-username-profile: https://twitter.com/minhazav
tip-tldr: JavaScript modules and build steps are getting more numerous and complicated, but what about boilerplate in new frameworks?

categories:
    - en
---



## #16 - 回调传参大法

> 16/01/2016 by [@minhazav](https://twitter.com/minhazav)

众所周知，回调函数在正常情况下是不能接收参数的，如：

```javascript
function callback() {
  console.log('Hi human');
}

document.getElementById('someelem').addEventListener('click', callback);
```

但如果你需要传参数怎么办呢？利用闭包可以完成这个任务。看下面例子：

```javascript
function callback(a, b) {
  return function() {
    console.log('sum = ', (a+b));
  }
}

var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));
```

什么是闭包呢？闭包是指函数有自由独立的变量。换句话说，定义在闭包中的函数可以“记忆”它创建时候的环境。参考下[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)文档了解更多闭包信息吧。

在上面代码中，`x`和`y`被调用时都在callback函数的作用域中。

还另一种实现方法是使用`bind`方法，示例：

```javascript
var alertText = function(text) {
  alert(text);
};

document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
以上两种方法在性能有微小的差别，可在[jspref](http://jsperf.com/bind-vs-closure-23)查看其区别

**笔记**：

- 使用闭包方法时，代码要写在callback方法的return函数内。写在return函数外则不会被触发
- 使用bind时，方法内不可以用闭包的写法。

**参考**：
[MDN bind用法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
