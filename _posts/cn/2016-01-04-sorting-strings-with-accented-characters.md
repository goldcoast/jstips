---
layout: post

title: Sorting strings with accented characters
tip-number: 04
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Javascript has a native method **sort** that allows sorting arrays. Doing a simple `array.sort()` will treat each array entry as a string and sort it alphabetically. But when you try order an array of non ASCII characters you will obtain a strange result.

categories:
    - en
---

## #04 - Sorting strings with accented characters

> 04/01/2016 [@loverajoel](https://twitter.com/loverajoel)

Javascript中array的原生方法[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)可以对数组进行排序。直接使用array.sort()时数组元素将被视为string类型，并按字母顺序排序。此外您还可以使用[自定义函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters)来排序。

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();  
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

但是当你要对一个非ASCII字符串排序时，比如 ['é', 'a', 'ú', 'c'], 你会得到一个非常奇怪的结果 ['c', 'e', 'á', 'ú']. 原因在于sort仅适用于英文排序。

来看下面这个例子：

```javascript
// Spanish  
['único','árbol', 'cosas', 'fútbol'].sort();  
// ["cosas", "fútbol", "árbol", "único"] // bad order  

// German  
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();  
// ["Wann", "Woche", "wäre", "wöchentlich"] // bad order  
```

幸运的是，有两种由ECMAScript国际化API提供的方法来解决这种问题：[localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) 和 [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator)。

> 这两种方法都可以自定义参数来适配更多的场景。

### Using localeCompare()

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["Wann", "wäre", "Woche", "wöchentlich"]

```

### Using Using Intl.Collator()

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- 两个方法都可以设定本地化语言。
- 据[Firefox文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance)描述Intl.Collator在处理大量string时性能要更上一筹。

附注：据firefox文档这两种方法需要IE11才可以，文档说safarif两种方法都不支持，但经测试safari9.0.1是支持localeCompare的，不支持Intl.Collator()。

