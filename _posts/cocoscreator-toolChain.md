---
layout: post
title: "cocos2d-creator学习之工具流"
description: ""
category: cocos2d-js
tags: [cocos2d-js]
---
{% include JB/setup %}

对于cocos2dx开发，官方推荐的工具还是mac Xcode；cocos-js开发，官方推荐的工具是cocos creator。除此之外，图片压缩、整合工具、粒子工具等，也是游戏开发中必不可少的工具。

下面介绍了mac下比较常用的cocos工具流：

 - TinyPNG4Mac、ImageAlpha图片压缩工具

TinyPNG在一个在线图片压缩工具，这个压缩率很高，有50%-70%，而且几乎不损失画质。



![TinyPNG4Mac][5]

ImageAlpha软件是一个苹果电脑png图片压缩工具，通过压缩，可以将24 位的图片 PNG 文件转换成为 8 位通道的 PNG 文件单位。具体用法比较简单，就是单纯的拖拽+导出。

![ImageAlpha][6]

 - TexturePacker图片碎图整合工具


cocos2dx引擎底层的渲染方式是基于OpenGL的，OpenGL载入纹理图片时，所用内存会自动扩张到2的N次方。比如，一张图片的大小为10&times;10像素，OpenGL会按照16&times;16的规格将图片载入到内存中；如果图片大小为64&times;65，那么就会按照64&times;128载入了，这就造成了内存的无必要开销。

所以，在游戏开发使用图片资源时，我们要尽量保证图片的大小在接近且不大于2的整数倍，理想状态下，如果每一张图的长宽都恰好是2的n次方数值，就不会有任何浪费了。

TexturePacker正是帮助我们将图片资源进行这样优化的一款软件。

![TexturePacker][8]

TexturePacker控制的参数比较多，常用的参数如下：

       Texture Format:纹理格式,默认png

       Image format:图片像素格式，默认RGBA8888...根据对图片质量的需求导出不同的格式

       Dithering:抖动,默认NearestNeighbour,(如果图像上面有许许多多的“条条”和颜色梯度变化)将其修改成FloydSteinberg＋Alpha;

       Scale: 让你可以保存一个比原始图片尺寸要大一点、或者小一点的spritesheet。比如，如果你想在spritesheet中加载“@2x"的图片（也即为Retina-display设备或者ipad创建的）。但是你同时也想为不支持高清显示的iphone和touch制作spritesheet，这时候只需要设置scale为 1.0,同时勾选autoSD就可以了。也就是说，只需要美工提供高清显示的图片，用这个软件可以自己为你生成高清和普清的图片。

       Algorithm TexturePacker:里面目前唯一支持的算法就是MaxRects，即按精灵尺寸大小排列，但是这个算法效果非常好，因此你不用管它。

[更多参数][7]

[TexturePacker具体使用方法][16]
 - cocosBuilder UI拖拽拼接工具

cocosBuilder是cocos团队负责开发维护的界面拼接工具，是cocos creator的前身，在cocos creator推出后，团队逐渐舍弃了cocosBuilder，停止了维护和版本迭代，但是ccbi文件仍然支持。

![cocosBuilder][9]

       cocosBuilder工程会产生3类文件，后缀分别为ccbproj, ccb, ccbi，其中ccbproj和ccb是项目工程文件、界面文件，而ccbi是导出的文件，被cocos2dx程序使用。

 - GlyphDesigner字体位图制作工具

Glyph Designer的一大优势就是可以支持汉字录入，可以通过Included Glyphs（收录文字）面板来实现。比起Photoshop或Illuetrator，它的功能显得比较简单。

 ![GlyphDesigner][10]

[GlyphDesigner详细介绍][11]

 - ParticleDesigner粒子编辑工具

Particle Designer是Mac上的粒子效果编辑工具，可用于Cocos2D、Cocos2D-X、Kobold2D等游戏框架的粒子系统的辅助开发，可以直接导出为plist文件供程序使用。

Particle Designer以图形化的方式实时显示粒子效果，并且内置了数百款优秀的云端粒子特效，可直接使用，节省开发时间。

![ParticleDesigner][12]

[ParticleDesigner官方网址][13]

 - Tiled地图编辑工具

Tiled是一款地图编辑器。我们常用它编辑一些相似度很大的背景，例如:超级玛丽的地图、天天酷跑、COC等。这些游戏的地图都有一个共同点那么就是有很多相同的色块组成。如果用代码或者UI实现会非常繁琐，并且浪费资源。但是用底图编辑器，就可以轻松解决。

![Tiled][17]

[Tiled使用方法][15]

 - cocos creator 一体化游戏开发工具

官方介绍文档中，描述cocos creator是以内容创作为核心的一体化游戏开发工具。

       1.基于 Cocos2d-x
       2.组件化
       3.脚本化
       4.数据驱动
       5.跨平台发布

![cocos creator][18]

[cocos creator官网][19]

---

[更多工具介绍][2]

附引擎相关源码：

[cocos引擎源码][1]

[cocos2d-js-demo][3]

[cocos论坛：推荐官网中文论坛][4]

  
  [1]: https://github.com/fusijie/Cocos-Resource
  [2]: https://github.com/fusijie/Cocos-Resource
  [3]: https://cocos2d-x.org/js-tests/
  [4]: https://forum.cocos.com/
  [5]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-TinyPNG4Mac.png?raw=true
  [6]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-ImageAlpha.png?raw=true
  [7]: https://blog.csdn.net/junjun331/article/details/50779720
  [8]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-TexturePacker.png?raw=true
  [9]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-cocosBuilder.png?raw=true
  [10]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-GlyphDesigner.png?raw=true
  [11]: http://book.51cto.com/art/201504/473598.htm
  [12]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-ParticleDesigner.png?raw=true
  [13]: https://www.71squared.com/
  [14]: https://blog.csdn.net/oskytonight/article/details/11827107
  [15]: https://blog.csdn.net/Super_Cola/article/details/81084506
  [16]: https://www.cnblogs.com/guangyun/p/5908332.html
  [17]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-Tiled.png?raw=true
  [18]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-creator.png?raw=true
  [19]: https://www.cocos.com/