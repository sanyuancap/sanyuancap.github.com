---
layout: post
title: "cocos2d-js学习之webstorm"
description: ""
category: cocos2d-js
tags: [webstorm]
---
{% include JB/setup %}


cocos2d-js学习之webstorm
=====================

js的开发工具有很多，除了Webstorm，cocos code ide也是一种选择。之前有用过cocos code ide开发过几个小游戏，也是只会做一些浅层次的小游戏。现在有时间就深入了解一下js。

---

## 下载
下载WebStorm版，然后打开[注册码][ws]页面，选择一个进行注册。我下载的是10.0.2版。
![WebStorm][wsi]

---

## 新建和导入
[参考文档](http://cn.cocos2d-x.org/tutorial/show?id=1105)

先在网上下了几个小游戏源码，然后用WebStorm打开，file->new project from existing，选择files a local but no Web server is configured，选择游戏源码目录，点击设置根目录“Project Root”，finish。

当然也可以直接载入自带的打飞机游戏，前提是必须把根目录设置在cocos2dx-js的根目录，不然缺少framework各种组件。

新建游戏的命令可以在终端输入：```cocos new -l js```，可以在当前目录下查看到新建的游戏项目。

---

## 修改底色
修改底色，在preference里，搜索font，右侧选择新的scheme，并且点击save as chengjy，可以修改字号和配色，Apply。

---

## chrome和JetBrains
运行游戏的前提是有浏览器，选择google的chrome以后，要安装JetBrains IDE Support[插件][jb]。

---

## 运行和调试
可以点击小箭头run，也可以回到根目录，命令行输入：```cocos run -p web```，ctrl+c停止进程。

断点不能再html文件上打，可以在js打，快捷键小花+F8。

弹出调试窗口，过程跟xcode、vs差不多。

左侧有目录结构，函数清晰可见。

WebStorm自带Terminal终端，比较方便。

---

## 控制台bug？
所有的cc.log()都无法在控制台显示，网上有说是因为lite版本不支持之类的，可以修改配置文件project.json，修改参数debugMode为1即可。

如果不想修改参数，就用console.log()代替cc.log()。

---

## 快捷键
 - ctrl+D调试
 - ctrl+r运行
 - 小花+ctrl+左右箭头可以翻页
 - 小花+鼠标左键进入文件
 - 小花+shift+f全局查找
 - 小花+斜杠注销
 - 自己在终端配置文件中配置一个：
```alias cjyrun='cocos run -p web'```，以后每次运行cjyrun，不用苦逼的敲代码了

## 低容量？

 - 错误描述：

		low disk space on a webstorm system directory partition


解决办法：在`.//Applications/WebStorm.app/Contents/bin/idea.properties`
下，修改`idea.no.system.path.space.monitoring=true`配置就可以了。

[ws]:http://www.uzzf.com/soft/95516.
[jb]:https://chrome.google.com/webstore/detail/jetbrains-ide-support/hmhgeddbohgjknpmjagkdomcpobmllji
[wsi]:http://www.lupaworld.com/data/attachment/portal/201502/06/165818ziopi1hmsmxaopo5.png "Webstorm logo"


























