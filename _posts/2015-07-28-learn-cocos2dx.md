---
layout: post
title: "XCode6.0、7.0的iOS免证书真机测试方法"
description: ""
category: cocos2dx
tags: [cocos2dx]
---
{% include JB/setup %}


XCode7.0
--------

随着7.0的发布，囊中羞涩的开发者，终于可以告别模拟器，在真机上免费调试了！喜大普奔，快记录一下调试方法！

 - 下载xcode7
 - 配置accounts

 打开xcode，点击“xcode”，选择“Preferences”，选择“Accounts”，点击“＋”，增加“add apple ID”，将自己的账号输入进去
 
 - 连接手机

XCode6.0
--------

想知道7.0以前，我们大程序是怎样想方设法省那99美元吗？其实6.0开始，就有大神研究出怎样跳过模拟器，直奔真机调试了！当然前提是**手机已经越狱**！

- 在用来测试的真机Cydia中添加源：http://apt.weiphone.com

- 创建证书

    路径是`钥匙串访问-证书助理-创建证书`

- 配置文件

        cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS8.0.sdk/
        sudo cp SDKSettings.plist SDKSettings.plist.orig
        open .

在弹出的Finder窗口中双击`SDKSettings.plist`，会启动Xcode的图形界面，展开`DefaultProperties`分支，将下面的`ENTITLEMENTS_REQUIRED和CODE_SIGNING_REQUIRED`两个属性改为 NO。

        sudo chmod -R 777 iPhoneOS.sdk
        sudo chmod 777 *
        cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform
        sudo cp Info.plist Info.plist.orig
        open .

- 准备自定义的生成后脚本

        sudo mkdir /Applications/Xcode.app/Contents/Developer/iphoneentitlements
        cd /Applications/Xcode.app/Contents/Developer/iphoneentitlements
        sudo curl -O http://www.alexwhittemore.com/iphone/gen_entitlements.txt
        sudo mv gen_entitlements.txt gen_entitlements.py
        sudo chmod 777 gen_entitlements.py

- 修改工程设置



        export CODESIGN_ALLOCATE=/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/codesign_allocate
        if [ "${PLATFORM_NAME}" == "iphoneos" ] || [ "${PLATFORM_NAME}" == "ipados" ]; then
        /Applications/Xcode.app/Contents/Developer/iphoneentitlements/gen_entitlements.py "my.company.${PROJECT_NAME}" "${BUILT_PRODUCTS_DIR}/${WRAPPER_NAME}/${PROJECT_NAME}.xcent";
        codesign -f -s "iPhone Developer" --entitlements "${BUILT_PRODUCTS_DIR}/${WRAPPER_NAME}/${PROJECT_NAME}.xcent" "${BUILT_PRODUCTS_DIR}/${WRAPPER_NAME}/"
        fi

## 参考链接
 
[XCode6.0的iOS免证书真机测试方法（MAC及黑苹果均有效）](http://www.tuicool.com/articles/ZvmER3)
[XCode7.0的真机测试方法][1]


  [1]: http://blog.csdn.net/lengxue789/article/details/46976025
