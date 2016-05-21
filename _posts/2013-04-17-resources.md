---
layout: post
title: "Bug记录：资源去重resources"
description: ""
category: cocos2d
tags: [Bug]
---
{% include JB/setup %}

Bug记录：资源去重resources
===================

系统报错：
-----

    pb-05.am pb-06.am pb-07.am plane+bullet重复

解决方法：
-----

资源重复错误一般是因为导入了两个相同名称的资源，可以再`Build Phase`里面`的Copy Bundle Resources`搜索名称查看