# TipList 本项目用于翻译Tips

## #13 测量JS语句块性能的建议

> 13/01/2016 by [@pklinger](https://github.com/pklinger/)

作为ES6的一个新功能，胖箭头(fat arrow)函数或许是个让我们码更少的代码来完成更多工作的 便捷工具。这个名字源于其语法符号 =>。胖当然是相较于瘦箭头 -> 而言 :) 。一些同学可能已经知道这类功能是借签于其它几种不同的编程语言，如Haskell的'lambada表达式'它们分别表示各自的'匿名函数'. 之所以称为匿名函数是因为这些箭头函数并没有函数描述名称。

### 优点在哪里？

- 语法层面：代码更简洁（LOC），不用再没完没了的敲'function'了
- 语义层面：关联当前上下文的this关键字

### 简单的语法示例

下面两段代码功能相同，比较一下，相信你很快就能理解箭头函数的作用。

```javascript
// general syntax for fat arrow functions
param => expression

// 也可以写在括号内
// 使用括号时，在括号内可以写多个参数
(param1 [, param2]) => expression


// using functions
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
  return x * x;
});
console.log(arr)

// using fat arrow
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```

如你所见，箭头函数在这种情况下可节省你敲括号,'function'和'return'等关键字的时间。建议不论什么情况下总是用括号括住参数，因为括号里可以写多个参数，如`(x,y) => x+y`。这种作法可以让我们忽视掉它在不同场景下的写法，尽管上面的代码这样写也可以：`x => x*x`。目前为止我们涉及的都语法层面的东西，它让代码更简洁，更易读。

### Lexically binding this

#todo

译注：  
LOC: line of code



## #13 测量JS语句块性能的建议

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



## #12 ES6函数参数的默认值

> 12/01/2016 by [Avraam Mavridis](https://github.com/AvraamMavridis)

在许多编程语言中，函数的参数在默认情况下是必须传递的，除非开发人员明确定义参数是可选的。在Javascript中每个参数都是可选的，但是我们也可以借助ES6的默认参数值功能让参数传递行为更丰富，却并不干扰函数的主要功能。

```javascript
const _err = function( message ){
  throw new Error( message );
}

const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b

getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
```

代码解读：`_err`方法只做一件事，抛出一个异常。如果第一个参数值没有传递，则使用默认值，`_err`方法将被执行并抛出一个Error。 查看更多示例请点击[MDN(Mozilla's Developer Network)](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters)。

译注：另参考了 [ECMAScript6入门](http://es6.ruanyifeng.com/#docs/function#函数参数的默认值)


## #11 变量声明提升（Hoisting）

> 11/01/2016 by [@squizzleflip](https://twitter.com/squizzleflip)

理解[变量声明提升（Hoisting）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var#var_hoisting)有助于我们更好的管理代码的作用域。要记住的是，变量声明和函数定义会被提升到当前作用域的顶部。变量定义不会被提升，即使你是在同一行上声明和定义的。此外，变量*声明*只是让系统知道有这么个东西存在，而*定义*是给变量赋值。

```javascript
function doTheThing() {
  // 编译出错ReferenceError: notDeclared is not defined
  console.log(notDeclared);

  // Outputs: undefined
  console.log(definedLater);
  var definedLater;

  definedLater = 'I am defined!'
  // Outputs: 'I am defined!'
  console.log(definedLater)

  // Outputs: undefined
  console.log(definedSimulateneously);
  var definedSimulateneously = 'I am defined!'
  // Outputs: 'I am defined!'
  console.log(definedSimulateneously)

  // Outputs: 'I did it!'
  doSomethingElse();

  function doSomethingElse(){
    console.log('I did it!');
  }

  // TypeError: undefined is not a function
  functionVar();

  var functionVar = function(){
    console.log('I did it!');
  }
}
```

为让代码易于阅读，良好的编码习惯是在作用域的顶部声明所有变量，清楚的标识出变量的作用域范围；使用变量前请先定义好；方法可以定义在底部这样阅读时不容易被干扰，可使代码整洁。

译者注，作用域可以参考[JS秘密花园](https://github.com/BonsaiDen/JavaScript-Garden/blob/master/doc/zh/function/scopes.md#变量声明提升hoisting)中的这篇，写的非常好，推荐阅读。


## #10 对象属性检测

> 10/01/2016 by [@loverajoel](https://www.twitter.com/loverajoel)

当你必须检查属性是否存在于一个对象时，你可能正在做这样的事情:

```javascript
var myObject = {
  name: '@tips_js'
};

if (myObject['name']) { ... }
```

这没问题(其实会有问题，当name是一个数字0时返回false。请参考下文的讨论链接)，但你需要知道还有另外两个原生方法也可以完成这个工作：`in`运算符和`Object.hasOwnProperty`方法，所有继承自Object的对象都拥有这两个方法。

来看下他们最大的区别：

```javascript
var myObject = {
  name: '@tips_js'
};

myObject.hasOwnProperty('name'); // true
'name' in myObject; // true

myObject.hasOwnProperty('valueOf'); // false, valueOf 继承自原型链接
'valueOf' in myObject; // true
```

两者最大的不同在于属性层级检测的深度。换言之`hasOwnProperty`方法只在属性为对象直接拥有时才返回true, 而`in`运算符并不区分属性是对象创建还是继承自原型链。

再看一个示例：

```javascript
var myFunc = function() {
  this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';

var user = new myFunc();

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, because age is from the prototype chain
```

有兴趣可以[点这](https://jsbin.com/tecoqa/edit?js,console)(jsbin)直接测试上面代码。

同样也推荐[阅读](https://github.com/loverajoel/jstips/issues/62)这篇关于检测已知对象属性的常见误区的贴子。



## #09 模板字符串

> 09/01/2016 by [@JakeRawr](https://github.com/JakeRawr)

自ES6起，JS可以用模板字符串来代替由引号括起字符串的做法了。

旧的做法：

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

你也可以使用一种被称为[带标签的模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings#Tagged_template_strings)方法来修改输出的字符串内容。

想知道更多关于模板字符串的知识？请看[这里](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2)


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




















