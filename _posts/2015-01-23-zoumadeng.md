---
layout: post
title: "cocos2dx图片特效之走马灯特效"
description: ""
category: cocos2dx
tags: [picEffect，]
---
{% include JB/setup %}

![effects][1]

图片效果很炫酷，感觉我等程序猿搞不定，需要美工妹子做动作帮忙？其实分析一下动画规律，也是可以用代码搞定的。
先特定关注单个子，比如第一个E字，它其实只有两个状态:一个实心，一个空心。它一直在重复一个动作：先变成实心的，很快就变成空心的，再变成实心，再空心...这样反复的交替。注意一个特点:实心出现的停留时间短些，空心的停留时间长些。 再看第二字,U，完全跟E是一个动作，只是比E慢一些时间出现。突然想起来这个效果就是球场上的人浪效果。每个人都有两个状态，站起来和蹲下，只是从左到右开始的时间不同。

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

[具体代码参考][2]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/picAffect.gif?raw=true
  [2]: http://www.2cto.com/kf/201411/355490.html