---
layout: post
title: "曲线ParallaxNode"
description: ""
category: 
tags: []
---
{% include JB/setup %}
cardinalsplineby/cardinalsplineat
：曲线

在游戏的实现过程中，我们有时会需要在某个游戏对象上的运动轨迹上实现间隐效果，这种感觉就好像是类似飞机拉线似的拖尾巴，使我们的游戏在视觉上感觉很好，比如子弹的运动轨迹等等，在kjava时代，这种效果，往往需要美术通过大量的图片来实现，cocos2d-x提供了一种内置的间隐效果拖尾的实现方法CCMotionStreak。

在节点类CCNode中，可以重写draw函数并在其中绘制图形，如tests项目中DrawPrimitivesTest文件夹下DrawPrimitivesTest.cpp文件中的DrawPrimitivesTest类中的draw函数

CParallaxNode(视差节点)
从名字上看得出来，此类继承自CCNode。cocos2D官方是这样说的：
A node that simulates a parallax scroller
The children will be moved faster / slower than the parent according the the parallax ratio.
此类能容纳一些孩子们，这些孩子们一般情况而言都是CCSprite。这些孩子们会按照事先设定好的比例来进行不同速度的移动。最终造成一种视觉上的景深感。
