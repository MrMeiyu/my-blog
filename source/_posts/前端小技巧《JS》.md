---
title: 前端小技巧《JS》
date: 2019-09-25 10:12:03
tags: [前端, JS]
categories:
- 前端
- js
---

## 总结一些前端的小技巧 《JS》篇

<!-- more -->

1. 给数字每三位加上逗号

```js
function commafy(num){
  return num && num
    .toString()
    .replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
      return $2 + ',';
    });
}
```

2. js求平面两点之间的距离

```js
// 数据可以以数组方式存储，也可以是对象方式
let a = {x:'6', y:10},
    b = {x: 8, y: 20};
  function distant(a,b){
    let dx = Number(a.x) - Number(b.x)
    let dy = Number(a.y) - Number(b.y)
    return Math.pow(dx*dx + dy*dy, .5)
  }
```