# TipList 本项目用于翻译Tips

## #03 - Improve Nested Conditionals

> 02/01/2016  by [@AlbertoFuente](https://github.com/AlbertoFuente)

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

使用switch语句或许是一种改进的方法。但是并不推荐使用，尽管switch方法并不繁琐且能让代码变得有序，原因在于它非常难以调试。

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

但如果我们在每个语句执行时都需要检测几个条件时又该怎么做呢？在上边这个例子中，如果我们想做得稍详细和有序些，可用使用条件开关(conditional switch).当swtich接收的参数为true时，它可以允许在每个case语句块中加入判断语句。

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

我们应该尽量避免判断时检测多个条件，尽可能的不使用switch。使用Object的属性是一个更高效的方法。

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




















