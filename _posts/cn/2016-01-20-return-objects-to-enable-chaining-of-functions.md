---
layout: post

title: Return objects to enable chaining of functions
tip-number: 20
tip-username: WakeskaterX
tip-username-profile: https://twitter.com/WakeStudio
tip-tldr: When creating functions on an object in Object Oriented Javascript, returning the object in the function will enable you to chain functions together.

categories:
    - en
---


## #20 - 返回对象的函数实现链式调用

> 20/01/2016 by [@WakeskaterX](https://twitter.com/WakeStudio)

使用面向对象的方法实现javascript对象时，对象的函数属性的返回值对象可以将所有函数方法链在一起，即可使用链式调用。

```javascript
function Person(name) {
  this.name = name;

  this.sayName = function() {
    console.log("Hello my name is: ", this.name);
    return this;
  };

  this.changeName = function(name) {
    this.name = name;
    return this;
  };
}

var person = new Person("John");
person.sayName().changeName("Timmy").sayName();
```



