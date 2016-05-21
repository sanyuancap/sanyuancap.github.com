---
layout: post
title: "iphone适配"
description: ""
category: cocos2d
tags: [适配]
---
{% include JB/setup %}

cocos2d如何适配iphone适配
========

cocos2d已经更新到了最新的版本 cocos2d-iphone-2.1-beta4。这个版本完美支持iphone 5.
以后的文件可以不用再进行特别的iphone5判断，只用对图片的后缀做一些命名就可以了。

> 最新版本已经对CCFileUtils进行了重写。可以指定后缀名和文件的插灶顺序。

比如：

    CCFileUtils *sharedFileUtils = [CCFileUtils sharedFileUtils];
    [sharedFileUtils setEnableFallbackSuffixes:NO];
    sharedFileUtils.enableiPhoneResourcesOniPad=YES;
    //指定每种版本对应的后缀名
    NSDictionary *dict =@{ 
        kCCFileUtilsDefault:@"",
        kCCFileUtilsiPadHD:@"-ipadhd",
        kCCFileUtilsiPad:@"-ipad",
        kCCFileUtilsiPhone5HD:@"-i5hd",
        kCCFileUtilsiPhone5:@"",
        kCCFileUtilsiPhoneHD:@"-hd",
        kCCFileUtilsiPhone:@""};
    sharedFileUtils.suffixesDict = [NSDictionary dictionaryWithDictionary:dict];
    //指定文件的查找循序，自己排列优先级。
    sharedFileUtils.searchResolutionsOrder = @[kCCFileUtilsiPadHD,kCCFileUtilsiPad,kCCFileUtilsiPhone5HD,kCCFileUtilsiPhoneHD,kCCFileUtilsiPhone5,kCCFileUtilsiPhone];


如果你不想自己命名一套后缀名的话，直接用默认的就可以了。默认的iphone5对应的文件后缀是 widehd。
