---
layout: post
title: "sourcetree学习之大小写不敏感的问题"
description: ""
category: sourcetree
tags: [sourcetree]
---
{% include JB/setup %}


 - sourcetree大小写不敏感。
 
 修改了文件名大小写，但是sourcetree并没有比对出差异，导致提交文件出现了问题。

 - 解决办法：

将sourceTree项目中，选择自己的远程仓库，然后编辑配置文件，在打开的文件中，把config ignorecase = 改为false。