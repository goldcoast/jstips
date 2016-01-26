---
layout: post

title: Insert item inside an Array
tip-number: 00
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.


categories:
    - en
---

## #0 - Insert item inside an Array
> 12/29/2015

数组中插件元素是件经常遇到的事情。可以使用push来增加元素到数据尾部，使用unshift来操作首个元素，或者使用splice操作中间的元素。

这些都是常用的方法，那是不是意味着就没有更高效的方法呢？来看下面...

使用push()给数据尾部增加元素是非常简单方便的方法，但是有个方法更高效。

```javascript
var arr = [1,2,3,4,5];

arr.push(6);
arr[arr.length] = 6; // 43% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
两种方法都会更改原始数组。不信可以试试介个 [jspref](http://jsperf.com/push-item-inside-an-array)

现在我们试着在数组头部增加元素

```javascript
var arr = [1,2,3,4,5];

arr.unshift(0);
[0].concat(arr); // 98% faster in Chrome 47.0.2526.106 on Mac OS X 10.11.1
```
增加些说明， unshift编辑的是原数组，concat返回的是一个新的数组。[jsperf](http://jsperf.com/unshift-item-inside-an-array)

在数组的中间插入元素使用splice方法做非常简单，并且是一个非常高效的方法。

```javascript
var items = ['one', 'two', 'three', 'four'];
items.splice(items.length / 2, 0, 'hello');
```
我试过在不同的浏览器和系统运行这些测试，结果均类似。希望这些小贴士将会对你有用并能鼓励你执行您自己的测试！
