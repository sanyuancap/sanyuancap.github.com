---
layout: post
title: "cocos2d-js学习之drawLine"
description: ""
category: cocos2d-js
tags: [drawLine]
---
{% include JB/setup %}

cocos2d-js学习之drawLine
===================

其实js和cocos2dx开发起来大同小异，就连划线函数的名字都差不多。进而联想到调用方法和参数也都差不多。举个栗子：

 - 创建draw对象
 - 调用API进行绘制

		var drawLineArray = [cc.p(tempBottomPosX,-100),cc.p(tempTopPosX,1060)];
		var drawNode = new cc.DrawNode();//创建draw对象，画点，线段，多边形
		this.addChild(drawNode);              //加入Layer层
		drawNode.clear();                      //清除节点缓存
		drawNode.ctor();                       //构造函数

		//曲线
		//参数说明:
		//congfig:点数组
		//tension:张力
		//segments:段落
		//lineWidth:线条宽度
		//color:颜色

		drawNode.drawCardinalSpline(drawLineArray, 0.5, 50, 2, cc.color(255, 255, 255, 255));    

 		//画三次贝塞尔曲线
		drawNode.drawCubicBezier(origin, control1, control2, destination, segments, lineWidth, color) 
		
		//画二次贝塞尔曲线
		drawNode.drawQuadBezier(origin, control, destination, segments, lineWidth, color)         
		///////////函数调用测试
		var drawNode = new cc.DrawNode();//创建draw对象，画点，线段，多边形
		this.addChild(drawNode);              //加入Layer层
		drawNode.clear();                      //清除节点缓存
		drawNode.ctor();                       //构造函数
		drawNode.drawQuadBezier(
		    cc.p(100,100),
		    cc.p(300,800),
		    cc.p(500,100),
		    10, 2, cc.color(255,255,255,255));


    