---
layout: post
title: "Egret学习之随机颜色"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}

 - 颜色代码

对于网页的颜色，大家都有所了解。除了RGB的表示方法外，还有十六进制色标表示法。例如黑色#000000，红色#ff0000，绿色#00ff00。其中`#`代表这是16进制。从00到ff时一个16进制，所以红色是`ff+00+00`的结果。

进而联想到，要产生随机颜色，需要至少产生三个随机16进制数，组合才能成为一个真正的颜色代码。

 - 怎样产生随机
 
 在js中，系统提供很多方法，帮助开发者产生随机数：

 1. 在j2se里我们可以使用Math.random()方法来产生一个随机数。这个产生的随机数是0-1之间的一个double，我们可以把他乘以一定的数，比如说乘以100，他就是个100以内的随机，这个在j2me中没有。 

 2. 在java.util这个包里面提供了一个Random的类，我们可以新建一个Random的对象来产生随机数。他可以产生随机整数、随机float、随机double，随机long，这个也是我们在j2me的程序里经常用的一个取随机数的方法。 
 
 3. 在我们的System类中有一个currentTimeMillis()方法，这个方法返回一个从1970年1月1号0点0分0秒到目前的一个毫秒数，返回类型是long，我们可以拿他作为一个随机数，我们可以拿他对一些数取模，就可以把他限制在一个范围之内。

不管是以上哪种随机数，都可以实现，举例说用Math.random()方法吧：

        var iFillColor:number = ( Math.floor( Math.random() * 0xff ) << 16 )
        + ( Math.floor( Math.random() * 0xff ) << 8 )
        + Math.floor( Math.random() * 0xff ) ;

Math.floor()方法也是js系统方法，它的作用是向下取整，和它相对的是Math.ceil()向上取整。这里取整的意义是保证了结果数是一个正确范围内的16进制数。

<< 的含义是左移16位，比如ff移动后就是十六进制的开头ff，后面的00向左移动8位，在最后面接着00，组成了红色#ff0000的十六进制色标。


----------


参考资料：

[js的随机数][1]

[js的移位操作][2]


  [1]: http://www.blogjava.net/cool2009/archive/2009/03/15/259882.html
  [2]: http://blog.csdn.net/chen_jp/article/details/8068448