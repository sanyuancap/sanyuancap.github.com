---
layout: post
title: "cocos2dx学习之retain、release"
description: ""
category: cocos2dx
tags: [retain,release]
---
{% include JB/setup %}

学习retain and release
====================

[参考资料][1]
CCNode是所有节点类的父类，他内部使用了一个CCArray对象管理他的所有子节点，当对象被添加为子节点时，实际上是被添加到CCArray对象中，同时会调用这个对象的retain方法。同理，从CCArray中移除时，也会调用release方法。

 - 你初始化(alloc/init)的对象，需要释放(release)它。
例如：

        NSMutableArray aArray = [[NSArray alloc] init];
        [aArray release];

 - retain或copy的，需要释放它。
例如：
 
        [aArray retain]
        [aArray release];

 - 被传递(assign)的对象，你需要斟酌的retain和release。例如：

        obj2 = [[obj1 someMethod] autorelease];


  [1]: http://blog.csdn.net/jasonwu1990/article/details/7454818