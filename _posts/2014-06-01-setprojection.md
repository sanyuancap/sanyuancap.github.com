---
layout: post
title: "Bug记录：图片闪烁问题"
description: ""
category: cocos2dx
tags: [Bug, 闪烁]
---
{% include JB/setup %}

Bug记录：图片闪烁问题
============

Bug描述：
------
在项目中遇到，一旦两个精灵图片交叠且移动的时候，偶尔会产生闪屏问题

原因与解决方法：
-----

系统分不清哪个是前景哪个是背景图，这是一个深度问题。所以在`AppDelegate::applicationDidFinishLaunching()`中，关闭深度测试：

    CCDirector::sharedDirector()->setDepthTest(false);//关闭深度测试
    //或者
    CCDirector::sharedDirector()->setProjection(kCCDirectorProjection2D);//使用2D投影(默认3D)
