---
layout: post
title: "But记录：iterater"
description: ""
category: cocos2dx
tags: [iterater]
---
{% include JB/setup %}

But记录：iterater
==============

Bug描述：
------

遍历数组时出现野指针的现象

原因分析：
-----

array在loop循环中会不停的删除出屏成员，导致数组的count发生了变化。此时遍历时用count计数，会出现野指针的问题。

解决方法：
-----

 
**怎样遍历ccarray才能够读到每一个成员变量？**
回答：遍历时，要从后往前遍历：

        int i = planeBullet->count() - 1;
        i >= 0 ; 
        i--

否则会因为i的值错误而导致去数据错误