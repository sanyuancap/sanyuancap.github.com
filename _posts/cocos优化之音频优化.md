# cocos优化之音频优化

## 音频支持格式

cocos creator audio支持三种格式：

    ogg 
    mp3 
    wav

![音频支持格式][5]

## ogg vs mp3 vs wav

 - 音质比较
同音源压缩出来同码率的ogg比mp3音质好，文件大小略小于mp3[参考][2]

WAV最好，其余两个都是有损格式。

 - 大小比较

 256K以上，AAC>OGG>WMA>MP3，256K以下时，OGG>AAC>WMA>MP3。

 - 波形对比

[参考资料][4]
 
 - mp3与ogg
MP3 是比较老的技术，在低码率（128k以下，例如96, 64, 32等）的情况下，MP3 音质会明显弱于 WMA，AAC，OGG 等较新的编码技术。
在高码率（192k 以上）的情况下，各种算法没有明显差距。
[MP3 与 OGG][7]

## 音频常识

码率：(也成位速、比特率)是指在一个数据流中每秒钟能通过的信息量，代表了压缩质量

[参考文档][3]

 - mp3

压缩方法：itunes：
![itunes导出mp3][1]

 - 人耳听到的赫兹范围和音频压缩码率有关系吗？

人耳听到的赫兹范围在20Hz~20kHz之间。
mp3码率小的能到16kHz，大的能到320kHz。

然而两个数据，没有半毛钱关系。![人耳听到的赫兹范围和音频压缩码率有关系吗][6]
一般来说，码率越高，保真率越大，占用空间越大。


[1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-itunes_mp3.png?raw=true
[2]: https://zhidao.baidu.com/question/336451301.html
[3]: https://www.jianshu.com/p/86e1b1017564
[4]: http://www.leawo.cn/space-138176-do-thread-id-58841.html
[5]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-oggvsmp3vswav.png?raw=true
[6]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/cocos-creator/cocos-creator-kHz.png?raw=true
[7]: https://www.zhihu.com/question/20291001/answer/14641612