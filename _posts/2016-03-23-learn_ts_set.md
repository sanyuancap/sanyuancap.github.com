---
layout: post
title: "learn_ts_set"
description: ""
category: 
tags: []
---
{% include JB/setup %}

学习set方法
class Main extends egret.DisplayObjectContainer{

	this.state = Main.STATE_INTRO;
	public set state(s:number)//设置state
    {

    }
    private gameStart(e:egret.Event)
    {
        this.state = Main.STATE_GAME;
    }
}
