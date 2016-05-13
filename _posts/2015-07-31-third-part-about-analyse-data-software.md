---
layout: post
title: "third part about analyse data software"
description: ""
category: 
tags: []
---
{% include JB/setup %}


##[DataEye第三方数据分析解决方案--h5版](http://www.dataeye.com/)

![dataeye](http://www.dataeye.com/images/logo.png "dataeye")

操作方法：

 * 把dcagent.min.js文件下载在src文件夹

 * 在初始化中进行初始化调用
 
         //统计
        DCAgent.init({
            appId: '3D4D756B9B4C7AEAD17C67309AF65E85',
            appVer: 'v1.0.0',
            interval: 15,
            virus: true
        })

 * 分享之前要先调用h5share的init函数
    
        h5Share.init({
            title: h5shareWords[0],
            desc: h5sharedesc,
            url: h5shareurl,
            img: h5shareimg
        });


 * 设置分享文字

        //分享
        h5Share && h5Share.conf({

            title: tempShareWord,
            desc: h5sharedesc
        });

 * 回调函数

        shareCallback:function(){
            h5Share.share();
        },

