---
layout: post
title: "我的.bash_profile配置"
description: ""
category: mac
tags: [.bash_profile]
---
{% include JB/setup %}

我的.bash_profile配置
===================

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
