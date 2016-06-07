---
layout: post
title: "cocos2d-js学习之animation"
description: ""
category: cocos2d-js
tags: [cocos2d-js]
---
{% include JB/setup %}

cocos2d-js学习之animation
========================

## js中的动画

        //爆炸动画
        /*ctor*/
        cc.spriteFrameCache.addSpriteFrames(res.baozhaPlist);
        var animFrames = [];
        for (var i = 0; i < 4; i++) {
            var str = i + ".png";
            var frame = cc.spriteFrameCache.getSpriteFrame(str);
            animFrames.push(frame);
        }
        this.baozhaanimation = cc.Animation.create(animFrames, 0.1);
        this.baozhaSprite = cc.Sprite.create(res.baozhaPng);
        this.baozhaSprite.runAction(cc.hide());
        this.addChild(this.baozhaSprite,999);

        /*touchend*/
        self.baozhaSprite.setPosition(self.blockDatas[tempn].getPosition());
        self.baozhaSprite.runAction(cc.sequence(
            cc.show(),
            cc.animate(self.baozhaanimation),
            cc.hide()
        ));

## js中的骨骼动画

    //拖鞋动画
    ccs.armatureDataManager.addArmatureFileInfo(res.sliperJson);
    this.armature= new ccs.Armature("xie_DZ");
    this.armature.getAnimation().play("Stand");
    this.armature.setPosition(400,400);
    this.addChild(this.armature,999);

## 遇到的bug：
cocos2d-js导入cocostudio资源后，执行报错：`ccs is not defined`.

## 解决方法：
要在project.json模块中导入 cocostudio，
"modules" : ["menus","cocos2d", "extensions", "external"],

## 找到播放的帧的名称

            "animation_data": [
                {
                  "name": "xie_DZ",
            ...
            }
            ]

