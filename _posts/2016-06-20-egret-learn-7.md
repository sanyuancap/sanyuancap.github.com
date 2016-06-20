---
layout: post
title: "Egret学习之布局方式"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

Egret支持的布局方式主要有下面几种：

 - 环形

        var rLayout:RingLayout = new RingLayout;
        this._grpLayout.layout = rLayout;

 - 网格

        var tLayout:eui.TileLayout = new eui.TileLayout();
        tLayout.paddingTop = 30;
        tLayout.paddingLeft = 30;
        tLayout.paddingRight = 30;
        tLayout.paddingBottom = 30;
        this._grpLayout.layout = tLayout;

 - 水平

        var hLayout:eui.HorizontalLayout = new eui.HorizontalLayout();
        hLayout.gap = 10;
        hLayout.paddingTop = 30;
        hLayout.horizontalAlign = egret.HorizontalAlign.CENTER;
        this._grpLayout.layout = hLayout;

 - 垂直

        var vLayout:eui.VerticalLayout = new eui.VerticalLayout();
        vLayout.gap = 10;
        vLayout.paddingTop = 30;
        vLayout.horizontalAlign = egret.HorizontalAlign.CENTER;
        this._grpLayout.layout = vLayout;

 - 基础

 基本布局是默认的布局，在基本布局容器中，可以对布局元素进行绝对定位、居中定位、边距定位，以及百分比定位。

        this._grpLayout.layout = new eui.BasicLayout();

 - 自定义布局：

 这个列表的项渲染器放在了一个EXML文件中(goodsListIRSkin.exml)，通过设置List实例的itemRenderer属性指向EXML皮肤类名为其渲染器。



