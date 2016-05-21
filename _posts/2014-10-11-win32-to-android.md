---
layout: post
title: "win32 to android"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##cocos2d-x win32移植到android

一．准备工具：

1.NDK R7版本以上
2.Android环境,JDK, Eclipse,Android SDK, NDK,Cygwin(windows上使用的交叉编译工具)。
3.Cocos2d-x 2.1rc0-x-2.1.3。

备注： 建议使用NDK R7 以上的版本，R7以后集成了Cygwin功能；请不要使用NDK R9,此版本有漏洞，警告信息会影响编译。

二．Android环境搭建：

Mac环境搭建，可参考http://www.myexception.cn/operating-system/1228154.html


三． Cocos2d中生成Android项目。

1. cocos2d-x目录下的create-android-project.bat，并进行修改，主要修改NDK_ROOT路径和ANDROIDTOOL路径，如下所示： 


![001](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-001.png)


如果没有使用cygwin，则不用指定cygwin。


2.运行cocos2d-x目录下的create-android-project.bat，依次输入包名，项目名，版本号。

![002](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-002.png)

![003](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-003.png)


3. 导入代码和资源文件

将win32项目中的classes和Resources中的文件拷贝过来。

4. 编译so

1）编辑proj.android\jni 目录中的Android.mk文件：



![004](https:/revolunet-logo/github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-004.png)



LOCAL_SRC_FILES：在这里加入Classes下的cpp文件
LOCAL_C_INCLUDES：在这里添加使用的库的h文件，如果有的话
LOCAL_LDLIBS：在这里添加使用的库的lib文件，如果有的话


每次那么多cpp文件，一个一个写文件名，要是有几百个cpp文件，那不崩溃了么，so贴一个群里大牛写的：



FILE_LIST := hellocpp/main.cpp  
FILE_LIST +=$(wildcard $(LOCAL_PATH)/../../Marbles/Classes/*.cpp)  
LOCAL_SRC_FILES := $(FILE_LIST:$(LOCAL_PATH)/%=%)  



2）运行cygwin，进入proj.android目录
3）运行build_native.sh脚本，编辑so



![005](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-005.png)


错误：
please define NDK_ROOT
在cygwin下的 /etc/defaults/etc/skel/.bash_profile
添加：
#ndk-root  
NDK_ROOT=/cygdrive/d/WORKBENCH/android-ndk-r8c  
export NDK_ROOT
然后重新编译即可。



5）等待编译完成，会看到android项目目录下多了很多文件，如下图：



![006](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-006.png)



5.导入Android项目到Eclipse,


1）打开eclipse  新建android项目：


![007](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-007.png)


点 next  注意下面的步骤。注意红框 Location 就是刚创建的andorid项目的位置。


![008](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-008.png)


点Next 选择 andorid版本。我选择的是 2.1



![009](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-009.png)


2）修改导入的android项目，好了项目导入进来了



![0010](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0010.png)


错误：
Cocos2dxActivity找不到
2.0以上版本的问题，将cocos2dx\platform\android\java\src\org\cocos2dx\lib目录下的文件拷贝到Eclipse项目的src\org\cocos2dx\lib中：


![0011](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0011.png)

3）配置Eclipse的NDK编译环境
下面在eclipse里面配置一下编译环境。
选中  win32androidDemo项目  点击 菜单栏 project -> properties 选项：



![0012](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0012.png)


点击 Builders， 接着点击 New...


![0013](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0013.png)


选中Program  点OK


![0014](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0014.png)


-------------------------------------------------------------------
下面的设置项有点多， 按图片来解说吧。  步骤都用红框圈出来了。
1. Name：  这里随便填一个就好了。 我填的是：win32android_Builder
2. 点击 Main
3. 点击  Browse File System...      弹出对话框后 选择NDK的安装路径 选中 ndk-build.cmd 文件。
4. 点击  Browse Workspace...      弹出对话框后 选择当前的项目。
5. 点击 Refresh (就在红色数字 2 的位置)
注意：现在  Apply  和   OK 都不要点。接着看下面的图。



![0015](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0015.png)



运行项目：




![0016](https://github.com/sanyuancap/myBlogPic/blob/master/win32-to-android/win32-to-android-0016.png)


三．移植项目时的注意点：
1）COCOS2D-X2.0以上因为OPGELES的关系不支持模拟器，所以请使用真机调试;
2）如果资源拷贝全，启动应用后会有黑屏问题。
3）.h文件中不能带有“::” 比如BattleScene::InitAllNotes()， 在gcc下会编译不通过。
4）如果在eclipse中出现资源编译问题，需确认图片资源的命名规则是否遵循android平台标准。
5）如果找不到某个object，需要确认，在adnroid.mk文件中，是否存在指定文件和目录。
6）移植到android后，可能会出现持久层数据文件(如xml,txt)，找不到的情况，如果有启动崩溃的问题，需要为这些文件指定全局路径，并确认android下，相关路径是否存在读写权限。




