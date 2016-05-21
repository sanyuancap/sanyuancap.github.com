---
layout: post
title: "TextureCache SpriteFrameChache"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##CCSpriteFrameCache
CCSpriteFrameCache加载的是一张拼接过的大图，每一个小图只是大图中的一个区域，这些区域信息都在plist文件中保存。用的时候只需要根据小图的名称就可以加载到这个区域。

##CCTextureCache
CCTextureCache是普通的图片缓存，我们所有直接加载的图片都会默认放到这个缓存这那更，以提高调用效率。
因此，每次加载一张图片，或者通过plist加载一张拼接图时，都会将整张图片加载到内存中。如果不去释放，那就会一直占用着。
