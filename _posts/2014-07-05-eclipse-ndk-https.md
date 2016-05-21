---
layout: post
title: "MAC下Android的Eclipse开发环境的搭建"
description: ""
category: Android
tags: [环境,Android,Eclipse]
---
{% include JB/setup %}

MAC下Android的Eclipse开发环境的搭建
==

Eclipse的下载
----------

[点我下载][1]
选择正确的版本系统，确定自己的系统是32位还是64位

    打开终端，输入命令 uname -a 回车

 - x86_64 表示系统为64位
 - i686 表示系统32位的

 

安装ADT
-----

ADT是Android应用程序的开发环境。可以在线安装：

 - 点击菜单中的Help ——> Install New Software;
 - 在弹出的对话框中有个“Work with”，在右边的输入栏中输入：https://dl-ssl.google.com/android/eclipse/ 然后下面就会pending出来一个“Developer Tools”，勾选上，然后一路的Next。


下载Android SDK
-------------

[点我下载][2]
选择Mac OS X （intel）的SDK版本进行下载

安装Android SDK
-------------

解压安装包出来，然后运行tools/Android,在弹出的Android SDK and AVD Manager对话框中选择左边的Installed packages，右边就会列出当前已经安装了的SDK，点击下面的“Update All”然后一步一步来就会下载所有的Android SDK的版本并进行安装。

然后在菜单栏Eclipse —> Preferences（偏好设置）,会弹出一个Preferences对话框，选Android，然后在SDK Loaction中填入刚下载的SDK的路径或者点击右边的Browser选择。

     

生成模拟器
-----

菜单栏Window —> Android SDK and AVD Manger 会弹出对话框，然后在对话框中选择new开始按自己的需求新建模拟器。


  [1]: http://www.eclipse.org/downloads/
  [2]: http://developer.android.com/sdk/index.html