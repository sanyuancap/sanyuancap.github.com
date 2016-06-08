---
layout: post
title: "cocos2d-lua学习之最佳lua开发工具"
description: ""
category: cocos2d-lua
tags: [cocos2d-lua]
---
{% include JB/setup %}


## cocos IDE

虽然说官方最新版本说明，intel版本的还没有lua代码补全，下个版本会发布，所以lua开发者只有用1.2版本。但是实践出不管是哪个版本，都根本没有补全一说，只有js补全。网上有[添加用户自定义库的代码补全](http://blog.csdn.net/qqmcy/article/details/40149593)，但是IDE的版本之间相差太大，找不到添加入口，就算添加进去，也无法补全，只有不停的闪退和卡顿。

## 最佳的lua开发，还是sublime+QuickXDev

找遍了开发lua的工具，对于烂到家的工具只能说拜拜，还是sublime最方便，有quickXDev插件，可以有quick的代码补全。

 * DoshDoc的安装，Shift+小花+P，选择install Package
 * 输入QuickXDev就安装成功了

## DoshDoc，API阅读文档的首选
 * DoshDoc的安装，Shift+小花+P，选择install Package，输入DoshDoc就安装成功了 
 * DoshDoc安装Bug：安装后无法跳转,提示quick_cocos2dx_root no set

	解决办法：[参考文档](http://blog.sina.com.cn/s/blog_750aad9a0101bf8v.html)

 * 添加quick-cocos2dx路径:cd到quick的root下，运行setup.py，可以在bash_profile中看到quickroot的路径。
 * 找到packageSetting里面的quickxdev，在default里填入root路径，并且把所有数值复制到user里

 * DoshDoc的使用方法：光标落在API出，快捷键Ctrl+Shift+G，选择提示的API列表即可
