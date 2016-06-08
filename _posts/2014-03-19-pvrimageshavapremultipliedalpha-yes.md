---
layout: post
title: "Bug记录：压缩后的图片无法读取？"
description: ""
category: cocos2dx
tags: [压缩,Bug]
---
{% include JB/setup %}


Bug描述：
---

TP工具压图以后，运行项目却读不出图了？

原因与解决：
------

    [CCTexture2D PVRImagesHavePremultipliedAlpha:YES]; 

如果在项目中添加了这句话，但是，忘记在TP工具中将倒数第二项打钩，那么你就悲剧了 ；
打包成pvr格式的不要忘记在TP打包前将TP的倒数第二个选项打钩哦～；

    



