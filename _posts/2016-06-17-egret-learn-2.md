---
layout: post
title: "Egret学习之高级图像"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 - 圆弧

 Egert提供了很多绘图api，比如绘制矩形、圆形、多边形等。
 
 如果要绘制一段圆弧路径，还分为顺时针和逆时针两种方向。如果加上遮罩的特效，可以实现很多动态效果。例如：圆弧路径的圆心在 (x, y) 位置，半径为 r ，根据anticlockwise （默认为顺时针）指定的方向从 startAngle 开始绘制，到 endAngle 结束。

        shape.graphics.drawArc(0, 0, 200, 0, angle * Math.PI / 180, i == -1);

![圆弧][1]

--------------------------------

 - 自动脏矩形

>  脏矩形是2D图形性能优化一个重要的概念。Egret2.5开始脏矩形完全可以由引擎自动计算，即"自动脏矩形"。 简单说脏矩形，就是画面**刷新**时，产生变化而需要**重绘**的舞台局部**区域**。

使用脏矩形将大大减少无用的渲染工作量，降低额外性能消耗。对移动设备来说，会节省大量电能以及降低设备运行温度。大多数情况，开发者不需要关系脏矩形如何工作。自动脏矩形是Egret引擎的一项被动技能，引擎运行时会每帧自动释放该技能来提升你的程序性能！

![脏矩形][2]

脏矩形的红框可以在`index.html`中搜索`data-show-paint-rect`属性，设置其值为`"true"`即可，发布给用户前，确保该值重置为`"false"`。


--------------------------------

 - 位图缓存

 位图缓存是一项在特定情况下可以**提升性能**的利器。其原理是将一组在相当长时间内显示状态及相对位置保持恒定的显示对象建立一个**快照**，在后续显示中用这个快照代替这一组显示内容。`通常用于图形或文字。`
 
 ![图片缓存][3]
 
        var cont:Sprite = new Sprite();
        cont.graphics.beginFill( iFillColor );
        cont.graphics.drawRect( xRdm - wRect/2, yRdm - hRect/2, wRect, hRect );
        cont.graphics.endFill();
        cont.cacheAsBitmap = true;//打开缓存

--------------------------------

 - 动态截屏

可以将指定显示对象(当然包括显示容器)中特定区域进行动态截取，保存为纹理格式，因此可以立即以位图的方式呈现出来！


 

> RenderTexture是动态纹理类，可以实现讲一个显示对象及其子对象绘制成纹理。

 
 
    var rt:egret.RenderTexture = new egret.RenderTexture;
    rt.drawToTexture( this._contMotion, this._rectClip );//将指定显示对象绘制成一个纹理
    this._bmpSnap.texture = rt;



  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/yuanhu.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/zangjuxing.png?raw=true
  [3]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/tupianhuancun.png?raw=true