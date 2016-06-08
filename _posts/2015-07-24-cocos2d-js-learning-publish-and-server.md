---
layout: post
title: "cocos2d-js学习之publish、server"
description: ""
category: cocos2d-js
tags: [cocos2d-js]
---
{% include JB/setup %}


## 发布游戏服务器登录操作

    //同步
    rsync -auxvp /Users/xxx/Desktop/projects/min_nmddl/Nmddl/publish/html5/  root@xxx.xxx.xxx.xxx:/data/static/nmddl

    //登录
    ssh -p 16322 root@xxx.xxx.xxx.xxx
    cd /data/static/

    //修改权限
    chmod -R 755 ProjectName

    //访问测试地址：
    http://xxx/static/nmddl/index.html

    //发布正式地址：
    http://xxx/cdn/nmddl/index.html

    //登录
    ssh xxx@xxx.xxx.xxx.xxx

    //根目录 创建nmddl文件夹
    rsync -auxvp /Users/ycma/Desktop/projects/min_nmddl/Nmddl/publish/html5/ xxx@xxx.xxx.xxx.xxx:~/nmddl
    su -
    da#@I*O(
    cp -r /home/ycma/nmddl/*  /data/static/nmddl/

## bugs

 * 本机使用rsync同步时报错：

```rsync error: error in rsync protocol data stream (code 12) at /SourceCache/rsync/rsync-45/rsync/io.c(453) [sender=2.6.9]```


目前还没有查到原因，可能是rsync版本问题，需要更新？

解决办法:用复制命令可以达到同样的效果：

    ```scp -r -P 16322 src/* root@223.252.196.144:/des```

 * 远程登录时出错：

    ```'id_rsa' are too open.```

解决办法：

    ```chmod  600  test.pem```

 * 远程登录时连接超时或者别的连不上问题
 
 解决办法：重置~/.ssh/id_rsa以及id_rsa.pub还有known_hosts，就可以解决

 * git和测试服务器的id_rsa冲突，等查到解决办法再更新































