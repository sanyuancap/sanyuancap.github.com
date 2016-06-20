---
layout: post
title: "Egret学习之时间与调试"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 - 动态帧频

 初始化游戏时，可以设定一个固定的帧频，然后在游戏开始后，根据手机性能需求，动态的增加或者减少帧频，这种适配效果能够增加游戏的运行效率，减少卡顿。

        this.stage.frameRate = Number(this.textInput.text);

--------------------------------

 - 延迟调用

        setTimeout（）;//延时回调函数
        
  如果在延时回调的时候，在回调函数中显示字体或者图片，会有很精彩的效果，例如打字机的效果，随着键盘打字，字体出现在显示器上：
        
        private typerEffect(obj,content:string = "",interval:number = 200,backFun:Function = null):void{
                var strArr:Array<any> = content.split("");//把字符串切割成数组
                var len:number = strArr.length;
                for (var i = 0; i < len; i++){
                    egret.setTimeout(function () {              
                        obj.appendText(strArr[Number(this)]);//给字符串增加字符
                        if ((Number(this) >= len - 1) && (backFun != null)) {
                            backFun();
                        }
                    }, i, interval*i);              
                }
            }

--------------------------------

 - 强制刷新

 修改了显示列表（如添加、减少、缩放、旋转等）后，如果调用强制更新，会忽略帧频，在绘制完后立即重绘屏幕，这种做法会让动画更加流畅，操作更加友好，但是会牺牲效率。

        event.updateAfterEvent();

--------------------------------

 - FPS监视器

开启帧频信息面板，Egret会在舞台的左上角显示FPS和其他性能指标。

![监视器][1]

在`index`文件内找到`data-show-fps`字段，设置为`true`即可显示帧频信息，反之关闭。各项信息的含义是：

 1. FPS：帧频
 2. Draw：每帧draw方法调用的平均次数，脏区域占舞台的百分比
 3. Cost：Ticker和EnterFrame阶段显示的耗时,每帧舞台所有事件处理和矩阵运算耗时，绘制显示对象耗时（单位是ms）

--------------------------------

 - Log面板

![调试][2]
 
Log可以从控制台看到，当然也可以直接在游戏界面中显示Egret的Log。打开Log面板，在`index.html`文件中设置`data-show-log`字段为`true`，即显示Log面板，反之关闭。


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/jianshiqi.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/tiaoshi.png?raw=true