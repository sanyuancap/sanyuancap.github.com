---
layout: post
title: "Bug记录：动画播放错乱"
description: ""
category: "cocos2d"
tags: [bug]
---
{% include JB/setup %}


描述：
---

用动作编辑器导出的动画，播放顺序错乱，一直播不出爆炸效果，但是代码本身没有报错。

原因：
---

> 编辑器加图的顺序，决定动画播放。

动画播放错乱，例如爆炸效果会出现错帧，是加载图片的顺序导致。打开Animation文件，查看导入顺序，或者在动作编辑器中查看，调整顺序。