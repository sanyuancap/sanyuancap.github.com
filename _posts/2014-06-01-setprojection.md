---
layout: post
title: "setProjection"
description: ""
category: 
tags: []
---
{% include JB/setup %}
一旦两个精灵图片交叠且移动的时候，偶尔会产生闪屏问题：即两个图片相互闪烁，仿佛引擎无法识别哪个是前景哪个是背景

    AppDelegate::applicationDidFinishLaunching()中，添加一行：
    CCDirector::sharedDirector()->setDepthTest(false);//关闭深度测试
    成功解决
    补充：还可以添加这行代码
    CCDirector::sharedDirector()->setProjection(kCCDirectorProjection2D);//使用2D投影(默认3D)
