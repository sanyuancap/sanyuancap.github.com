---
layout: post
title: "cocos2d-creator学习之切图"
description: ""
category: cocos2d-js
tags: [cocos2d-js]
---
{% include JB/setup %}

 - cocoscreator图集的参数解释：
将指定的一系列碎图打包成一张大图，具体作用和 Texture Packer 的功能很相近。

![autoatlas][1]

 - 优点

        1.合成图集时会去除每张图片周围的空白区域，加上可以在整体上实施各种优化算法，合成图集后可以大大减少游戏包体和内存占用
        2.多个 Sprite 如果渲染的是来自同一张图集的图片时，这些 Sprite 可以使用同一个渲染批次来处理，大大减少 CPU 的运算时间，提高运行效率

 - tinyPNG的使用

TinyPNG在一个在线图片压缩工具，这个压缩率很高，有50%-70%，而且几乎不损失画质。 由于是在线，所以在网页上上传下载就显得有些繁琐，不过最近github上出现一个TinyPNG的mac客户端，简直就是神作。

[TinyPNG4Mac.app][2]

另外要提的是，使用 TinyPNG4Mac 需要 TinyPNG 的 API，你可以在后者官网免费申请到。

[具体用法][3]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-autoatlas.png?raw=true
  [2]: https://github.com/kyleduo/TinyPNG4Mac
  [3]: https://sspai.com/post/41979