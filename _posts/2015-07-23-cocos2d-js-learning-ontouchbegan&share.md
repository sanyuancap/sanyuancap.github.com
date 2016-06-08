---
layout: post
title: "cocos2d-js学习之this和self"
description: ""
category: cocos2d-js
tags: [cocos2d-js]
---
{% include JB/setup %}


遇到的问题：
---------

 无法在ontouchbegan或者ontouchend的函数中调用this指针。

原因与解决办法：
------------

 [（参考地址）](http://blog.csdn.net/lipei1220/article/details/39339557)


this指向的是调用执行环境的那个对象，也就是说this的作用域不同，当函数内部调用this时，不会指向环境外部的变量，所以报错找不到方法！

 - 第一种方法：赋值（用一个变量self保存当前函数执行环境中的this对象）
    var self = this;
    self.blockDatas[0].state = 0;
 - 第二种方法：获取(在函数外部赋值，就可以获取到temp变量了)
    temp = this.temp;

如何添加分享接口
------

    shareCallback:function(){
        h5Share && h5Share.conf({
            desc:this.shareDes,
            title:this.title
        });
        h5Share.share();
    },
    h5Share.init({
        title: "cjy",
        desc: "你一定练过的吧？"
        url: 'http://xxxx/index.html',
        img: 'http://xxxx/favicon.ico'
    });

    index.html添加接口

    <script src="http://xxx/h5.zepto.js"></script>
    <script src="http://xxx/h5.share.js?v=b3e55c4d2986c765151206d50d83b40d"></script>

