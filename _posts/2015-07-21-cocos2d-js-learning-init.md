---
layout: post
title: "cocos2d js learning 2init"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##语法
js的语法很随意，比如说```cc.log("cjy" + 123);```，不用%d、%s等的乱入，感觉不错。

##ctor
ctor是Cocos2d-JS中的构造函数，在ctor中必须调用this._super();以确保正确的初始化。

##不同的版本
cocos2d-js-lite.js是轻量级版本，可以让项目很小，但是核心功能却一点不少。

##配置文件与语法
project.json中的jsList是所有的js文件列表，不在其中的文件会找不到。

resource.js中会有图片映射，要写对路径```"res/1.png"```。

设置适配在main.js里```cc.view.setDesignResolutionSize(768, 1024, cc.ResolutionPolicy.SHOW_ALL);```。

##开始设计
设计一个打地鼠类型游戏，9格子初始化并接受点击事件：

            ctor:function () {
                this._super();
                var size = cc.winSize;
                //背景
                var background = cc.Sprite.create(res.startBg);
                background.setAnchorPoint(0.5,0.5);
                background.setPosition(size.width/2,size.height/2);
                this.addChild(background);
                //格子
                this.data = [];
                for(var i = 0; i < 9; i++) {
                    var blocksprite = cc.Sprite.create(res.block0_png);
                    var tempposx = i % 3 - 1;
                    var tempposy = Math.floor(i / 3) - 1;
                    blocksprite.setPosition(size.width / 2 + tempposx * 138, size.height / 2 + tempposy * 138);
                    this.addChild(blocksprite);
                    this.data.push(blocksprite);
                }
                var tempsprite = this.data[4];
                cc.log("cjy:" + tempsprite.getPositionX());
                //添加点击事件
                cc.eventManager.addListener({
                    event:cc.EventListener.TOUCH_ONE_BY_ONE,
                    swallowTouches : false,
                    onTouchBegan:function(t, e){
                        cc.log("touchbegan");
                        return true;
                    },
                    onTouchEnded : function(t, e){
                        var pos = t.getLocation();
                        var cjy = pos.x - background.getPositionX();
                        cc.log(cjy);
                        //cc.log("posx: " + pos.x + " posy: " + pos.y);
                    }
                },this);        
                return true;
            }

##打包
打包时候会用到google closure compiler，`It parses your JavaScript, analyzes it, removes dead code and rewrites and minimizes what's left. It also checks syntax, variable references, and types, and warns about common JavaScript pitfalls.`

webstorm代码补全貌似不是很全，当我想输入```cc.EventListener```时，自动补全成为```cc.eventListener```，因为大小写的原因找不到文件而出错。总之跟xcode+2dx开发有些区别，新的语法和开发工具让我有点不适应。熟能生巧，只能多看代码了。