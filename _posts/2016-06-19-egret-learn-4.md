---
layout: post
title: "Egret学习之文本"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 - 富文本

 
> 富文本格式（Rich
> TextFormat，即RTF）是由微软公司开发的跨平台文档格式，意即多文本格式。这是一种类似DOC格式（Word文档）的文件，有很好的兼容性。一般的格式设置，比如字体和段落设置，页面设置等等信息都可以存在RTF格式中。

 虽说Egret引擎是用来开发游戏的，对于网页排版等支持不多，但是仍然支持富文本。textFlow是设置富文本的入口。

 - 文本超链接

egret.TextEvent.LINK：用户在富文本中，单击超链时，对象将调度TextEvent属性，Line定义link事件对象的type属性值。

          text.textFlow = new Array<egret.ITextElement>(
                    { text:"这段文字有链接", style: { "href" : "event:text event triggered", underline:true } }, 
                    { text:"\n这段文字没链接", style: {"textColor" : 0x999999} }
                );
                text.touchEnabled = true;
                text.addEventListener(egret.TextEvent.LINK, function (e:egret.TextEvent) {
                    egret.log( e.text );
                }, this);


--------------------------------

 - 富文本标准格式

![fuwenben][1]

        text.textFlow = <Array<egret.ITextElement>>[
            {text: "妈妈再也不用担心我在", style: {"size": 20}}, 
            {text: "Egret", style: {"textColor": 0x336699, "size": 60, "strokeColor": 0x6699cc, "stroke": 2}},
            {text: "里说一句话不能包含", style: {"fontFamily": "楷体"}},
            {text: "各种", style: {"fontFamily": "楷体", "underline" : true}},
            {text: "五", style: {"textColor": 0xff0000}},
            {text: "彩", style: {"textColor": 0x00ff00}},
            {text: "缤", style: {"textColor": 0xf000f0}},
            {text: "纷", style: {"textColor": 0x00ffff}},
            {text: "、\n"},
            {text: "大", style: {"size": 56}},
            {text: "小", style: {"size": 16}},
            {text: "不", style: {"size": 26}},
            {text: "一", style: {"size": 34}},
            {text: "、"},
            {text: "格", style: {"italic": true, "textColor": 0x00ff00}},
            {text: "式", style: {"size": 26, "textColor": 0xf000f0}},
            {text: "各", style: {"italic": true, "textColor": 0xf06f00}},
            {text: "样的文字", style: {"fontFamily": "KaiTi"}},//楷体
            {text: "了！"}
        ];



或者XML格式：


        var str = '<font size=20>妈妈再也不用担心我在</font>'
                  + '<font color=0x336699 size=60 strokecolor=0x6699cc stroke=2>Egret</font>'
                  + '<font fontfamily="楷体">里说一句话不能包含</font>' 
                  + '<font fontfamily="楷体"><u>各种</u></font>' 
                  + '<font color=0xff0000>五</font>' 
                  + '<font color=0x00ff00>彩</font>' 
                  + '<font color=0xf000f0>缤</font>' 
                  + '<font color=0x00ffff>纷</font>' 
                  + '<font>、\n</font>' 
                  + '<font size=56>大</font>' 
                  + '<font size=16>小</font>' 
                  + '<font size=26>不</font>' 
                  + '<font size=34>一</font>' 
                  + '<font>、</font>' 
                  + '<font color=0x00ff00><i>格</i></font>' 
                  + '<font size=26 color=0xf000f0>式</font>' 
                  + '<font color=0xf06f00><i>各</i></font>' 
                  + '<font fontfamily="KaiTi">样的文字</font>' //楷体
                  + '<font>了！</font>' 
        text.textFlow = new egret.HtmlTextParser().parser(str);


--------------------------------


 - 输入文本示例

关于文本输入，是一个获得焦点、失去焦点、输入过程中的事件响应过程。egret.FocusEvent：用户将焦点从显示列表的一个对象更改到另一个对象时，对象将调度FocusEvent对象。目前只支持输入文本。

    var input:egret.TextField = new egret.TextField();
    input.addEventListener(egret.FocusEvent.FOCUS_IN, function (e:egret.FocusEvent) {
                label.text = "输入开始：";
            }, this);
            input.addEventListener(egret.FocusEvent.FOCUS_OUT, function (e:egret.FocusEvent) {
                label.text += "\n输入结束";
            }, this);
            input.addEventListener(egret.Event.CHANGE, function (e:egret.Event) {
                label.text = "输入开始：\n" + input.text;
            }, this);



  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/fubenwen.png?raw=true