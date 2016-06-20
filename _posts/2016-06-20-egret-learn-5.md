---
layout: post
title: "Egret学习之声音和视频"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 

 - 声音播放
 声音播放进度条可以通过mask遮罩实现。

        //sound 播放会返回一个 SoundChannel 对象this_channel，暂停、音量等操作请控制此对象
        this._channel = this._sound.play(this._pauseTime, 1);
        
        //暂停时记录播放位置，再播放时从该时刻继续播放
        this._channel.position//声音结点播放的位置




--------------------------------

 - 视频播放

 Video允许用户在应用中使用视频，但是在大多数移动设备中，视频是强制全屏播放的，所以可以调用play()方法全屏播放，不用绘制在stage中。
 
        this._video = new egret.Video();
        
        //未播放时的截图
        this._video.poster = this._video.fullscreen ? "resource/assets/posterfullscreen.jpg" : "resource/assets/posterinline.jpg";
        
        //加载
        this._video.load("resource/assets/trailer.mp4");
        this.addChild(this._video); 
        
        //全屏
        this._video.fullscreen = !this._video.fullscreen;

