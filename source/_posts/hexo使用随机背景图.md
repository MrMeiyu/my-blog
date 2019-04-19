---
title: hexo-next主题使用随机背景图
date: 2019-04-19 10:10:27
tags: [blog, hexo, next]
type:
- Github
---

### 在next中使用随机的背景图片

> 如果有小伙伴不想自己的页面太素了，可以加上这个背景图，每次都是随机的图片

<!-- more -->

1. [图片来源](https://source.unsplash.com/)

2. 修改背景样式

找到这个 `themes\next\source\css\ _custom\custom.styl` 文件，这是 next 主题故意留下来用户自定义的文件，在文件中添加一下代码

```
  body {
    background: url(https://source.unsplash.com/random/1600x900);
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-position: 50% 50%;
    background-size: cover;
  }
```

以上就是 `hexo-next主题使用随机背景图` 