---
layout: post
title: "jekyll post and page"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##post VS page
_post文件夹中放的是自己要发布的post文章。post文件的命名规则为YEAR-MONTH-DATE-title.MARKUP,使用rake post会自动将post文件命名合适。
而对于page，所有放在根目录下或不以下划线开头的文件夹中有格式的文件都会被Jekyll处理成page。
```rake post title="cjy"```