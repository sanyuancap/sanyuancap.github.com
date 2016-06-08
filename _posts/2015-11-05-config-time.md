---
layout: post
title: "cocos2dx-js学习之日期格式转换"
description: ""
category: cocos2dx-js
tags: [cocos2dx-js]
---
{% include JB/setup %}


最近项目遇到一个问题，要把当前时间转换成某些固定的格式，比如将当前日期改成自定义格式：2015-11-5--17：10：20，其实实现原理很简单，就是根据格式，分析年月日结果，然后展现出来。上网搜了下，有很多例子：


    Date.prototype.format = function(pattern) {
        /*初始化返回值字符串*/
        var returnValue = pattern;
        /*正则式pattern类型对象定义*/
        var format = {
            "y+": this.getFullYear(),
            "M+": this.getMonth()+1,
            "d+": this.getDate(),
            "H+": this.getHours(),
            "m+": this.getMinutes(),
            "s+": this.getSeconds(),
            "S": this.getMilliseconds(),
            "h+": (this.getHours()%12),
            "a": (this.getHours()/12) <= 1? "AM":"PM"
        };
        /*遍历正则式pattern类型对象构建returnValue对象*/
        for(var key in format) {
            var regExp = new RegExp("("+key+")");
            if(regExp.test(returnValue)) {
                var zero = "";
                for(var i = 0; i < RegExp.$1.length; i++) { zero += "0"; }
                var replacement = RegExp.$1.length == 1? format[key]:(zero+format[key]).substring(((""+format[key]).length));
                returnValue = returnValue.replace(RegExp.$1, replacement);
            }
        }
        return returnValue;
    };



[参考资料][1]


  [1]: http://hanqilong2006.blog.163.com/blog/static/34590531201371172839875/