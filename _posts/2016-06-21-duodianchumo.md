---
layout: post
title: "Egret学习之多点触摸"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 - 触发事件

 不管是单点触摸，还是多点触摸，Egret的触发事件都是TouchEvent类。其中TOUCH_BEGIN、TOUCH_END和TOUCH_MOVE分别是触摸开始、触摸结束和触摸移动。
 
 
        this.stage.addEventListener(egret.TouchEvent.TOUCH_BEGIN, this.mouseDown, this);
 

 - evt.touchPointID

 evt.touchPointID是分配给触摸点的唯一标示号，例如2990688278。这个标识号是全局唯一，没有重复。如果是多点触摸，每一点的标识号默认是依次递增，例如多点触摸的第二个点就是2990688279，以此类推。
 
 - 缩放和旋转

 touchPoints并不是系统默认的类，而是用户填充触摸点并且进行处理的数组：
 
        private touchPoints:Object = {names:[]};
        //{touchid:touch local,names:[ID1,ID2]};
        
 为了处理多点触摸的缩放和旋转，必须知道两个手指间的触摸点距离变化和角度变化，所以通过touchPoints数组的push方法，添加两点的信息。
 
 
         if(this.touchPoints[evt.touchPointID]==null)
        {
            this.touchPoints[evt.touchPointID] = new egret.Point(evt.stageX,evt.stageY);
            this.touchPoints["names"].push(evt.touchPointID);
        }
 
 在存储了两点信息之后，可以通过计算距离和计算角度，来实时的变换显示对象的位移和缩放。例如处理角度：
 
        var names = this.touchPoints["names"];
        var p1:egret.Point = this.touchPoints[names[names.length-1]];
        var p2:egret.Point = this.touchPoints[names[names.length-2]];
        ang = Math.atan2((p1.y-p2.y),(p1.x-p2.x)) / this.c;

 处理距离：

        var names = this.touchPoints["names"];
        _distance = egret.Point.distance( this.touchPoints[names[names.length-1]],
        this.touchPoints[names[names.length-2]]);