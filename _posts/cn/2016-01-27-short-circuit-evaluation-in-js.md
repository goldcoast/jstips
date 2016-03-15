---
layout: post

title: Short circuit evaluation in JS.JS中的短路求值。
tip-number: 27
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 短路求值是指，只有当第一个参数不足以确定表达式的值时第二个参数（表达式）才执行或求值。 与运算`&&`的第一个参数表达式为 false 时，整个表达式的值肯定是 false; 或运算`||` 第一个参数表达式为 true 时，整个表达式的值肯定为 true。


categories:
    - cn
---


[短路求值](https://en.wikipedia.org/wiki/Short-circuit_evaluation) 是指，只有当第一个参数不足以确定表达式的值时第二个参数（表达式）才执行或求值。 与运算`&&`的第一个参数表达式为 false 时，整体的值肯定是 false; 或运算`||` 第一个参数表达式为 true 时，整体的值肯定为 true。

接下来测试 `test` 条件和 `isTrue`、`isFalse`方法。

```js
var test = true;
var isTrue = function(){
  console.log('Test is true.');
};
var isFalse = function(){
  console.log('Test is false.');
};

```
使用逻辑与 - `&&`。

```js
// 普通的if语句
if(test){
  isTrue();    // 测试为 true 的情况
}

// 上面也可以使用'&&'运算实现

( test && isTrue() );  // 测试为 true 的情况
```
使用逻辑或 - `||`。

```js
test = false;
if(!test){
  isFalse();    // 测试为 false的情况
}

( test || isFalse());  // 测试为 false的情况
```
逻辑或也可以用来设置函数参数的默认值。

```js
function theSameOldFoo(name){ 
  name = name || 'Bar' ;
  console.log("My best friend's name is " + name);
}
theSameOldFoo();  // My best friend's name is Bar
theSameOldFoo('Bhaskar');  // My best friend's name is Bhaskar
```

逻辑与可以用来规避读取一个undefined对象属性的异常。
例如：
```js
var dog = { 
  bark: function(){
    console.log('Woof Woof');
  }
};

// 调用 dog.bark();
dog.bark(); // Woof Woof.

// 但如果dog没有定义，则dog.bark()会抛出一个错误 "Cannot read property 'bark' of undefined."
// 规避这个错误可以使用 &&

dog&&dog.bark();   // 它只在dog定义好了才会执行dog.bark()方法 

```


