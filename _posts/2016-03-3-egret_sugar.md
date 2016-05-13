---
layout: post
title: "egret_sugar"
description: ""
category: 
tags: []
---
{% include JB/setup %}

语法糖：吃一颗糖开心一下吧

解释：糖是简化的语法，对原语言没有影响：a[i] = *(a + i )

例：

<e:Group class="app.MyGroup" xmlns:e="http://ns.egret.com/eui">
    <e:Image source="image/button_up.png" x="10">
        <e:scale9Grid>
            <e:Rectangle x="10" y="10" width="45" height="35"></e:Rectangle>
        </e:scale9Grid> 
    </e:Image>
</e:Group>

注：九宫格的语法糖

<e:Group class="app.MyGroup" xmlns:e="http://ns.egret.com/eui">
    <e:Image source="image/button_up.png" x="10" scale9Grid="10,10,45,35" ></e:Image>
</e:Group>


自定义组件

module app {   
    export class MyGroup extends eui.Group {       
        public constructor(){
            super();
        }
    }
}


egret 二维数组
