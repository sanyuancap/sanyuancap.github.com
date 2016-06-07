---
layout: post
title: "Egret学习之字体"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

Egret学习之字体
=============

 - But描述：egretEngine3.0.3的button字体存在bug——在chrome浏览器点击button，button上的字体会变小

 解决办法：删除button皮肤设置的字体font，里面一共有两个，删除一个


 - 赋值

		var b = a;

 修改b以后，a跟着修改了；

 解决办法：
传递参数或者内容，必须新建和赋值，否则使用的依旧是原参数的引用，导致原来的数组错乱。