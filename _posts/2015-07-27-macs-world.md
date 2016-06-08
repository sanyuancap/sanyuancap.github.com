---
layout: post
title: "我的.bash_profile配置"
description: ""
category: mac
tags: [.bash_profile]
---
{% include JB/setup %}


## 怎样在命令行中用sublime打开文本文档？

在配置文件中设置

    alias subl='/Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl'

打开时用subl命令

    subl 2015-07-27-macs-world.md


## 怎样快速的切换到目录？

在配置文件中设置
    
    alias cdcjy='cd /Users/easegame/xxx/'

打开时用subl命令

    cdcjy

## 怎样缩短命令行？

在配置文件中设置

    alias cjyinstall='brew cask install'

打开时用cjyinstall命令

    cjyinstall

## 如何切换zsh and bash？

输入命令

    chsh -s /bin/zsh
    chsh -s /bin/bash

重启客户端

## 我的zsh配置

    alias gita='git add .'
    alias gitc='git commit -m'
    alias gitp='git push'
    alias subl='/Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl'
    alias cdcjy='cd /Users/easegame/xxx/'
    alias cdpost='cd /Users/easegame/xxx/myBlog/sanyuancap.github.com/_posts'
    alias newblog='rake post'
    alias cdblog='cd /Users/easegame/xxx/myBlog/sanyuancap.github.com/'
    alias cjyinstall='brew cask install'
    alias sourcezsh='source /Users/easegame/.zshrc'

## cocos2d-js发布包

    alias cocospublish='cocos compile -p web -m release'

## 配置bash文件

    alias configbash='open /Users/ycma/.bash_profile'
    alias sourcebash='source /Users/easegame/.bash_profile'

## 环境配置

    export ANDROID_SDK_ROOT=/Users/easegame/xxx/chengDocument/android-sdk_r24_2
    export ANDROID_NDK_ROOT=/Users/easegame/xxx/chengDocument/android-ndk-r10d
    export NDK_ROOT=/Users/easegame/xxx/chengDocument/android-ndk-r10d
    export PATH=$PATH  ANDROID_SDK_ROOT
    export PATH=$PATH  ANDROID_NDK_ROOT
    export PATH=$PATH  NDK_ROOT
    export ANT_ROOT=/Applications/Cocos/tools/ant/bin

    # Add environment variable COCOS_CONSOLE_ROOT for cocos2d-x
    export COCOS_CONSOLE_ROOT=/Users/easegame/xxx/mySVN/cocos2d-x-3.6/tools/cocos2d-console/bin
    export PATH=$COCOS_CONSOLE_ROOT:$PATH

    # Add environment variable COCOS_FRAMEWORKS for cocos2d-x
    export COCOS_FRAMEWORKS=/Applications/Cocos/frameworks
    export PATH=$COCOS_FRAMEWORKS:$PATH

    # Add environment variable COCOS_TEMPLATES_ROOT for cocos2d-x
    export COCOS_TEMPLATES_ROOT=/Users/easegame/xxx/mySVN/cocos2d-x-3.6/templates
    export PATH=$COCOS_TEMPLATES_ROOT:$PATH

    # Add environment variable QUICK_V3_ROOT for cocos2d-x
    export QUICK_V3_ROOT=/Users/easegame/xxx/chengDocument/quick-3.5
    export PATH=$QUICK_V3_ROOT:$PATH





