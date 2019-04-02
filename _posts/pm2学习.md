
PM2是node进程管理工具，可以利用它来简化很多node应用管理的繁琐任务，如性能监控、自动重启、负载均衡等，而且使用非常简单

 - 生态文件:（方便管理所有应用的所有选择及环境变量）

 - 简单用法


        启一个应用: pm2 start app.js

        停止：pm2 stop app_name|app_id

        删除：pm2 delete app_name|app_id

        重启：pm2 restart app_name|app_id

        停止所有：pm2 stop all

        查看所有的进程：pm2 list

        查看所有的进程状态：pm2 status

        查看某一个进程的信息：pm2 show app_name|app_id

        查看日志： pm2 logs

 - 安装

        npm install -g pm2

 - nuxt + pm2生态文件

基础配置+日志切割

[PM2相关资料][1]

 - 概念


        npm nuxt node nginx yaml async koa koa-body koa-router koa-cors 



 [1]: https://www.jianshu.com/p/f640450bd120