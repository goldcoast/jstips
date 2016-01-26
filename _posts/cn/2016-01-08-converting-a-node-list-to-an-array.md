---
layout: post

title: Converting a Node List to an Array
tip-number: 08
tip-username: Tevko
tip-username-profile: https://twitter.com/tevko
tip-tldr: Here's a quick, safe, and reusable way to convert a node list into an array of DOM elements.

categories:
    - en
---

## #08 - DOM节点集合转为Array

> 08/01/2016 [@Tevko](https://twitter.com/tevko)

`querySelectorAll`方法返回一个类似于数组的集合，我们称其为节点集合(node list). 这种数据结构被称为“类数组对象”(Array-like), 它们看上去类似数组，只是不能使用map，foreach等数组拥有的方法。下边这个方法可以将节点集合对象转换成一个DOM元素的数组，且此方法高效、安全、又可以重用。

```javascript
const nodelist = document.querySelectorAll('div');
const nodelistToArray = Array.apply(null, nodelist);

//later on ..

nodelistToArray.forEach(...);
nodelistToArray.map(...);
nodelistToArray.slice(...);

//etc...
```

代码解读：apply方法用于将数组参数传递并赋值给这个方法，[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)明确标明了apply方法可以接受类数组对象，确切的说也就是`querySelectorAll`方法的返回值。因为在这函数的上下文中不需要给this赋值，所以传null或0就可以。返回值是真正的DOM元素数组，它们可以调用所有可用的数组方法。

如果你用的是ES2015那你可以用[展开运算符 ...](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_operator)

```javascript
const nodelist = [...document.querySelectorAll('div')]; // returns a real Array

//later on ..

nodelist.forEach(...);
nodelist.map(...);
nodelist.slice(...);

//etc...
```

另请参考：  
[NodeList](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)  


