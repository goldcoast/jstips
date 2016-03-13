---
layout: post

title: Filtering and Sorting a List of Strings 字符串数组的过滤与排序
tip-number: 26
tip-username: davegomez
tip-username-profile: https://github.com/davegomez
tip-tldr: 假如你有一个非常大的姓名数组，需要你去除掉里面重复的数据，并让结果按照字母排序。

categories:
    - en
---

假如你有一个非常大的姓名数组，需要你去除掉里面重复的数据，并让结果按照字母排序。

在示例中，我们计划使用**JavaScript保留关键字**列表来测试，这些关键字是从多个不同版本的JS中选出，不过正如你注意到的，其中有许多重复的关键字，而且没有按字母排序。因此它是一个完美的测试数组([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)) 。

```js
var keywords = ['do', 'if', 'in', 'for', 'new', 'try', 'var', 'case', 'else', 'enum', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'delete', 'export', 'import', 'return', 'switch', 'typeof', 'default', 'extends', 'finally', 'continue', 'debugger', 'function', 'do', 'if', 'in', 'for', 'int', 'new', 'try', 'var', 'byte', 'case', 'char', 'else', 'enum', 'goto', 'long', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'final', 'float', 'short', 'super', 'throw', 'while', 'delete', 'double', 'export', 'import', 'native', 'public', 'return', 'static', 'switch', 'throws', 'typeof', 'boolean', 'default', 'extends', 'finally', 'package', 'private', 'abstract', 'continue', 'debugger', 'function', 'volatile', 'interface', 'protected', 'transient', 'implements', 'instanceof', 'synchronized', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'await', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof'];
```

Since we don't want to change our original list, we are going to use a high order function named [`filter`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), which will return a new filter array based in a predicate (*function*) we pass to it. The predicate will compare the index of the current keyword in the original list with its `index` in the new list and will push it to the new array only if the indexes match.
由于并不想改变原数组，我们打算使用一个高阶函数[`filter`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)来完成这个任务，它会基于你传递的过滤方法返回一个新数组。过滤方法中返回值为true或等于true的值会被加入到新数组中返回。


Finally we are going to sort the filtered list using the [`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) function which takes a comparison function as the only argument, returning a alphabetically sorted list.
最后我们对过滤后的数据进行排序，使用[`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)方法可以完成此任务，它只带一个比较函数做为参数，返回按字母排序后的数组。


```js
var filteredAndSortedKeywords = keywords
  .filter(function (keyword, index) {
      return keywords.lastIndexOf(keyword) === index;
    })
  .sort(function (a, b) {
      return a < b ? -1 : 1;
    });
```

The **ES6** (ECMAScript 2015) version using [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) looks a little simpler:
**ES6** (ECMAScript 2015)使用箭头函数看起来会更简洁些：

```js
const filteredAndSortedKeywords = keywords
  .filter((keyword, index) => keywords.lastIndexOf(keyword) === index)
  .sort((a, b) => a < b ? -1 : 1);
```

下边是过滤并排序后的JavaScript保留关键字的最终结果：
And this is the final filtered and sorted list of JavaScript reserved keywords:

```js
console.log(filteredAndSortedKeywords);

// ['abstract', 'arguments', 'await', 'boolean', 'break', 'byte', 'case', 'catch', 'char', 'class', 'const', 'continue', 'debugger', 'default', 'delete', 'do', 'double', 'else', 'enum', 'eval', 'export', 'extends', 'false', 'final', 'finally', 'float', 'for', 'function', 'goto', 'if', 'implements', 'import', 'in', 'instanceof', 'int', 'interface', 'let', 'long', 'native', 'new', 'null', 'package', 'private', 'protected', 'public', 'return', 'short', 'static', 'super', 'switch', 'synchronized', 'this', 'throw', 'throws', 'transient', 'true', 'try', 'typeof', 'var', 'void', 'volatile', 'while', 'with', 'yield']
```

*Thanks to [@nikshulipa](https://github.com/nikshulipa), [@kirilloid](https://twitter.com/kirilloid), [@lesterzone](https://twitter.com/lesterzone), [@tracker1](https://twitter.com/tracker1), [@manuel_del_pozo](https://twitter.com/manuel_del_pozo) for all the comments and suggestions!*


