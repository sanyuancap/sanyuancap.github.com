---
layout: post
title: "Bug记录：setTextureRect"
description: ""
category: cocos2dx
tags: [Bug,setTextureRect]
---
{% include JB/setup %}

Bug描述：
------

设置图片大小时，超出了图片尺寸，只显示图片一部分？

解决方法：
-----

在进入场景的时候，设置了图片缩放。设置的是纹理的大小，一定要获取纹理大小，而不是乘以缩放参数：

    setTextureRect(CCRectMake(x,y,width,height)

