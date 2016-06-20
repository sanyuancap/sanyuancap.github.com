---
layout: post
title: "Egret学习之基本显示对象"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 - 遮罩的概念：

 指定遮罩后，只能看到遮罩形状下的被遮物体，被遮物体其余的部位都看不到。例如下图：

![遮罩1][1]

遮罩是this._bird，也就是图中的小鸟：

    this._bird = new egret.Bitmap( evt.currentTarget.data );

被遮物体是this._shpBeMask，绘制的图形：

    this._shpBeMask = new egret.Shape;
    this._shpBeMask.graphics.lineStyle( 0x000000 )
    this._shpBeMask.graphics.beginFill( this.getRdmClr() );
    this._shpBeMask.graphics.drawEllipse( 0, 0, 200, 300 );
    this._shpBeMask.graphics.endFill();

 - 指定遮罩：

    this._shpBeMask.mask = this._bird;

指定遮罩后，点击物体，可以看到，只有小鸟形状下的图形能够被看到，其余的都被遮蔽起来。

![遮罩2][2]

 - 删除遮罩：

    this._shpBeMask.mask = null;

--------------------------------

 - 碰撞检测

 Egret的碰撞检测分为两种模式，一种是对显示对象所在的**矩形包围盒检测**，另一种是其**透明度不为零的区域检测**。
 
        var bResult:boolean = this._bird.hitTestPoint( stageX, stageY, flag );
        //flag是true的时候，开启透明度不为零的区域检测，这时候消耗的性能要远大于矩形包围盒。


 - 点击穿透

 点击穿透功能是与碰撞检测的形状检测开关接近的概念。这两个功能，都是针对位图的完全透明像素区域来说的。打开点击穿透开关的位图，触摸其透明区域将不会再派发事件。
 

        this._bigbird.pixelHitTest = false;//是否开启精确碰撞检测

 
 - 不同点

 点击穿透需要通过**触摸事件**来检测，而碰撞检测不需要任何触摸，是直接用一个点对一个显示对象进行检测。
 

>  总结一句话就是点击穿透需要用户交互，去点击才能触发。碰撞检测是一种被动技能，只要是场景中被检测物体，都会自动的碰撞检测。

    


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/zhezhao1.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/zhezhao2.png?raw=true

