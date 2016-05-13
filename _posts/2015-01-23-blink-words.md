---
layout: post
title: "blink words"
description: ""
category: 
tags: []
---
{% include JB/setup %}

#如果制作闪光标题

    var MyLayer = cc.Layer.extend({
        isMouseDown:false,
        helloImg:null,
        helloLabel:null,
        circle:null,
        sprite:null,
        scaleRate:0.8,
     
        init:function () {
     
            this._super();
     
            var size = cc.Director.getInstance().getWinSize();
     
            var clip = this.clipper();
            var clipSize = clip.getContentSize();
            clip.setPosition(cc.p(size.width / 2, size.height / 2));
            var gameTitle = cc.Sprite.create(s_GameTitle);
            gameTitle.setScale(this.scaleRate);
            var spark = cc.Sprite.create(s_Spark);
            clip.addChild(gameTitle, 1);//先添加标题,会完全显示出来,因为跟模板一样大小
            spark.setPosition(-size.width / 2,0);
            clip.addChild(spark,2);//会被裁减
            clip.setScaleY(1.2);
            this.addChild(clip,4);
     
            var moveAction = cc.MoveTo.create(0.6, cc.p(clipSize.width, 0));
            var moveBackAction = cc.MoveTo.create(0.6, cc.p(-clipSize.width, 0));
            var seq = cc.Sequence.create(moveAction, moveBackAction);
            var repeatAction = cc.RepeatForever.create(seq);
            spark.runAction(repeatAction);//进行左右移动的重复动作
     
        },
         clipper : function(){  //创建以标题作为大小的模板,超出标题部分都会被裁掉
            var clipper = cc.ClippingNode.create();
            var gameTitle = cc.Sprite.create(s_GameTitle);
            gameTitle.setScale(this.scaleRate);
            clipper.setStencil(gameTitle);//创建以标题作为大小的模板
            clipper.setAlphaThreshold(0);
            clipper.setContentSize(cc.size(gameTitle.getContentSize().width, gameTitle.getContentSize().height));
            return clipper;
        }
    });
     
    var MyScene = cc.Scene.extend({
        onEnter:function () {
            this._super();
            var layer = new MyLayer();
            this.addChild(layer);
            layer.init();
        }
    });