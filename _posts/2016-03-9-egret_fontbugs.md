---
layout: post
title: "egret_fontbugs"
description: ""
category: 
tags: []
---
{% include JB/setup %}

egretEngine3.0.3
button字体bug：
在chrome浏览器点击button，button上的字体会变小

解决：
删除button皮肤设置的字体font，里面一共有两个，删除一个

===============

解决了一个超级头疼郁闷的bug：
var b = a;
修改b以后，a跟着修改了；

解决：
传递参数或者内容，必须新建和赋值，否则使用的依旧是原参数的引用，导致原来的数组错乱。
！！！！！！！！！！！