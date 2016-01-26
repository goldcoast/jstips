---
layout: post

title: Keys in children components are important
tip-number: 02
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: The key is an attribute that you must pass to all components created dynamically from an array. It's a unique and constant id that React uses to identify each component in the DOM and to know whether it's a different component or the same one. Using keys ensures that the child component is preserved and not recreated and prevents weird things from happening.

categories:
    - en
---

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