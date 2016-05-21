---
layout: post
title: "开关控件menuItemToggle"
description: ""
category: cocos2dx
tags: [开关控件]
---
{% include JB/setup %}

开关控件menuItemToggle的使用
==================

在播放音乐、视频的应用中，少不了有开关按钮的使用。以前在做静音的效果时，实现切换图片的方法特别复杂，而且与其它功能同时实现的时候总是出错，后来才知道有CCMenuItemToggle，实现起来非常简单，随手记一下，方便以后查看。



    CCMenuItemImage *btnOn = [CCMenuItemImage itemFromNormalImage:@"soundon.png" selectedImage:@"soundoff.png"]; 
    CCMenuItemImage *btnOff = [CCMenuItemImage itemFromNormalImage:@"soundoff.png" selectedImage:@"soundon.png"]; 
    CCMenuItemToggle *btnSnd = [CCMenuItemToggle itemWithTarget:self selector:@selector(doSndSwtch) items:btnOn, btnOff, nil]; 
    CCMenu *menu = [CCMenu menuWithItems:btnSnd,nil]; 

实现起来很简单，但是当不知道CCMenuItemToggle控件时，确实很让人头疼。