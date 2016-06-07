---
layout: post
title: "cocos2dx学习之优化"
description: ""
category: cocos2dx
tags: [cocos2dx]
---
{% include JB/setup %}

cocos2dx学习之优化
==============


## 引擎优化
cocos2dx-2.0用openGL ES 2.0图形库

## 渲染优化
 * CCSpriteBatchNode：一次加载所有纹理，一次渲染 

## 资源缓存优化
 * 进入场景之前加载，退出场景后remove，用进度条或者图像文字的提示方式，减少客观等待时间
 * CCSpriteFrameCache：帧缓存
 * CCTextureCache：图片缓存

## 内存优化
 * 内存池方案：把新资源加载到内存池，多次使用，不用多次释放和重新加载
 * autorelease：引用计数
 * 工具Instrument可以检查内存泄露

## 纹理优化
 * 色深优化：ARGB4444+图像抖动
 * 纹理尺寸限制：iPhone4（4096*4096）
 * 骨骼动画
 * 纹理压缩格式：PVR格式，iOS使用PowerVR显示芯片，可以直接读取，并且压缩ccz。普通的png图可以通过压缩软件比如tinypng，从24位压缩为8位，同时视觉上不会有差异

## 文件读取优化
 * xml
 * 尽量减少文件读取


[参考资料](http://blog.csdn.net/xzongyuan/article/details/9175645)














