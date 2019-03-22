---
layout: post
title: "sourcetree学习之巧妙使用遴选"
description: ""
category: sourcetree
tags: [sourcetree]
---
{% include JB/setup %}

在多人开发中，会有多个分支，经常会有从不同分支合并代码的需求。有时候分支之间合并的代码文件比较多，代码行比较多，很容易错乱。

一个很好的解决办法就是“遴选”，如果没有冲突，可以直接合并推送，非常方便，只要不手抖，几乎不会产生错提、漏提的情况。

    遴选：就是只合并分支上某个commit

 - 遴选的视图操作：

        1.打开sourcetree，切换到需要遴选提交代码的分支

        2.选中某些提交，右键选择遴选

        3.推送分支

 - 遴选的命令行操作：

        1.git checkout -b'feature' 切换到新分支

        2.git reflog  找到需要遴选的<commit_id1> <commit_id2>

        3.git cherry-pick <commit_id1><commit_id2> 把1、2的提交合并到新分支

        4.提交并推送

[更多git命令][1]

 [1]: https://www.cnblogs.com/garryfu/p/7988444.html