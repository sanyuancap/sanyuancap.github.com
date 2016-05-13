---
layout: post
title: "zoumadeng"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##走马灯效果

    void TitleSprite::extraInit(float delayTime){
        auto seq = Sequence::create(DelayTime::create(delayTime), CallFunc::create(CC_CALLBACK_0(TitleSprite::changeToPressFrame, this)), NULL);
        this->runAction(seq);
    }
     
    void TitleSprite::changeToNormalFrame(){
        this->setSpriteFrame(_normalFrameName);
        auto changeFrameAction = Sequence::create(DelayTime::create(1.6), CallFunc::create(CC_CALLBACK_0(TitleSprite::changeToPressFrame, this)), NULL);
        this->runAction(changeFrameAction);
    }
     
    void TitleSprite::changeToPressFrame(){
        this->setSpriteFrame(_pressFrameName);
        auto changeFrameAction = Sequence::create(DelayTime::create(0.6), CallFunc::create(CC_CALLBACK_0(TitleSprite::changeToNormalFrame, this)), NULL);
        this->runAction(changeFrameAction);
    }