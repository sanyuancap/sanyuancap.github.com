---
layout: post
title: "cocos2d-js学习之时间选择器的实现"
description: ""
category: cocos2dx
tags: [cocos2dx]
---
{% include JB/setup %}

cocos2d-js学习之时间选择器的实现
=====================

产品提出需求了，要在游戏中做一个时间选择器，但是ScrollView繁琐，最重要的是listview控件可以支持滑动和选择，但是没有循环滑动，并且没法定位，只有自己用代码实现了。网上搜索到大神写的半成品，拿来借鉴下。

![选择器][1]

## 核心代码分析：
 1. 鉴于效率和方便性，使用一个contentNode来管理所有item。
 2. 通过_bMoveing和_bTouching标识来处理触摸和移动之间相互影响。
 3. 循环滚动的实现逻辑：向上移动，那么最上的item会移动到最下，向下则反之。
 4. 在操作结束之后，做矫正平衡（准确移动到固定的位置）。

        
        var ScrollSelector = ccui.Layout.extend({
            ...
            
            update: function(dt){
                if(!this._bTouching && this._bMoveing){ // Action中的时候，计算偏移量
                    var diffY = this._contentNode.y - this._beginPos.y;
                    this._diffYCount = this._diffYCount + diffY;
                    this._beginPos = this._contentNode.getPosition();
                }
                this._balance();
                if(this._bBeginCountTime) this._timeCount = this._timeCount + dt;
            },
    
            _onTouchBegan:function (touch, event) {
                ...
            },
    
            _onTouchMoved:function (touch, event) {
                // Move中的时候，计算偏移量
                ...
                var diffY = getPoint.y - target._beginPos.y;
            },
    
            _onTouchEnded:function (touch, event) {
                ...
                // 计算滑动  计算距离  计算速度
                if (target._timeCount < target._timeCondition) {
                    var distance = Math.round(target._onceDiffYCount*target._velocity);
                    var time = target._timeCount * target._velocity;
                    var pn = distance > 0 ? 1 : -1;
                    distance = Math.abs(distance) > Math.abs(target._distanceLimit) ? pn * target._distanceLimit: distance;
                    time = time < target._timeLimit ? target._timeLimit: time;
                    var move = cc.moveBy(time, 0, distance);
                    target._runningAction = cc.sequence(move.easing(cc.easeSineOut()), cc.callFunc(target._bounceBalance, target));
                    target._runningAction = target._contentNode.runAction(target._runningAction);
                    target._beginPos = target._contentNode.getPosition();
                    target._bMoveing = true;
                }else{ // 如果不移动，那么直接做平衡
                    target._bounceBalance();
                }
                target._onceDiffYCount = 0;
                target._timeCount = 0;
                target._bBeginCountTime = false;
            },
        });
    
    
[参考文章][2]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/selectTime.jpg?raw=true
  [2]: http://blog.csdn.net/xiaofeiaiai/article/details/42025407

  