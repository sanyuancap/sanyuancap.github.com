---
layout: post
title: "bash_profile"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##cjy' custom##
alias sshlogin='ssh -p 16322 root@223.252.196.144'
alias cdGaoPlane='cd /Users/easegame/chengjunyuan/MiniGameSVN/GaoPlane/'
alias synssh='scp -r -P 16322 /Users/easegame/chengjunyuan/MiniGameSVN/GaoPlane/publish/html5/* root@223.252.196.144:/data/static/GaoPlane/'

alias cocospublish='cocos compile -p web -m release'

alias cdcjy='cd /Users/easegame/chengjunyuan/'

alias gita='git add .'
alias gitc='git commit -m'
alias gitp='git push'
alias subl='/Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl'
alias cdpost='cd /Users/easegame/chengjunyuan/myBlog/sanyuancap.github.com/_posts'
alias newblog='rake post'
alias cdblog='cd /Users/easegame/chengjunyuan/myBlog/sanyuancap.github.com/'

alias cjyinstall='brew cask install'

alias sourcezsh='source /Users/easegame/.zshrc'
alias sourcebash='source /Users/easegame/.bash_profile'

alias cls='clear'
alias ll='ls -l'
alias la='ls -a'
alias vi='vim'
alias javac="javac -J-Dfile.encoding=utf8"
alias grep="grep --color=auto"

export ANDROID_SDK_ROOT=/Users/easegame/chengjunyuan/chengDocument/android-sdk_r24_2
export ANDROID_NDK_ROOT=/Users/easegame/chengjunyuan/chengDocument/android-ndk-r10d
export NDK_ROOT=/Users/easegame/chengjunyuan/chengDocument/android-ndk-r10d
export PATH=$PATH  ANDROID_SDK_ROOT
export PATH=$PATH  ANDROID_NDK_ROOT
export PATH=$PATH  NDK_ROOT
export ANT_ROOT=/Applications/Cocos/tools/ant/bin

# Add environment variable COCOS_CONSOLE_ROOT for cocos2d-x
export COCOS_CONSOLE_ROOT=/Users/easegame/chengjunyuan/mySVN/cocos2d-x-3.6/tools/cocos2d-console/bin
export PATH=$COCOS_CONSOLE_ROOT:$PATH

# Add environment variable COCOS_FRAMEWORKS for cocos2d-x
export COCOS_FRAMEWORKS=/Applications/Cocos/frameworks
export PATH=$COCOS_FRAMEWORKS:$PATH

# Add environment variable COCOS_TEMPLATES_ROOT for cocos2d-x
export COCOS_TEMPLATES_ROOT=/Users/easegame/chengjunyuan/mySVN/cocos2d-x-3.6/templates
export PATH=$COCOS_TEMPLATES_ROOT:$PATH

# Add environment variable QUICK_V3_ROOT for cocos2d-x
export QUICK_V3_ROOT=/Users/easegame/chengjunyuan/chengDocument/quick-3.5
export PATH=$QUICK_V3_ROOT:$PATH
