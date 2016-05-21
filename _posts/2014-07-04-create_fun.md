---
layout: post
title: "关于CREATE_FUNC宏定义"
description: ""
category: cocos2dx
tags: [CREATE_FUNC]
---
{% include JB/setup %}

关于CREATE_FUNC宏定义
================

 - 创建自定义的CCNode类

自定义的CCNode类的对象（如自定义的CCScene，CCSprite）不能用CCNode的create静态方法来创建，因为CCNode的create静态方法是创建一个CCNode类的对象（如CCMyScene调用CCScene的create，创建的是CCScene的对象，而不是CCMyScene的对象）

 - 可用在自定义的CCNode类声明中使用CREATE_FUNC(HelloWorld);

