---
title: js中的交集、并集、差集
date: 2019-04-25 17:21:24
tags: [前端, js]
categories:
- 前端
- js
---

## 前言

> 写在前面，前段时间写项目遇到一个很棘手的问题，求数组内容里全是对象的交集，这个需求说难并不是很难，但是我还是花了一个小时才想明白怎么做

1. 数组里全数字的交集、并集、差集

数组里面的全数字的交集其实很简单，如果你有认真的看下 [这篇文章](http://es6.ruanyifeng.com/#docs/set-map)，其中就有讲到数组中全数字怎么得到交集、并集、差集，如果你没有仔细看，那请看下我怎么实现的。

```
  // 定义两个数组
  let a = new Set([1, 2, 3]);
  let b = new Set([4, 3, 2]);

  // 并集
  let union = new Set([...a, ...b]);
  // Set {1, 2, 3, 4}

  // 交集
  let intersect = new Set([...a].filter(x => b.has(x)));
  // set {2, 3}

  // 差集
  let difference = new Set([...a].filter(x => !b.has(x)));
  // Set {1}
```
但是从打印的地方来看，我们得到的并不是我们想要的数组结构，这里有两种变通的方法可以解决，

- 利用原 Set 结构映射出一个新的结构，然后赋值给原来的 Set 结构

```
  // 方法一
  let set = new Set([1, 2, 3]);
  set = new Set([...set].map(val => val * 2));
  // set的值是2, 4, 6
```

- 利用ES6的 `Array.form` 方法

```
  // 方法二
  let set = new Set([1, 2, 3]);
  set = new Set(Array.from(set, val => val * 2));
  // set的值是2, 4, 6
```

这里个人推荐的是第二种方法

2. 数组里全对象的交集、并集、差集

```
  let arr1 = [
    {
      name: 'xiaoming',
      id: 1
    },
    {
      name: 'xiaohong',
      id: 2
    }
  ]
  let arr2 = [
    {
      name: 'xiaoming',
      id: 1
    },
    {
      name: 'xiaohong',
      id: 2
    },
    {
      name: 'xiaozhang',
      id: 3
    }
  ]

  // 并集
  let arr3 = arr1.concat(arr2)
  let obj = []
  let result = arr3.reduce((cur, next) => {
    obj[next.id]
      ? ''
      : obj[next.id] = true && cur.push(next)
    return cur
  }, [])
  console.log(result)

  // 交集
  let arrId = arr1.map(m => m.id)
  let result = arr2.filter(v => arrId.includes(v.id))
  console.log(result)

  // 差集
  let arr1Id = arr1.map(m => m.id)
  let arr2Id = arr2.map(m => m.id)
  let arr3 = arr1.concat(arr2)
  let result = arr3.filter(v => !(arr1Id.includes(v.id)) || !(arr2Id.includes(v.id)))
  console.log(result)
```

## 友情链接

[ECMAScript 6入门 - 阮一峰](http://es6.ruanyifeng.com/#docs/set-map)
