---
layout: post
title: "关于推送notifications"
description: ""
category: 
tags: []
---
{% include JB/setup %}

  
    /*推送代码*/
    [[UIApplication sharedApplication] setApplicationIconBadgeNumber:0];
    [[UIApplication sharedApplication] cancelAllLocalNotifications];
    
    UILocalNotification *notification=[[UILocalNotification alloc] init];
    if (notification != nil)
    {
        notification.fireDate = [NSDate dateWithTimeIntervalSinceNow:role_delegate.pushTime_zh];
        notification.repeatInterval = kCFCalendarUnitWeek;
        notification.timeZone = [NSTimeZone defaultTimeZone];
        notification.alertBody = role_delegate.push_ZH;
        notification.alertAction = NSLocalizedStringFromTable(@"Now", @"language", nil);
        notification.applicationIconBadgeNumber = 1;
        notification.soundName = UILocalNotificationDefaultSoundName;
        [[UIApplication sharedApplication] scheduleLocalNotification:notification];
    }
    [notification release];