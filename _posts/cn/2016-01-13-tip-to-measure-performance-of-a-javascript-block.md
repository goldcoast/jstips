---
layout: post

title: Tip to measure performance of a javascript block
tip-number: 13
tip-username: manmadareddy
tip-username-profile: https://twitter.com/manmadareddy
tip-tldr: For quickly measuring performance of a javascript block, we can use the console functions like `console.time(label)` and `console.timeEnd(label)`

categories:
    - en
---


## #13 - 测量JS语句块性能的建议

> 13/01/2016 by [@manmadareddy](https://twitter.com/manmadareddy)

为快速即时判断javascript语句块性能，我们可以使用控制台的方法如`console.time(label)`和`console.timeEnd(label)`

```javascript
console.time('Array initialize');
var arr = new Array(100),
    len = arr.length,
    i;

for (i = 0; i < len; i++){
  arr[i] = new Object();
};

console.timeEnd("Array initialize"); // Outputs: Array initialize:0.711ms
```

更多介绍: [Console object](https://github.com/DeveloperToolsWG/console-object),[Javascript benchmarking](https://mathiasbynens.be/notes/javascript-benchmarking) 

Demo: [jsfiddle](https://jsfiddle.net/meottb62/) - [codepen](http://codepen.io/anon/pen/JGJPoa)(outputs in browser console)


