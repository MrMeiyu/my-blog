---
title: 原生JS懒加载
date: 2019-04-26 11:20:03
tags: [前端, JS]
categories:
- 前端
- JS
---

## 原生JS懒加载

1. 先理解图片的加载过程，一般在网页中如果 `<img />` 这个标签中src属性中没得值，那图片就不会加载
，所以我们可以利用这点。
2. 知道了图片加载的方式，我们还需要了解一个知识点就是我们所看到的视口大小，这样才能算出来图片加载多少。
3. 最后就一步整个代码的实现

<!-- more -->

## JavaScript 中获取dom元素高度和宽度的方法

1. 网页可见区域宽： document.body.clientWidth
2. 网页可见区域高： document.body.clientHeight
3. 网页可见区域宽： document.body.offsetWidth (包括边线的宽)
4. 网页可见区域高： document.body.offsetHeight (包括边线的高)
5. 网页正文全文宽： document.body.scrollWidth
6. 网页正文全文高： document.body.scrollHeight
7. 网页被卷去的高： document.body.scrollTop
8. 网页被卷去的左： document.body.scrollLeft

```
// html部分
<img src="" data-src="1.png">
<img src="" data-src="2.png">
<img src="" data-src="3.png">
<img src="" data-src="4.png">

// JS部分
var aImg = document.querySelectorAll('img');
var len = aImg.length;
var n = 0;
window.onscroll = function() {
    var seeHeight = document.documentElement.clientHeight;
    var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
    for (var i = n; i < len; i++) {
        if (aImg[i].offsetTop < seeHeight + scrollTop) {
            if (aImg[i].getAttribute('src') == '') {
                aImg[i].src = aImg[i].getAttribute('data-src');
            }
            n = i + 1;
        }
    }
};
```