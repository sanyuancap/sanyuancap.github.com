---
layout: post
title: "listView cycle"
description: ""
category: 
tags: []
---
{% include JB/setup %}
##扩展listview
listview控件可以支持滑动和选择，但是没有循环滑动，并且没法定位。下面是对listView的扩展。

/*js*/

    var scene2_0Layer = cc.Layer.extend({
        sprite:null,
        buttonX : null,
        ctor:function () {
            this._super();
        var list = ["1","2","3","4","5","6","7","8","9","10","11","12"];
        var definition = {
            size:cc.size(60,460),
            items:list,
            backGround: res.clip_PIC
        };
        var monthNode = new ScrollSelector(definition);
            this.addChild(monthNode);
            return true;
        }
    });

    var ScrollSelector = ccui.Layout.extend({
        _visibleClipNumber:5,   // 同时显示Item的个数
        _velocity:3,            // 速率
        _timeLimit:0.5,         // 时间限制
        _distanceLimit:500,     // 距离限制
        _timeCondition:0.3,     // 时间条件
        _distanceCondition:30,  // 距离条件

        _diffY:0,
        _diffYCount:0,          // 周期性计数,y轴的移动距离
        _onceDiffYCount:0,      // 一次触摸y轴的移动距离
        _timeCount:0,           // 触摸时间计时
        _runningAction:null,
        _list:null,             // item列表，用来平衡坐标
        _originList:null,
        _currentItemIndex:2,          // 目前是第几个item
        _value:null,            // 当前item的value
        _beginPos:null,
        _contentNode:null,
        _backGround:null,

        _bMoveing:false,
        _bTouching:false,
        _bBeginCountTime:false,

        _fontColor: cc.color.BLACK,
        _fontSize: 40,
        _fontname: "Arial",
        // _mode:null,             //游戏类型：选择器，游戏器

        ctor: function (params) { //params 参数列表： items, textures.back, size
            this._super();
            this.setClippingEnabled(true);
            this.setContentSize(params.size);//每一个数字的content
            this.setAnchorPoint(cc.p(0.5, 0.5));
            this.ignoreAnchor = false;
            this._backGround = new cc.Sprite(params.backGround);
            this.addChild(this._backGround);
            this._backGround.setVisible(false);
            this._backGround.x = this.width/2;
            this._backGround.y = this.height/2;
            this._contentNode = new cc.Node();
            this._contentNode.setAnchorPoint(cc.p(0.5,0));
            this.addChild(this._contentNode);
            this._contentNode.setPosition(cc.p(this.width/2, 0));

            // 创建N个Item
            this._list = [];
            this._originList = [];

            for(var i = 0; i < params.items.length; i++){
                var text = ccui.Text.create(params.items[i], this._fontName, this._fontSize);
                text.setTextVerticalAlignment(cc.VERTICAL_TEXT_ALIGNMENT_CENTER);
                text.getVirtualRenderer().setColor(this._fontColor);
                text.setTextAreaSize(cc.size(params.size.width, 50));
                text.setPosition(cc.p(0, i* text.height + text.height/2));
                this._contentNode.addChild(text,1,i);
                this._list.push(text);
                this._originList.push(text);
            }
            this._value = this._originList[1].getString();

            this._lister = cc.EventListener.create({
                swallowTouches: true,
                event: cc.EventListener.TOUCH_ONE_BY_ONE,
                onTouchBegan:this._onTouchBegan,
                onTouchMoved:this._onTouchMoved,
                onTouchEnded:this._onTouchEnded
            });
            cc.eventManager.addListener(this._lister ,this);
            this.scheduleUpdateWithPriority(0);

            // init data
            this._diffYCount = this._list[0].height;
            this._beginPos = cc.p(0,0);
            this._distanceLimit = params.size.height*2 + Math.random()*50;

        },

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
            var target = event.getCurrentTarget();
            if (!target.containsTouchLocation(touch)) return false;
            target._beginPos = touch.getLocation();
            target._bTouching = true;
            target._bMoveing = false;
            if (target._contentNode.isRunning())
                target._contentNode.stopAction(target._runningAction);
            // 开启滑动计时
            target._bBeginCountTime = true;
            target._timeCount = 0;
            return true;
        },

        _onTouchMoved:function (touch, event) {
            // Move中的时候，计算偏移量
            var target = event.getCurrentTarget();
            var getPoint = touch.getLocation();
            var diffY = getPoint.y - target._beginPos.y;
            target._contentNode.y = target._contentNode.y + diffY;
            target._beginPos = getPoint;
            target._diffYCount = target._diffYCount + diffY;
            target._onceDiffYCount = target._onceDiffYCount + diffY;
        },

        _onTouchEnded:function (touch, event) {
            var target = event.getCurrentTarget();
            target._bTouching = false;

            // 计算滑动  计算距离  计算速度
            if (/*Math.abs(target._onceDiffYCount) > target._distanceCondition &&*/ target._timeCount < target._timeCondition) {
                if (target._contentNode.isRunning())  target._contentNode.stopAction(target._runningAction);
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

        containsTouchLocation:function (touch) {
            var getPoint = touch.getLocation();
            var myRect = this.getBoundingBox();
            return cc.rectContainsPoint(myRect, getPoint);
        },

        _balance:function(){
            if(this._diffYCount > this._list[0].height){
                var topItem = this._list.pop();
                topItem.y = this._list[0].y - this._list[0].height;
                this._list.unshift(topItem);
                this._diffYCount = this._diffYCount - this._list[0].height;
            }else if (this._diffYCount < -this._list[0].height) {
                var bottomItem = this._list.shift();
                bottomItem.y = this._list[this._list.length-1].y + this._list[this._list.length-1].height;
                this._list.push(bottomItem);
                this._diffYCount = this._diffYCount + this._list[0].height;
            }
        },

        _bounceBalance:function(){
            var itemHight = this._list[0].height;
            var num = Math.round(this._contentNode.y%itemHight);
            var distance = 0;
            if ( num > 0){
                distance = num > itemHight/2 ? itemHight-num : -num;
            }else {
                distance = num > -itemHight/2 ? -num : -(itemHight + num);
            }
            var action = cc.moveBy(0.2, 0, distance).easing(cc.easeSineOut());
            this._contentNode.runAction(cc.sequence(action, cc.callFunc(this._end, this)));
        },

        _end: function(){
            var num = Math.round(this._contentNode.y/this._list[0].height);
            var num2 = -1 * (num % this._list.length);
            if (num2 > 0){
                this._currentItemIndex = num2 + 2;
            }else if (num2 < 0){
                this._currentItemIndex = this._list.length + num2 + 2;

            }else{
                this._currentItemIndex = 2;
            }
            if (this._currentItemIndex > this._list.length){
                this._currentItemIndex = this._currentItemIndex % this._list.length;
            }
            this._value = this._originList[this._currentItemIndex-1].getString();
            cc.log(this._value);


        }

    });