---
layout: post

title: Node.js - Run a module if it is not `required`
tip-number: 17
tip-username: odsdq
tip-username-profile: https://twitter.com/odsdq
tip-tldr: In node, you can tell your program to do two different things depending on whether the code is run from `require('./something.js')` or `node something.js`. This is useful if you want to interact with one of your modules independently.

categories:
    - en
---


## #17 - Node.js: 运行一个模块如果不是用required方式引入的话

> 17/01/2016 by [@odsdq](https://twitter.com/odsdq)

在Node中，可以让你的JS程序根据运行命令的不同而执行不同的动作，比如你可以使用`require('./something.js')`或`node something.js`。当你需要单独与某个模块做交互时，这个技巧非常有用。

```javascript
if (!module.parent) {
    // ran with `node something.js`
    app.listen(8088, function() {
        console.log('app listening on port 8088');
    })
} else {
    // used with `require('/.something.js')`
    module.exports = app;
}
```

更多信息请查看[modules文档](https://nodejs.org/api/modules.html#modules_module_parent) ([中文API](http://wiki.jikexueyuan.com/project/nodejs/modules.html#e80c310e6ae7ca889532ec40388a497f))

