---
layout: post
title: "onTouchBegan"
description: ""
category: 
tags: []
---
{% include JB/setup %}


*遇到的问题：无法在ontouchbegan或者ontouchend的函数中调用别的this.函数，或者this.数组，只能访问变量。还在纠结这个问题ing，找到答案以后，会更新答案的。
*原因与解决办法：[（参考地址）](http://blog.csdn.net/lipei1220/article/details/39339557)
this指向的是调用执行环境的那个对象，也就是说this的作用域不同，当函数内部调用this时，不会指向环境外部的变量，所以报错找不到方法！

            //第一种方法：赋值（用一个变量self保存当前函数执行环境中的this对象）
            var self = this;
            self.blockDatas[0].state = 0;
            //第二种方法：获取(在函数外部赋值，就可以获取到temp变量了)
            temp = this.temp;

            //添加点击事件
            cc.eventManager.addListener({
                event:cc.EventListener.TOUCH_ONE_BY_ONE,
                swallowTouches : false,
                onTouchBegan:function(t, e){
                    return true;
                },
                onTouchEnded : function(t, e){
                    var pos = t.getLocation();
                    var cjyx = pos.x - blockbg.getPositionX();
                    var cjyy = pos.y - blockbg.getPositionY();
                    var posx,posy;
                    posx = Math.floor(cjyx / 100);
                    //cc.log(posx);
                    /**分区
                    *2  6  7  8
                    *1  3  4  5
                    *0  0  1  2
                    *   0  1  2
                    */
                    if(posx >= 1 && posx <= 2){
                        posx = 2;
                    }else if(posx <= -2 && posx >= -3){
                        posx = 0;
                    }else if(posx <= 0 && posx >= -1){
                        posx = 1;
                    }
                    posy = Math.floor(cjyy / 100);
                    if(posy >= 1 && posy <= 2){
                        posy = 2;
                    }else if(posy <= -2 && posy >= -3){
                        posy = 0;
                    }else if(posy <= 0 && posy >= -1){
                        posy = 1;
                    }
                    //cc.log(posx);
                    //cc.log(posy);
                    //cc.log("---------");
                    if(posx >= 0 && posy >= 0 && posx <= 2 && posy <= 2){
                        var tempn= posx + posy * 3;//得到0-9的id
                        //cc.log(tempn);
                        if(blockDatas[tempn].state == 1){
                            blockDatas[tempn].showBlanck();//让雪糕筒消失
                        }
                    }
                }
            },this);

*分享接口

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

*index.html添加接口

    <script src="http://xxx/h5.zepto.js"></script>
    <script src="http://xxx/h5.share.js?v=b3e55c4d2986c765151206d50d83b40d"></script>

