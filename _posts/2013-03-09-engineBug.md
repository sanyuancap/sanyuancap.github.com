---
layout: post
title: "升级cocos2d引擎到2.0Bug"
description: ""
category: cocos2d
tags: [升级]
---
{% include JB/setup %}

Bug记录：升级cocos2d引擎到2.0
=================

 - 按照教程中的步骤：下载->覆盖->检查库。
 - 如果遇到找不到头文件的错误，可以在`Build Setting`里面的`Search Patch->Header Search
   Paths`添加路径名称：`libs/kazmath/include`