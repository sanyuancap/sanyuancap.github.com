---
layout: post
title: "ssh秘钥冲突的解决办法"
description: ""
category: mac
tags: [mac]
---
{% include JB/setup %}

ssh秘钥冲突的解决办法
============

我本身有git的ssh秘钥，用于登录github和发布博客。但是最近开始开发了几款h5游戏，需要在测试服上面测试，直接导致的问题就是，我的ssh秘钥冲突了！

## 解决办法

 * 首先把测试服的秘钥设置为id_rsa与id_rsa.pub
 * 测试检验可以登入测试服
 * 设置git的秘钥为id_rsa.github和id_rsa.github.pub
 * 把git的秘钥拷贝到账户的ssh设置中
 * 在.ssh中新建config
 * 修改config权限

        chmod 600 ~/.ssh/config

 * 配置config

        Host [223.252.196.144]:16322
            IdentityFile ~/.ssh/id_rsa
            User root
         
        Host github.com
            IdentityFile ~/.ssh/id_rsa.github
            User sanyuancap

 * 测试输入ssh git@github.com，登陆成功！再也不用为ssh秘钥冲突发愁啦~

        PTY allocation request failed on channel 0
        Hi sanyuancap! You've successfully authenticated, but GitHub does not provide shell access.
        Connection to github.com closed.

 * 系统会自动产生一个known_hosts文件，里面是各种可以访问的域列表
        github.com,192.30.252.131 ssh-rsa AAAA...FAaQ==
        192.30.252.130 ssh-rsa AAAA...FAaQ==
        [223.252.196.144]:16322 ssh-rsa AAAA...U6P5
        192.30.252.129 ssh-rsa AAAA...FAaQ==
        192.30.252.128 ssh-rsa AAAA...FAaQ==


[参考链接](http://www.leeyupeng.com/2011/11/multiple-ssh-private-keys/)
























