---
layout: post
title: "cocos2d-js学习之图片特效之闪光效果"
description: ""
category: cocos2d-js
tags: [cocos2d-js,ClippingNode]
---
{% include JB/setup %}

如果制作闪光效果
========

![clip][1]

> ClippingNode(裁剪节点)可以用来对节点进行裁剪，可以根据一个模板切割图片的节点，生成任何形状的节点显示。

 - 所谓模板，就是一个形状，透过该形状可看到底板上的图层，如果底板上没有任何内容，则直接看到Layer上的内容，而底板上的东西又不会妨碍Layer上的东西，即模板在底板之外的空间对于Layer来说是透明的。

![特效][2]

 - 对于该图的特效来说，以标题作为模板,光效经过ClippingNode(裁剪节点),裁剪掉多余的部分，就可以简单实现。具体代码如下：
     
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
                //先添加标题,会完全显示出来,因为跟模板一样大小
                clip.addChild(gameTitle, 1);
                spark.setPosition(-size.width / 2,0);
                //会被裁减
                clip.addChild(spark,2);
                clip.setScaleY(1.2);
                this.addChild(clip,4);
                var moveAction = cc.MoveTo.create(0.6, cc.p(clipSize.width, 0));
                var moveBackAction = cc.MoveTo.create(0.6, cc.p(-clipSize.width, 0));
                var seq = cc.Sequence.create(moveAction, moveBackAction);
                var repeatAction = cc.RepeatForever.create(seq);
                //进行左右移动的重复动作
                spark.runAction(repeatAction);
            },
            //创建以标题作为大小的模板,超出标题部分都会被裁掉
             clipper : function(){  
                var clipper = cc.ClippingNode.create();
                var gameTitle = cc.Sprite.create(s_GameTitle);
                gameTitle.setScale(this.scaleRate);
                //创建以标题作为大小的模板
                clipper.setStencil(gameTitle);
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
    
    
 - 参考文章
[狂斩三国特效][3]
[裁剪节点][4]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/clipping/1.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/clipping/2.gif?raw=true
  [3]: http://blog.csdn.net/teng_ontheway/article/details/45651343
  [4]: http://www.mamicode.com/info-detail-247772.html