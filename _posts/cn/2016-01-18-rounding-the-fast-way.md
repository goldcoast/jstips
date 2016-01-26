---
layout: post

title: Rounding the fast way
tip-number: 18
tip-username: pklinger
tip-username-profile: https://github.com/pklinger
tip-tldr: Today's tip is about performance. Ever came across the double tilde `~~` operator? It is sometimes also called the double NOT bitwise operator. You can use it as a faster substitute for `Math.floor()`. Why is that?

categories:
    - en
---


## #18 - 数字取整最高效的方法

> 18/01/2016 by [@pklinger](https://github.com/pklinger)

今天的小技巧是关于性能方面的。不知你是否遇到过 `~~` 双波浪号运算符？它有时也被称作双重非位运算符。它可以用来替代`Math.floor()`，为什么呢？

单个非位运算符`~`将输入值'inputV'转换为-(inputV+1)。故而两个非位运算符会转为-(-(inputV+1)+1), 这造就了一个非常好的舍入整数位的方法。如果输入的是数字，它便相当于负数运行`Math.ceil()`方法和正数执行`Math.floor()`方法。当运算失败时它返0，这个特性让它在一些情况下可以替代`Math.floor()`方法，因为`Math.floor()`方法在参数为非数字类型时返回NaN。

```javascript
// single ~
console.log(~1337)    // -1338

// numeric input 
console.log(~~47.11)  // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3)      // -> 3

// on failure
console.log(~~[]) // -> 0 
console.log(~~NaN)  // -> 0
console.log(~~null) // -> 0

// greater than 32 bit integer fails
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```

虽说`~~`的性能更好些，但为了代码的可读性还是推荐使用`Math.floor()`方法。

