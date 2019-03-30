# impress.js 制作酷炫 PPT
## impress.js 概述
impress.js是基于**CSS3**转换和过渡的表现层框架，工作于现代浏览器(Google Chrome或Safari (或 Firefox 10 或 IE10))的创建在线演示的**JS**库， 可以让开发者轻松创建杀手级在线演示PPT。

 - 实现效果：炫酷

三维空间的无限延伸，3D效果，任意角度的旋转，任意大小的缩放，把一页幻灯片放在三维空间的任一位置等。

impressjs 的代码量也不大,一千行左右，注释非常清晰，基本可以当文档读。

 - 流行的幻灯工具[(更多幻灯工具)][6]

有不少的HTML slides的工具, deckjs, reveal, slides 等等大概十来种吧。逐个看过效果后就决定由impressjs了，效果最炫。impressjs就是仿照prezi。

 1. Prezi[(Prezi.app)(收费)][5]

Prezi的技术基于Flash。

 2. 斧子演示[(AxeSlide.app)(2015年)(收费、已倒闭)][3]

斧子演示是一款基于H5技术开发的演示文稿制作软件。

 3. Focusky[(Focusky.app)(收费)][4]

输出格式：EXE/视频/MacApp/在线上传/PDF/HTML等。

 4. Reveal.js[(github源码)][7]

支持markdown，非常方便将平时用markdown作的笔记，借用pandoc迅速转成展示用的幻灯片。它的特点在于可以水平和垂直两个方向进行幻灯片的切换

 5. Bespoke.js[(github源码)][11]

基于浏览器的演示文稿微框架，支持 Gulp 构建系统的样板演示。
 
 6. Impressionist 和 Strut (impress在线编辑器)

Strut在线编辑支持markdown+css编码，可以导入json，导出json或者zip包。

[Strut在线编辑][8]
[Strut github源码][10]
[Impressionist github源码][9]

 7. blockly + impress[(demo)][12]

blockly包装的impress.js可视化编辑demo[(github源码)][13]

## impress 优缺点

缺点：

1. impressjs 不支持页内段落动画 （开始显示一部分，按空格后再显示另一部分）。

impress.js只适用于注重幻灯片的切换效果的场合，比如商业总结性报告，在线简历等。对于单张幻灯片的细枝末节却需要一点一点的写代码。

2. 结合图表
百度的图说不错，试了下果然是不错，数据输入简单，有点类似excel. 显示效果看起来也是挺好的。建了个图表试了下，在线显示的确挺不错的，但是放到自己的页面中那些样式就消失了， 提供的代码原来不包含样式的。没有办法，只能放弃了，本来还是想用下国产的

## impress 代码解析

 - 简化模板
去除掉了一些css加载，js加载和注释的相关语句。虽然不能正常运行，但是可以很清楚的看出使用impress.js的相关语法。

```html
<!doctype html>
<html lang="zh">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
    <title>a mod of impress.js</title>
</head>
<body>
    <div id="impress">  
        <div class="fallback-message">
            Your browser doesn't support impress.js.  Try Chrome or Safari.
        </div>
        <div id="first" class="step" data-x="0" data-y="0" data-z="0" data-rotate="0" data-rotate-x="0" data-rotate-y="0" data-scale="0">
            <p>This is my first slide.  </p>
        </div>
    </div>
</body>
</html>
```

1. 先建立一个id="impress"的div，表示初始化它里面impress的相关语句；
2. 然后是class="fallback-message"也就是回调函数的div，表示如果浏览器不支持就返回这些信息：Your browser doesn't support impress.js. Try Chrome or Safari.
3. 最后是id="first" class="step"的div，表示这是一张幻灯片。

解释一下幻灯片语句里面的相关参数：

    id="first"这张幻灯片的id，可以自定义，方便css文件中调。
    class="step"表示这是一张幻灯片，必须写step。
    data-x表示这张幻灯片的x轴偏移量，y，z也是同理。
    data-rotate表示这张幻灯片的三围旋转量，x，y，z也是同理。
    data-scale表示这张幻灯片的放大缩小量。

 - 详细介绍

1. 坐标

impress.js创建了一个三维空间，所有的幻灯片都有各自的位置坐标（x，y，z）。

整个空间的中心是原点（0，0，0）。

其他的幻灯片或文字都是相对于这个原点来设置位置的。（中心不一定是第一张幻灯片）

data-x——表示x轴坐标
data-y——表示y轴坐标
data-z——表示z轴坐标

只有x和y坐标是必须的。

需要注意的是Y轴向上是负值。简单的理解就是：往右（x），往下（y），往上（z）是正值；相应为负值。

![impress_position][15]
2. id（可选）

id（可选）——可以用来表示幻灯片的顺序，格式是id=“step-N”，（比如id=”step-2″，序号为2）。

如果不指定id的话，幻灯片按照代码从上往下的顺序出现。

3. class（必须）

class（必须）——通常有两个值，“step”表示一个步骤，元素透明显示，“step slide”有幻灯片白色方框。

其他的调整选项都以data开头。

4. 旋转

data-rotate——表示旋转，分别有data-rotate-x，data-rotate-y和data-rotate-z

正值表示按照相应的轴顺时针旋转，负值则是逆时针。

5. 插入媒体

使用video和audio标签插入音视频，控制方式有三种：
        
``` html
controls
<!-- 显示视频控制条 -->
loop
<!-- 自动播放，循环播放 -->
autoplay
<!-- 自动播放 -->

<video width="320" height="460" autoplay>
    <source src="video/test.webm" type=video/webm>
</video>
```   
在impress.js中，把视频标签放入DOM限制了媒体的**autoplay**。这时我们可以在impress.js中插入这段代码：

``` js
// 设置了两个变量，分别代表幻灯片和视频文件，后面分别填上相应的id。
var videoStep = document.getElementById("video-step");
var video1 = document.getElementById("video-1");
var video2 = document.getElementById("video-2");
// 监听当前幻灯片上的事件，如果进入幻灯片就执行相应的函数（即播放视频文件）
// 设置离开幻灯片时执行的函数（即暂停视频文件）。
videoStep.addEventListener("impress:stepenter", function(){
    video1.play();
}, false);
videoStep.addEventListener("impress:stepleave", function(){
    video1.pause();
}, false);
// 一张幻灯片里放入多个视频或音频
videoStep.addEventListener("impress:stepenter", function(){
    video1.play();
    video2.play();
}, false);
```

``` html
<!-- 把有视频的那张幻灯片的id设为video-step，视频的id设为video。 -->
<div id="video-step" class="step" data-x="-50000" data-y="2000" data-z="-60000" data-scale="6">
    <video id="video" width="420" height="340" autoplay>
        <source src="video/IMG_1254.webm" type="video/webm">
    </video>
</div>
```

6. markdown

```markdown
<div id="common" class="step markdown"  data-rel-x="0" data-rel-y="-3000" data-rotate="360" data-scale="4">
# impress.js 制作酷炫 PPT
## impress.js 概述
impress.js是基于**CSS3**转换和过渡的表现层框架，工作于现代浏览器(Google Chrome或Safari (或 Firefox 10 或 IE10))的创建在线演示的**JS**库， 可以让开发者轻松创建杀手级在线演示PPT。

```

5. 其他

data-transition-duration——幻灯片切换的时间，默认为1000，单位为ms（1000ms=1s）

data-perspective——表示视角，设为0则取消3D效果。默认为1000。


 - impress 主要API

``` js
    goto(), init(), next(), prev()，initStep（）

    pfx（）// 它通过检测浏览器给css3属性加上当前浏览器可用的前缀，这样就不用人工手写'Webkit" ,"Moz" 'O' ,'ms' .'Khtml'等浏览器前缀
    arrayify（） //将Array-Like对象转换成Array对象
    css（）// -将指定属性应用到指定元素上
    toNumber（）//  将参数转换成数字，如果无法转换返回默认值
    byId（）// -通过id获取元素
    $（）//  返回满足选择器的第一个元素
    $$（）// -返回满足选择器的所有元素
    triggerEvent（）//  在指定元素上触发指定事件
    translate（）// -将translate对象转换成css使用的字符串
    rotate（）// -将rotate对象转换成css使用的字符串
    scale（）// - 将scale对象转换成css使用的字符串
    perspective（）// -将perspective对象转换成css使用的字符串
    getElementFromHash（）// - 根据hash来获取元素，hash就是URL中形如#step1的东西computeWindowScale（）// - 根据当前窗口尺寸计算scale。用于放大和缩小当前窗口
```
-----

[impress学习文档][1]
[impress学习文档2][14]
[impress学习demo][2]

[1]: https://www.jianshu.com/p/388843ed117b
[2]: https://hashdog.com/brochure/#/second
[3]: http://www.pc6.com/mac/233523.html
[4]: http://www.focusky.com.cn/
[5]: https://prezi.com/
[6]: https://www.jianshu.com/p/09a3bbb8b362
[7]: https://github.com/hakimel/reveal.js
[8]: http://strut.io/editor/#
[9]: https://github.com/harish-io/Impressionist
[10]: https://github.com/tantaman/Strut
[11]: https://github.com/bespokejs/bespoke
[12]: http://summerscar.me/impress-blockly/#/bored
[13]: https://github.com/summerscar/impress-blockly
[14]: https://www.imooc.com/article/22786?block_id=tuijian_wz#
[15]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/FE/impress_position.jpg?raw=true