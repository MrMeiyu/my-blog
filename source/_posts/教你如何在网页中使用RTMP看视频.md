---
title: 教你如何在网页中使用RTMP看视频
date: 2019-04-29 14:06:01
tags: [前端, JS, Vue, Video.js]
categories: 
- 前端
- Vue
- Video.js
---

## 任何使用RTMP在VideoJS中播放

> 其实 github 上开源了一个基于 `vudeo.js` 封装的一个 `vue` 的组件但是老是报错，所以这篇文章主要还是教你使用 `vudeo.js`

<!-- more -->

1. 下载的依赖

> ⚠️请使用 `yarn` 或者 `npm` 下载

- video.js // yarn add video.js -S
- video.flash // yarn add video.flash -S 切换到flash，因为html5播放不了RTMP格式的流
- 
还有一个 `swf` 的文件，因为我下载引入老是不对，索性我就找了一个在线的 `https://vjs.zencdn.net/swf/5.3/video-js.swf`

这是我的 `package.json` 文件
```js
  {
    "name": "koa2-fe-vue",
    "version": "0.1.0",
    "private": true,
    "scripts": {
      "serve": "vue-cli-service serve",
      "build": "vue-cli-service build",
      "lint": "vue-cli-service lint"
    },
    "dependencies": {
      "axios": "^0.18.0",
      "echarts": "^4.2.1",
      "element-ui": "^2.5.4",
      "js-cookie": "^2.2.0",
      "v-charts": "^1.19.0",
      "video.js": "^7.5.4",
      "videojs-flash": "^2.1.0",
      "vue": "^2.6.6",
      "vue-i18n": "^8.10.0",
      "vue-router": "^3.0.1",
      "vuex": "^3.0.1"
    },
    "devDependencies": {
      "@vue/cli-plugin-babel": "^3.0.5",
      "@vue/cli-plugin-eslint": "^3.4.0",
      "@vue/cli-service": "^3.0.5",
      "@vue/eslint-config-prettier": "^4.0.1",
      "babel-eslint": "^10.0.1",
      "babel-plugin-component": "^1.1.1",
      "babel-plugin-transform-remove-console": "^6.9.4",
      "eslint": "^5.8.0",
      "eslint-plugin-vue": "^5.0.0",
      "file-loader": "^3.0.1",
      "imagemin-jpegtran": "^6.0.0",
      "imagemin-pngquant": "^7.0.0",
      "loadsh": "^0.0.4",
      "lodash-webpack-plugin": "^0.11.5",
      "node-sass": "^4.11.0",
      "sass": "^1.17.3",
      "sass-loader": "^7.1.0",
      "vue-cli-plugin-axios": "^0.0.4",
      "vue-cli-plugin-element": "^1.0.1",
      "vue-template-compiler": "^2.5.21"
    }
  }
```

2. 编写代码

从官网中看了下代码的 🌰 ，所以代码如下：

```js
  <template>
  <div class="video">
    <h2>VideoJS 流媒体</h2>
    <video
      id="myVideo"
      class="video-js vjs-default-skin"
      controls
      preload="auto"
      crossOrigin="anonymous"
      width="400"
    >
      <!-- eslint-disable-next-line -->
      <source
        src="rtmp://184.72.239.149/vod/&mp4:BigBuckBunny_115k.mov"
        type="rtmp/flv"
      />
      <p class="vjs-no-js">
        To view this video please enable JavaScript, and consider upgrading to a
        web browser that
        <a href="https://videojs.com/html5-video-support/" target="_blank">
          supports HTML5 video
        </a>
      </p>
    </video>
  </div>
</template>

<script>
/* VideoJS */
import 'video.js/dist/video-js.css'
import videojs from 'video.js'
import 'videojs-flash'

export default {
  name: 'Video',
  data() {
    return {}
  },
  mounted() {
    this.initVideo()
  },
  destroyed() {
    // 卸载组件的时候清除掉 video 的实例
    this.player1.dispose()
  },
  methods: {
    initVideo() {
      videojs.options.flash.swf = 'https://vjs.zencdn.net/swf/5.3/video-js.swf'
      this.player1 = videojs('myVideo', {
        bigPlayButton: false,
        textTrackDisplay: false,
        posterImage: false,
        errorDisplay: false,
        controlBar: false
      })
      this.player1.play()
    }
  }
}
</script>
```

好，到这里就完成 `video.js` 播放RTMP流的步骤

3. 如果你使用的 React 的话，代码和你这个类似主要是语法变下就行了。

## 源代码

[koa-fe-vue](https://github.com/MrMeiyu/koa2-fe-vue)

如果对你有帮助，麻烦帮忙点下 ✨(star)

## 参考链接

[video官网](https://github.com/videojs/video.js)