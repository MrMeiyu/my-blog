---
title: HTML5 Web Speech API
date: 2019-07-22 09:28:56
tags: [前端, js, 语音]
categories: 
- 前端
- js
- 语音
---

## 前言

> 之所以写这篇文章主要就是在我司的老项目中有个需求，此需求就是根据页面重量播放语音，比如：56KG,那么页面就会读出来这个数字

<!-- more -->

### Speech Synthesis API

- 因为之前没有过这种需求所以只能去百度下，然后就发现了 [HTMl5 SpeechSynthesis API](https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechSynthesis)

- `HTML5` 中 `Web Speech` 其实有两类的：a. 是 `Speech Recognition` 代表的是语音识别,通俗来说就是语音转文字;b. 是 `Speech Synthesis` 代表的是语音合成,通俗来说就是文字转语音.

### 使用方式

1. 语音识别

``` js
  // 创建实例
  const demo = webkitSpeechRecognition();

  // 开
  demo.start();
  // 关
  demo.stop();

  // 事件机制
  demo.onresult = function(e) {
    console.log(e);
  }
```

- [详细的地址参考](https://developer.mozilla.org/zh-CN/docs/Web/API/%E8%AF%AD%E9%9F%B3%E8%AF%86%E5%88%AB)

---

2. 语音合成

```js
  // 举个栗子
  const demo = new window.SpeechSynthesisUtterance('hello world');
  window.speechSynthesis.speak(demo);

```

- 上面这段代码可以试着放在控制台然后就可以听到声音了
- `SpeechSynthesisUtterance` 和 `speechSynthesis` 为核心的API
- 其他方法和属性请看这里,[走你](https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechSynthesis)

---

以上就是这次所学，因为太简单了，所以没有写过多的代码。还有这个API其实以后会应用的更多，比如适合“盲人”。