---
layout: post
title: "schedule without node parents"
description: ""
category: 
tags: []
---
{% include JB/setup %}
##cocos2dx-js
当前类不是继承自Node，无法进行正常的schedule，例如：this.sheduleupte()。
此时必须调用

        cc.director.getScheduler().scheduleUpdate(this,0,false);
        cc.director.getScheduler().scheduleUpdate(this,0,true);