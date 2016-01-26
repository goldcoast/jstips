---
layout: post

title: use strict and get lazy
tip-number: 07
tip-username: nainslie
tip-username-profile: https://twitter.com/nat5an
tip-tldr: Strict-mode JavaScript makes it easier for the developer to write "secure" JavaScript.

categories:
    - en
---

## #07 - “use strict” 省心的严格模式

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

