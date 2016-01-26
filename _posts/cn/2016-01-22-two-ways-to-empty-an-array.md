---
layout: post

title: 清空数组的两种方法
tip-number: 22
tip-username: microlv
tip-username-profile: https://github.com/microlv
tip-tldr: Javascript清空数组的方法有很多，但这是效率最好的。

categories:
    - en
---

## #22 清空数组的两种方法

> 22/01/2016 by [@microlv](https://github.com/microlv)


假设你定义了一个数组并且想清空它所有成员，通常情况下，你可能会这样做：

```javascript
// define Array
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list = [];
}
empty();
```

但是，还有一种更高效的方法，代码如下：

```javascript
var list = [1, 2, 3, 4];
function empty() {
    //empty your array
    list.length = 0;
}
empty();
```

* `list = []` 分配了一个新的数组引用给变量，并且不影响现有的其它变量。然而这意味着之前引用的数组还在内存中，它可能会导致内存泄露。

* `list.length=0`将清空数组内所有东西，并直接作用在之前的引用上。

换言之，如果你有两个引用在同一个数组时 (`a = [1,2,3]; a2 = a;`), 然后使用`list.length = 0`清空了数组，这两个数组此时都会指向同一个空的数组。(因此，当你不想a2也置为空数组时不要这样做)

思考下，下面代码会输出什么值：

```js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);

// [] [] [1, 2, 3] []
```

Stackoverflow more detail:
[difference-between-array-length-0-and-array](http://stackoverflow.com/questions/4804235/difference-between-array-length-0-and-array)


