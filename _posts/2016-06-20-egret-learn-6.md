---
layout: post
title: "Egret学习之资源与动画"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}


 - RES资源加载

 RES.getResByUrl：来加载一个没有在default.res.json中配置的文件。


 RES.createGroup()：通过加载一个group组，来载入一组图片。
 
         RES.createGroup("icons", ["cartoon-egret_00_png", "cartoon-egret_01_png", "cartoon-egret_02_png", "cartoon-egret_03_png"]);
        egret.log("创建后：" + RES.getGroupByName("icons").length);
        
        //加载
        RES.loadGroup("icons");

 还有一种方法是直接在resource.json里新建组，并且重命名即可。
 
 ![jiazaizu][1]

--------------------------------

 - 换装动画

 Slot是骨头上的一个插槽，是显示图片的容器。

 一个Bone上可以有多个Slot，每个Slot中同一时间都会有一张图片用于显示，不同的Slot中的图片可以同时显示。每个Slot中可以包含多张图片，同一个Slot中的不同图片不能同时显示，但是可以在动画进行的过程中切换，用于实现帧动画。

 最典型的就是换装动画。由于换装时人物是不停的运动的，所以如果按照传统的动画替换来做，必须要知道精确的动画坐标和偏移角度，否则会产生错位。这时换装动画就派上用场了。slot可以忽略坐标和夹角，因为slot直接绑定在Bone上。

        var slot:dragonBones.Slot = this._armature.getSlot( slotName );
        var b:egret.Bitmap = new egret.Bitmap();
        b.texture = RES.getRes( textureName );
        b.x = slot.display.x;
        b.y = slot.display.y;
        b.anchorOffsetX = b.width/2;
        b.anchorOffsetY = b.height/2;
        slot.setDisplay( b );


--------------------------------

 - 骨骼动画实时生成

 骨骼动画虽然精巧，但是都是美术妹子细心调好的，如果想要随时运动，恐怕没有那么灵活。但是Egret支持骨骼动画的动态调整，offset的rotation属性可以动态旋转骨骼。
 
        this.head = this.armature.getBone("head");
        this.head.offset.rotation = r;



  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/jiazaizu.png?raw=true