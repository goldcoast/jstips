---
layout: post

title: Writing a single method for arrays and a single element
tip-number: 06
tip-username: mattfxyz
tip-username-profile: https://twitter.com/mattfxyz
tip-tldr: Rather than writing separate methods to handle an array and a single element parameter, write your functions so they can handle both. This is similar to how some of jQuery's functions work (`css` will modify everything matched by the selector).

categories:
    - en
---

## #06 - 一个方法搞定参数值为单个元素或多元素的情况

> 06/01/2016 [@mattfxyz](https://twitter.com/mattfxyz)

分两个方法独立处理参数是单值或多值的作法显然不如果一个方法能同时搞定两者好。 这有点类似jQuery中的某些方法工作方式 。（如CSS方法就可以同时处理选择器匹配到的元素为单值或多值的情况）

做法很简单，你只需先将传来的参数连入一数组即可，`Array.concat`方法即可搞定一切，它接收数组和单个元素参数。

```javascript
function printUpperCase(words) {
  var elements = [].concat(words);
  for (var i = 0; i < elements.length; i++) {
    console.log(elements[i].toUpperCase());
  }
}
```

`printUpperCase`方法现在即可接收单个元素或多个元素组成的数组做为参数了。


```javascript
printUpperCase("cactus");  
// => CACTUS  
printUpperCase(["cactus", "bear", "potato"]);  
// => CACTUS  
//  BEAR  
//  POTATO  
```

