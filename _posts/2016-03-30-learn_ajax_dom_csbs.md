---
layout: post
title: "那些让我混乱的概念"
description: ""
category: web
tags: [前端]
---
{% include JB/setup %}

那些让我混乱的概念
=========

 - AJAX（Asynchronous JavaScript and XML）

异步的**JavaScript**与**XML**技术，指的是一套综合了多项技术的浏览器端网页开发技术。

![ajax][1]

> 其实就是为了解决传统页面同步刷新，消耗过多带宽，用户界面效果不友好等问题提出的。

**XMLHttpRequest**是AJAX的基础，可以提供不重新加载页面的情况下更新网页，在页面加载后在客户端向服务器请求数据，在页面加载后在服务器端接受数据，在后台向客户端发送数据。XMLHttpRequest对象提供了对 HTTP协议的完全的访问，包括做出 POST和 HEAD请求以及普通的 GET请求的能力。

> XMLHttpRequest可以同步或异步返回 Web服务器的响应，并且能以文本或者一个 DOM文档形式返回内容。

----------

 - DOM（对象文档模型（Document Object Model））

**DOM**可以以一种独立于平台和语言的方式访问和修改一个文档的内容和结构。也就是说，这是表示和处理一个HTML或XML文档的常用方法。DOM技术是用户页面可以动态的变化，从而大大使页面的交互性增强。

> 但是DOM必须通过JavaScript等脚本语言来进行读取，改变HTML、XHTML以及XML等文档,通过JavaScript对HTML网页内容进行操作

----------

 - C/S结构

**Client/Server**(客户机/服务器)结构，是大家熟知的软件系统体系结构，

> 通过将任务合理分配到Client端和Server端，降低了系统的通讯开销，可以充分利用两端硬件环境的优势。

早期的软件系统多以此作为首选设计标准。

 - B/S结构

**Browser/Server**(浏览器/服务器)结构，是随着Internet技术的兴起，对C/S结构的一种变化或者改进的结构。

> 在这种结构下，用户界面完全通过WWW浏览器实现，一部分事务逻辑在前端实现，但是主要事务逻辑在服务器端实现，形成所谓3-tier结构。

B/S结构，主要是利用了不断成熟的WWW浏览器技术，结合浏览器的多种Script语言(VBScript、JavaScript…)和ActiveX技术，用通用浏览器就实现了原来需要复杂专用软件才能实现的强大功能，并节约了开发成本，是一种全新的软件系统构造技术。

----------

 - jQuery

一个函数库

    语法：$(selector).animate({params},speed,callback);

示例：Jquery基础之DOM操作+AJAX

    <!DOCTYPE html>
    <html>
        <head>
            <script src="/jquery/jquery-1.11.1.min.js"></script>
            <script>
                $(document).ready(function(){
                  $("button").click(function(){
                    $("#div1").load("/example/jquery/demo_test.txt",function(responseTxt,statusTxt,xhr){
                      if(statusTxt=="success")
                        alert("外部内容加载成功！");
                      if(statusTxt=="error")
                        alert("Error: "+xhr.status+": "+xhr.statusText);
                    });
                  });
                });
            </script>
        </head>
        <body>
            <div id="div1"><h2>使用 jQuery AJAX 来改变文本</h2></div>
            <button>获得外部内容</button>
        </body>
    </html>


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/ajax.jpg?raw=true