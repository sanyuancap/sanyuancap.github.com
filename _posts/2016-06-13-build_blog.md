---
layout: post
title: "免费的博客要不要？"
description: ""
category: web
tags: [web,博客]
---
{% include JB/setup %}

曾经github风靡一时的时候，就见过大神在上面搭建博客，我也曾想赶时髦，把博客从博客园转移过来，可惜一直没有功夫去弄。现在下定决心治愈我的拖延症！！so，开始吧~

简单说几个概念
-------

 - 为什么用jekyll+git+markdown？

 很好理解原因，免费是我的首选。我的博客只记录技术学习知识，并不是大型网站，也没什么数据库需求，jekyll足以满足我的需求；另外一个域名也不少钱呢，等我成了伪大神的时候，再去买一个吧，先用git顶一顶；再说markdown，用过之后都说好，sublime还专门有插件方便我们使用，何乐而不为？

 - jekyll是什么？

> jekyll是一个简单的博客形态的静态站点生产机器，不需要数据库即可支持一个独立博客站点。

 它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的Liquid渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。

 jekell的原理是先扫描post目录，layout目录, 然后是page，装入一个site对象后，用Liquide渲染出来。


 - Liquid模板语言

> Liquid uses a combination of tags, objects, and filters to load
> dynamic content. They are used inside Liquid template files, which are
> a group of files that make up a theme. For more information on the
> available templates, please see Building themes.

 简单地说Liquid就是使用一系列标签，对象和过滤器的组合来加载动态内容。

 举个栗子： Filters过滤器

![Liquid][1]

 - jekyll-bootstrap

 Jekyll-Bootstrap在Jekyll基础上，集成了twitter-bootstrap界面风格和一些实用的插件，并且易于扩展。
 
 bootstrap可以理解为：别人已经写好，具有blog雏形的简易blog开源系统框架，拿来即可使用。使用时把托管在Github上的jekyll-bootstrap框架clone下来，然后替换上面搭建个人主页的repository根目录下所有的文件。

 - markdown

> Markdown 是一个 Web 上使用的文本到HTML的转换工具，可以通过简单、易读易写的文本格式生成结构化的HTML文档。

![markdonw][2]

 Markdown 语法的目标是：成为一种适用于网络的书写语言。

 我以前直接在sublime用插件写，现在用作业部落的Cmd Markdown，是ghosert大神的神作，流畅友好，写起来很是受用啊~
 
 
 举个栗子：标题的写法
 
        # 这是 H1 #
        ## 这是 H2 ##
        ### 这是 H3 ######

 - jekyll 目录结构

如下：

       /jekyll_demo
       |--　_config.yml
       |--　_layouts
       |　　　|--　default.html
       |--　_posts
       |　　　|--　2012-08-25-hello-world.html
       |--　index.html 

----------


动手吧！
----

 1. 添加SSH Key（参考资料见文章末尾）；
 2. 在github页面上添加一个项目库库名为username.github.com；
 3. 下载boots框架  `git clone https://github.com/plusjade/jekyll-bootstrap.git`;
 4. 本地测试 `jekyll serve` ，打开浏览器在`http://localhost:4000`可以看到效果;
 5. 新建文章  `rake post title="Hello World"`;
 6. push刷新.

铛铛铛~~~完工！



具体的实现可以参考文章末尾的链接，jekyll的配置有很多，比如说config文件的修改，评论的添加等，在这里就不详述了。jekyll支持自定义主题，很多大神无私的奉献了很多漂亮的主题，比如这个theme-the-program主题，是不是很赞？！

![主题][3]

安装主题很简单，浏览到自己喜欢的主题，终端安装。举个栗子，安装theme-the-program主题：

    $ rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.git"


提供几个大神的jekyll博客赏析，拿走不谢~

[Franciskeke][4]

[panxw][5]

[hzmook][6]

[Joshua Leung][7]

[others][8]


----------


还是要吐槽下遇到的坑
----------

 - 首先是jekyll的缺点


 1. 它生成的是静态网页，添加动态功能必须使用外部服务，比如评论功能就只能用disqus。
 2. 它不适合大型网站，因为没有用到数据库，每运行一次都必须遍历全部的文本文件，网站越大，生成时间越长。


 - 安装失败

 很多时候，在安装gem的过程中会出现找不到资源的error，理由是什么就不多说了。这时候我们需要从另外一个gem服务器下载安装。通过`gem sources` 命令配置源，或通过修改Gemfile中的source语句可以实现。

       //常用的源
       https://rubygems.org/
       http://gems.github.com
       http://gems.rubyforge.org
       http://ruby.taobao.org 

       //显示当前使用的sources
       gem sources

       //添加一个source
       gem sources -a url地址

       //删除一个source
       gem sources -r url地址

       //更新source cache
       gem sources -u

 - 安装报错

问题打印，缺少了组件jekyll-sitemap

       Dependency Error: Yikes! It looks like you don't have jekyll-sitemap or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-sitemap' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/! 

解决办法：`$ gem install jekyll-sitemap`，安装完成就好使了。
  
  
       missing：
       /assets/themes/css/style.css
       /assets/themes/css/syntax.css
        
 - 权限问题

 本地浏览很丑，就因为缺少了css文件。
 
 ![cssMissing][9]
 
 可是为什么缺少了css样式文件，我直接clone下来，都没改过，难道是bootstrap出错了吗？在其他文件夹里找找吧，反正我是在themes/twitter/css里找到了。

       You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.

权限不足，那就改权限吧：把权限修改过来用命令`sudo chmod 777 /Library/Ruby/Gems/2.0.0`


----------


参考资料
-----

[jekyll快速上手][10]

[jekyll目录结构说明][11]

[搭建指南3][12]

[搭建指南2][13]

[搭建指南][14]

[问题集锦][15]

[markdown][16]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/jekyll/Liquid.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/jekyll/cmdMarkdown.png?raw=true
  [3]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/jekyll/zhuti.png?raw=true
  [4]: http://www.francissoung.com/
  [5]: http://www.panxw.com/
  [6]: http://hzmook.github.io/
  [7]: http://joshualeung.github.io/
  [8]: https://github.com/jekyll/jekyll/wiki/Sites
  [9]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/jekyll/cssMissing.png?raw=true
  [10]: http://jekyllbootstrap.com/usage/jekyll-quick-start.html
  [11]: http://www.chinaz.com/web/2014/0616/355745.shtml
  [12]: http://www.tuicool.com/articles/ruMVjyN/
  [13]: http://www.2cto.com/kf/201211/167662.html
  [14]: http://pigerla.com/learn-note/2013-06-12/create-a-blog-with-jekyll-bootstrap/
  [15]: http://www.jianshu.com/p/f5ebfadb0a20
  [16]: http://www.markdown.cn/