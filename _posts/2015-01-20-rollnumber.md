---
layout: post
title: "cocos2dx图片特效之数字滚动"
description: ""
category: cocos2dx
tags: [cocos2dx]
---
{% include JB/setup %}

数字上下转动效果
========

玩过捕鱼达人的都有同感，金币哗啦哗啦的增加时，那种爽快感。其实在游戏中数值显示是一个常用部件，cocos2dx虽然没有提供组件，但是也可以用代码轻松实现。将数字分解为个位 ，十位等，  每个位的对象都只需要管理自己这个位上的数字滚动显示，然后有一个对每个位进行管理的调度对象，将这些位相互之间的数学关系维护起来。

![rollNum][1]

    //主函数调用
    //设置6个
    RollNumGroup::createWithGameLayer(this, 6);
    m_pRollNumGroup->setPosition(ccp(353, 21));
    
    //不断更新数字纹理显示的位置，达到滚动数字的效果
    void RollNum::updateNumber(cocos2d::CCTime dt)
    {
        if(m_bRolling && m_nCurTexH == m_nEndTexH)
        {
            this->unschedule(schedule_selector(RollNum::updateNumber));
            m_bRolling = false;
            return;
        }
        if(m_bUp)
        {
            m_nCurTexH += 4;
            if(m_nCurTexH >= TEXTUREHEIGHT)
                m_nCurTexH = 0;
        }
        else
        {
            m_nCurTexH -= 4;
            if(m_nCurTexH < 0)
                m_nCurTexH = TEXTUREHEIGHT;
        }
        int h = m_nCurTexH;
        if(m_nCurTexH >= 180)
            h = 180;
        CCSpriteFrame *pFrame = CCSpriteFrame::createWithTexture(m_pTexture, CCRectMake(0, h, NUMBERWIDTH, NUMBERHEIGHT));
        this->setDisplayFrame(pFrame);   
        m_bRolling = true;
    }
    
    void RollNum::setNumber(int var, bool bUp)
    {    
        m_nNumber = var;
        m_bUp = bUp;
        //计算当前位的数字纹理滚动到位置
        m_nEndTexH = m_nNumber * (NUMBERHEIGHT + 4);
        //周期更新数字纹理的位置，形成滚动效果
        this->schedule(schedule_selector(RollNum::updateNumber), 0.01f);
       
    }

[具体代码请点击][2]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/rollNum.jpg?raw=true
  [2]: http://blog.csdn.net/hezeping888/article/details/9197385