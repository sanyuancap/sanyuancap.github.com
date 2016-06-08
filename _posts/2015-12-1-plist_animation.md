---
layout: post
title: "cocos2d-js学习之plist、Animation"
description: ""
category: cocos2d-js
tags: [Animation,plist]
---
{% include JB/setup %}


项目中经常会用到动作，原画甩给你plist文件和图片后，该怎么处理呢？

 - 用bathNode的好处就是初始化只要一张图片，也就是那张大图。然后把所有用到那张大图里面的小图的sprite都加到 CCSpriteBatchNode的child，绘制效率就会提高。
 - 把plist存到spriteFrameCache里
 - 把图片存到textureCache里
 - 新建一个BatchNode，并且添加到场景里

 
		 // explosion batch node
		cc.spriteFrameCache.addSpriteFrames(res.explosion_plist);
		var explosionTexture = cc.textureCache.addImage(res.explosion_png);
		this._explosions = new cc.SpriteBatchNode(explosionTexture);
		this._explosions.setBlendFunc(cc.SRC_ALPHA, cc.ONE);
		this.addChild(this._explosions);


