---
layout: post
title: "Bug记录：continue and break"
description: ""
category: cocos2dx
tags: [Bug]
---
{% include JB/setup %}


bug描述：
------

程序执行不到最后一行就跳出了。

原因分析：
---
这是一个for循环方法，循环查找某个变量，如果找不到则继续寻找。这是需要continue来进入下一个循环。但是我错误的写成了break，导致程序执行不到最后一行。

注意break和continue的区别

 - return：如果直接return，会跳出函数。
 - break：如果break，跳出这个函数的循环，并且循环后面的功能都不会执行
 - continue：系统会跳过这一次的循环，进入下一次循环