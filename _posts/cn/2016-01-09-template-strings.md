---
layout: post

title: Template Strings
tip-number: 09
tip-username: JakeRawr
tip-username-profile: https://github.com/JakeRawr
tip-tldr: As of ES6, JS now has template strings as an alternative to the classic end quotes strings.

categories:
    - en
---

## #09 - 模板字符串

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


