---
layout: post

title: Shuffle an Array
tip-number: 21
tip-username: 0xmtn
tip-username-profile: https://github.com/0xmtn/
tip-tldr: Fisher-Yates Shuffling it's an algorithm to shuffle an array.

categories:
    - en
---

## #21 数组随机重新排序(洗牌)

> 21/01/2016 by [@0xmtn](https://github.com/0xmtn/)

下面这段代码使用了费希尔-耶茨洗牌(Fisher-Yates Shuffling)算法对数组中元素进行随机排序。

```javascript
function shuffle(arr) {
    var i,
        j,
        temp;
    for (i = arr.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    return arr;    
};
```

演示示例：

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
var b = shuffle(a);
console.log(b);
// [2, 7, 8, 6, 5, 3, 1, 4]
```

**笔记**  
Math.random()返回(0-1)的浮点值伪随机数
