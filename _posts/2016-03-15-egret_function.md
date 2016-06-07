---
layout: post
title: "Egret学习之函数"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

Egret学习之函数
=============


 - complete: () => void

 其实就是把函数做为参数，可以用在函数回调的时候：

		module common {
		    export class Loading {
				public constructor(groupName: string, complete: () => void, container:egret.DisplayObjectContainer) {}
		}


 - 学习set方法

		class Main extends egret.DisplayObjectContainer{
			this.state = Main.STATE_INTRO;
			public set state(s:number)//设置state
		    {
		    	...
		    }
		    
		}
