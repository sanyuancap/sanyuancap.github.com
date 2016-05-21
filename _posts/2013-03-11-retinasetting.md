---
layout: post
title: "retina屏幕设置模式"
description: ""
category: cocos2d
tags: [retina]
---
{% include JB/setup %}

retina屏幕设置模式
========

当**contentScaleFactor**为 1 时采用 point点和pixels点一致的模式，视网膜屏:1 point = 4 pixels

而当**contentScaleFactor**为2时，采用point点和pixels非一致的方式，也就是说，1个point里的4pixels会用自己不同的颜色
