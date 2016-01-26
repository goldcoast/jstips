---
layout: post

title: Improve Nested Conditionals
tip-number: 03
tip-username: AlbertoFuente 
tip-username-profile: https://github.com/AlbertoFuente
tip-tldr: How can we improve and make a more efficient nested `if` statement in javascript?

categories:
    - en
---

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

