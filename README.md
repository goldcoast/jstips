# TipList 本项目用于翻译Tips

## #09 模板字符串

> 09/01/2016 by [@JakeRawr](https://github.com/JakeRawr)

自ES6起，JS可以用模板字符串来代替经典的双引号括起来字符串了。

以前的常规做法：

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log('My name is ' + firstName + ' ' + lastName);
// My name is Jake Rawr
```

使用模板字符串：

```javascript
var firstName = 'Jake';
var lastName = 'Rawr';
console.log(`My name is ${firstName} ${lastName}`);
// My name is Jake Rawr
```

在模板字符串中可以写多行内容而不需使用\n，并且在${}内还可以包含一些简单的逻辑。

你也可以使用一种被称为[带标签的模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings)方法来修改输入内容。

你或许想知道更多关于模板字符串的知识，请看[这里](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2)


## #08 DOM节点集合转为Array

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


## #07 “use strict” 省心的严格模式

> 07/01/2016 [@nainslie](https://twitter.com/nat5an)

JavaScript的严格模式可以帮开发人员省心的写出更合理也更安全的代码。

在默认情况下，JavaScript的语法非常的宽松。比如，在第一次使用一个变量时并不需要我们使用"var"来做声明。这看上去是方便了没有经验的开发者，但这同时也是导致一些错误的根源，如变量名拼写错误或超出作用域范围。

程序猿比较喜欢让计算机来完成一些机械无趣的工作，而且让它对工作进行自检以确保工作的正确无误。这也是JS中"use strict"指令帮我们做的，它将代码中的问题转化为Javascript错误。

实现代码的严格模式可以将指令写在JS文件的最上面：

```javascript
// Whole-script strict mode syntax
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

也可以写在方法内：

```javascript
function f()
{
  // Function-level strict mode syntax
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function f2() { return "I'm not strict."; }
```

在JS文件或方法中引入此指令后，Javascript引擎将开启严格模式来运行代码。在较大型的JS项目里使用严格模式可以禁止不少不良的开发习惯。此外，严格模式还改变了以下行为：

- 变量都必须先用`var`声明，然后再使用
- 对只读属性赋值将会报错
- 使用构造函数时必须加上`new`
- "this"不再隐性指向全局对象
- 允许非常有限的情况使用eval()函数
- 禁止变量名使用保留字或新版本中的保留字

严格模式非常适合于新的项目，但在没怎么使用它的旧项目可能很难引入。 另一个问题就是如果你打包时将所有JS打包为一个文件，这可能会导致你所有的代码在严格模式下执行。

严格模式是一行文本而非语句，旧版本的浏览器会将它视为一行普通字符串而忽略。支持严格模式的浏览器有：

- IE10+
- Firefox 4+
- chrome 13+
- safari 5.1+

参考:  
[Firefox MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)（中文）    
[阮一峰博文 Javascript 严格模式详解](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html)  






## #06 一个方法搞定参数值为单个元素或多元素的情况

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


## #05 `undefined` 与 `null` 的不同之处

> 05/01/2016 [@loverajoel](https://twitter.com/loverajoel)

- `undefined` 变量未被声明 或 已声明但尚未赋值
- `null` 变量值，意思是没有值
- Javascript中没赋值的变量默认为`undefined`
- Javascript永远不会设置值为`null`, null是程序员用来声明这个变量还没有值。
- `undefined`在JSON中无效, 但是`null`有效
- `undefined`的typeof值为`undefined`
- `null`的typeof值为`object`
- 两者都是基本元素(primitives,不知道怎么翻译, 差不多就是这个意思)
- 两者都是[falsy对象](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) (`Boolean(undefined) // false`, `Boolean(null) // false`)

- 你可以检测一个变量是不是`undefined`类型

```javascript
typeof variable === "undefined"
```

- 也可以校验变量值是不是`null`

```javascript
variable === null
```

- `==`的结果是true, 但是绝对等于(`===`)为false

```javascript
null == undefined // true

null === undefined // false
```

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



## #03 - Improve Nested Conditionals

> 03/01/2016  by [@AlbertoFuente](https://github.com/AlbertoFuente)

在javascript中，应该怎样改善嵌套的if语句的性能呢？

```javascript
if (color) {
  if (color === 'black') {
    printBlackBackground();
  } else if (color === 'red') {
    printRedBackground();
  } else if (color === 'blue') {
    printBlueBackground();
  } else if (color === 'green') {
    printGreenBackground();
  } else {
    printYellowBackground();
  }
}
```

使用switch语句或许是一种改进的方法。但是并不推荐使用，尽管switch方法并不繁琐且能让代码变得有序，真正原因在于它非常难以调试。

```javascript
switch(color) {
  case 'black':
    printBlackBackground();
    break;
  case 'red':
    printRedBackground();
    break;
  case 'blue':
    printBlueBackground();
    break;
  case 'green':
    printGreenBackground();
    break;
  default:
    printYellowBackground();
}
```

但如果我们在switch的每个语句块执行时都需要检测多个条件时又该怎么做呢？在上边这个例子中，如果想做得稍详细和有序些，可用使用条件开关(conditional switch)的做法。设置swtich的参数为true，此时它可以允许在每个case语句块中加入判断语句。

```javascript
switch(true) {
  case (typeof color === 'string' && color === 'black'):
    printBlackBackground();
    break;
  case (typeof color === 'string' && color === 'red'):
    printRedBackground();
    break;
  case (typeof color === 'string' && color === 'blue'):
    printBlueBackground();
    break;
  case (typeof color === 'string' && color === 'green'):
    printGreenBackground();
    break;
  case (typeof color === 'string' && color === 'yellow'):
    printYellowBackground();
    break;
}
```

尽管如此，我们也应该尽量避免在判断时去检测多个条件，尽可能的不使用switch。下边是一种更高效的做法，方法是使用Object的属性。

```javascript
var colorObj = {
  'black': printBlackBackground,
  'red': printRedBackground,
  'blue': printBlueBackground,
  'green': printGreenBackground,
  'yellow': printYellowBackground
};

if (color && colorObj.hasOwnProperty(color)) {
  colorObj[color]();
}
```

更多详情[点此进入](http://www.nicoespeon.com/en/2015/01/oop-revisited-switch-in-js/)


## #02 - ReactJs - Keys in children components are important

> 02/01/2016  by [@loverajoel](https://twitter.com/loverajoel)


从数组中创建的所有的动态组件都必需设置[Key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children)这个属性。Key在React中是个唯一标识的常量，用来区分DOM中的不同组件。keys将会确保子组件会被保留而不是重新创建，并且能防止些奇怪的异常情况。

> Key 并不是真的关乎性能，更多的是用来标识身份（这反过来将导致更好的性能）。随机分配和不断变化的值都不能做为唯一标识。[Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- 使用对象已有的唯一值。
- 在父组件中定义key值，而非子组件中。

	```javascript
	//bad
	...
	render() {
		<div key={{item.key}}>{{item.name}}</div>
	}
	...

	//good
	<MyComponent key={{item.key}}/>
	```
- [不使用数组索引为key值](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- 使用`random()`方法将无效

	```javascript
	//bad
	<MyComponent key={{Math.random()}}/>
	```
- 可以生成自定义的唯一标识，只要你确保该方法速度够快且能加入到你的对象中。
- 当你的子组件数量很大，或涉及到开销很大的组件时，使用keys可以改善性能。
- 当使用了CSS动效果时你必需为所有子组件设置key属性。[ReactCSSTransitionGroup](http://docs.reactjs-china.com/react/docs/animation.html)


## #1 - AngularJs: `$digest` vs `$apply`

> 01/01/2016

双向绑定功能是AngularJs最被人称赞的特点之一，为了做到这一点AngularJs使用了$digest方法来周期性的检测model和view的变化。为更好的理解框架的在上述方式下的工作情况你需要好好理解这个概念。

在已知的$digest周期里，Angular会检测每一个watcher当有事件触发时。而有些时候你只能手动开启一个新的周期而且必需使用正确的方法，因为这是最影响性能的地方之一。

### `$apply`
此核心方法可以明确的让你开始进入消化(digestion)周期，这意味着所有的监视器watchers都会被检查，整个应用启动‘$digest loop’。$scope.$apply()会调用$rootScope.$digest()。

### `$digest`
在此情景下$digest方法为当前scope和其子scope开始了$digest检测周期.应该当注意到父scope是不会被检测而且不会被影响到。

### 推荐做法
- 仅在非AngularJS上下文环境下，触发DOM事件时才使用`$apply` 或 `$digest`
- 使用带函数参数的$apply方法，其内部有错误处理机制并且允许在digest周期内修改

	```javascript
	$scope.$apply(() => {
		$scope.tip = 'Javascript Tip';
	});
	```

  __个人注：经测试，如果使用带参数的$apply方法,则只会更新参数函数里处理的model,貌似没有开启消化周期。__
- 如果只是要更新当前的scope或它的子scope,使用$digest, 它会防止为整个应用程序开新的digest周期。这种优势不言而喻。
- $apply()是对机器来说比较有压力，当有大量双向绑定时可能会导致性能问题
- 如果你正使用的版本 >AngularJS 1.2.X, 那么使用`$evalAsync`是一种将计算表达式在当前周期或下一期间的核心方法。这可以提高您的应用程序的性能。（这个方法没用过，不太了解）

附上一篇博文翻译 [理解Angular中的$apply()以及$digest()](http://blog.csdn.net/dm_vincent/article/details/38705099) 内有原文链接

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




















