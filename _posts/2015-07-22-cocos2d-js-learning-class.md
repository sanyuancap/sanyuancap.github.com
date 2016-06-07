---
layout: post
title: "cocos2d-js学习之class"
description: ""
category: cocos2d-js
tags: [cocos2d-js]
---
{% include JB/setup %}

cocos2d-js学习之class
====================

## 创建新的类
创建一个文件叫做blockSprite.js:

            /**
             + -----状态：
             + 空白 blanck
             + 雪糕 icecream
             + 飞机 plane
             + 拖鞋打击 slipper
            + */
        var blockSprite = cc.Sprite.extend({
                spriteB : null,
                    ctor : function(){
                        this._super();
                        cc.log("this is cjy's world");
                        this.spriteB = cc.Sprite.create(res.planeImg);
                        this.addChild(this.spriteB);
                    },
                    showIcecream : function(){
                       this.spriteB.setTexture(res.planeImg);
                    }
                }
        );

## 调用该类

        //创建block元素
        this.blockDatas = [];
        for(var i = 0 ; i < 9 ; i++){
            var blocksprite = new blockSprite();
            blocksprite.setPosition(111,111);
            this.addChild(blocksprite);
            this.blockDatas.push(blocksprite);
        }


## 遇到的问题
 * 在ctor（）函数中没有调用```this._super();```所以出错。 
 * 控制台的错误提示简直就是0，只能注释代码运行，判断哪个模块出错。
