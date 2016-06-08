---
layout: post
title: "Bug记录：%f和%d的区别"
description: ""
category: cocos2d
tags: [浮点，整型]
---
{% include JB/setup %}


 1. 整形必须用%d输出。
 2. 浮点必须用%f输出。否则输出的数会出现-8798464143.153456，出现错误