---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript modules and build steps are getting more numerous and complicated, but what about boilerplate in new frameworks?

categories:
    - en
---

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
