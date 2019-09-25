---
title: 前端小技巧《CSS》
date: 2019-09-25 10:12:03
tags: [前端, CSS]
categories:
- 前端
- css
---

## 总结一些前端的小技巧 《CSS》篇

<!-- more -->

### css 相关

1. 修改 chrome 记住密码后自动填充表单的黄色背景

```css

input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
  background-color: rgb(250, 255, 189); /* #FAFFBD; */
  background-image: none;
  color: rgb(0, 0, 0);
}
```

2. 让页面里的字体变清晰

```css
-webkit-font-smoothing: antialiased;
```

3. 让 overflow:scroll 平滑滚动

```css
-webkit-overflow-scrolling: touch;
```

4. 开启硬件加速

```css
// 目前，像Chrome/Filefox/Safari/IE9+以及最新版本Opera都支持硬件加速，当检测到某个DOM元素应用了某些CSS规则时就会自动开启，从而解决页面闪白，保证动画流畅。
.css {
  -webkit-transform: translate3d(0,0,0);
  -moz-transform: translate3d(0,0,0);
  -ms-transform: translate3d(0,0,0);
  transform: translate3d(0,0,0);
}

```

5. css 禁用鼠标事件

```css
.disabled {
  pointer-events: none;
  cursor: default;
  opacity: 0.6;
}
```

6. css禁止用户选择

```css
body {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
```