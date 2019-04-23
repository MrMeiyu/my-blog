---
title: JS原型和原型链
date: 2019-04-22 16:16:33
tags: [前端, JS基础]
categories:
- 前端
---

## 原型和原型链

### 知识点

- 构造函数
- 构造函数 - 扩展
- 原型规则和示例
- 原型链
- instanceof

<!-- more -->

## 构造函数

```
function Foo(name, age) {
  this.name = name
  this.age = age
  this.class = 'class-1'
  // return this // 默认有这一行
}
var f = nwe Foo('zhangsan', 20) // f就有Foo的属性
```

## 构造函数 - 扩展

- var a = {} 其实是 var a = new Object() 的语法糖
- var a = [] 其实是 vat a = nwe Array() 的语法糖
- function Foo() {...} 其实是 var Foo = new Function(...)
- 使用 instanceof 判断一个函数是否是一个变量的构造函数

## 原型规则和示例

5条原型规则

- 所有的引用类型（数组、对象、函数），都具有对象特性，即可自由扩展属性（除了"null"）

```
var obj = {}; obj.a = 100;
var arr = []; arr.a = 100;
function fn() {}; fn.a = 100;
```

- 所有的引用类型（数组、对象、函数），都有一个__proto__属性，属性值是一个普通的对象

```
...

console.log(obj.__proto__);
console.log(arr.__proto__);
console.log(fn.__proto__);
```

- 所有的函数，都有一个 prototype 属性，属性值也是一个普通对象

```
...

console.log(fn.prototype)
```

- 所有的引用类型（数组、对象、函数），__proto__属性值指向它的构造函数的 “prototype” 属性值

```
...

console.log(obj.__proto__ === Object.prototype) 
```

- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的__proto__（即它的构造函数的prototype）中寻找

```
  function Foo() {
    this.name = name
  }

  Foo.prototype.alertName = function() {
    alert(this.name)
  }

  var f = new Foo(‘food’)
  f.printName = function() {
    console.log(this.name)
  }

  f.printName()  // food
  f.alertName()  // food
```

## 原型链

```
  ...

  f.toString() // f.__proto__.__proto__中查找 如果最上层没有的就是null
```

## 原型继承

```
  // 封装DOM查询

  function Elem(id) {
    this.elem = document.getElementById(id)
  }

  Elem.prototype.html = function(val) {
    var elem = this.elem
    if (val) {
      elem.innerHTML = val
      return this // 链式操作
    } else {
      return elem.innerHTML
    }
  } 

  Elem.prototype.on = function(type, fn) {
    var elem = this.elem
    elem.addEventListener(type, fn)
    return this
  }

  let div1 = new Elem('div1')
  // console.log(div1.html())
  div1.html('<p>hello m</p>').on('click', function() {
    alert('clicked')
  })
```