---
layout: post
title: "retain and release"
description: ""
category: 
tags: []
---
{% include JB/setup %}

CCNode是所有节点类的父类，他内部使用了一个CCArray对象管理他的所有子节点，当对象被添加为子节点时，实际上是被添加到CCArray对象中，同时会调用这个对象的retain方法。同理，从CCArray中移除时，也会调用release方法。
