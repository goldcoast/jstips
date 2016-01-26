---
layout: post

title: Differences between `undefined` and `null`
tip-number: 05
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: Understanding the differences between `undefined` and `null`.

categories:
    - en
---

## #05 - `undefined` 与 `null` 的不同之处

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

