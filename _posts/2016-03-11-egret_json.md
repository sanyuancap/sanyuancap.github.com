---
layout: post
title: "Egret学习之皮肤主题管理"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

Egret学习之皮肤主题管理
=============

 - 皮肤
 Egret跟cocos有很多不同，其中有一个就是皮肤分离机制，就是把样式从逻辑中解耦出来，用一个逻辑组件外加一个皮肤对象的方式去实现原来单个组件的功能。逻辑组件里只负责动态的逻辑控制代码，如事件监听和数据刷新。皮肤里只负责外观，如实例化子项，初始化样式和布局等静态的属性。

 - 主题

 但如果有一个全局通用的默认皮肤，我们需要每次实例化组件时都赋值一次皮肤，这样还是挺麻烦的。因此我们提供了一个主题机制，能够让您为指定的组件配置默认皮肤，全局指定一次即可，之后直接实例化组件，不再需要显式设置组件的skinName属性。


 主题的配置文件其实就是default.thm.json，例如：

		 {
		  "skins": {
		    "eui.Button": "skins/ButtonSkin.exml",
		    "eui.CheckBox": "skins/CheckBoxSkin.exml",
		    "eui.HScrollBar": "skins/HScrollBarSkin.exml",
		    "eui.HSlider": "skins/HSliderSkin.exml",
		    "eui.Panel": "skins/PanelSkin.exml",
		    "eui.ProgressBar": "skins/ProgressBarSkin.exml",
		    "eui.RadioButton": "skins/RadioButtonSkin.exml",
		    "eui.Scroller": "skins/ScrollerSkin.exml",
		    "eui.ToggleSwitch": "skins/ToggleSwitchSkin.exml",
		    "eui.VScrollBar": "skins/VScrollBarSkin.exml",
		    "eui.VSlider": "skins/VSliderSkin.exml"
		  },
		  "exmls": [ ],
		  "autoGenerateExmlsList": true
		}

[参考资料][1]

  [1]:http://edn.egret.com/cn/article/index/id/511