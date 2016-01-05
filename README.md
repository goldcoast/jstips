# TipList 本项目用于翻译Tips

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




















