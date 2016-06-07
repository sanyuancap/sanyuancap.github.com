---
layout: post
title: "cocos2d-js学习之scheduleUpdate"
description: ""
category: cocos2d-js
tags: [scheduleUpdate]
---
{% include JB/setup %}

cocos2d-js学习之scheduleUpdate
================

 - Bug描述：

 在初始化成功后调用scheduleUpdate()，竟然没有成功。

 - 解释：

 仔细看了下，当前类不是继承自Node，无法进行正常的schedule，例如：this.sheduleupte()等。所以此时必须调用

        cc.director.getScheduler().scheduleUpdate(this,0,false);
        cc.director.getScheduler().scheduleUpdate(this,0,true);