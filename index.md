---
layout: page
title: 来自艾泽拉斯的一封密码信!
tagline: Life is but a span.
---
{% include JB/setup %}


上周收到网易云信的“密码信”，信说解密正确可以获得魔兽手办。我不玩魔兽，但是我家那位是十年的魔兽玩家，曾经为了解锁炉石马，拉着我玩炉石……不如研究一下解密，人品好兴许弄个手办带回家。
闲话不多说，直接记录一下解密过程。答案在文章中。

线索一：对称加密
----

![对称加密][1]

 - 头脑风暴：什么是对称加密？
一句话回答：**同一秘钥**加密解密。
 
> 采用单钥密码系统的加密方法，同一个密钥可以同时用作信息的加密和解密，这种加密方法称为对称加密，也称为单密钥加密。

 - 头脑风暴：“对称加密”解决的切入点？
一句话回答：找到**秘钥**！

> 加密的安全性不仅取决于加密算法本身，密钥管理的安全性更是重要。因为加密和解密都使用同一个密钥，如何把密钥安全地传递到解密者手上就成了必须要解决的问题。

> 比如甲乙约定，一起买一个保险箱，保存金银财宝，共用一个钥匙。只要甲乙小心保管好钥匙，那么就算有人得到保险盒，也无法打开。可是一旦获取钥匙，就很可能拿到财宝。



线索二：八皇后
-------

![八皇后][2]

 - 头脑风暴：八皇后是什么？
一句话回答：关于棋子**摆放位置**的解

> 八皇后问题是十九世纪著名数学家高斯于1850年提出的。

> 问题是：在8*8的棋盘上摆放8个皇后，使其不能互相攻击，即任意的两个皇后不能处在同一行，同一列，或同一斜线上。
。

- 头脑风暴：摆放位置都有哪些？
一句话回答：解有**92组**，但是不知道哪一个才是正解。

> 对于某个满足要求的8皇后的摆放方法，定义一个皇后串a与之对应，即a=b1b2...b8，其中bi为相应摆法中第i行皇后所处的列数。
> 例如：15863724，代表皇后分别在第一行第一列，第二行第五列……第八行第4列等。


线索三：已知1月、2月的秘钥，求5月秘钥
----

![秘钥][3]


- 头脑风暴：从1月秘钥可以看出，皇后分别放在（15863724）第一行第一列，第二行第五列……第八行第四列；从2月秘钥可以看出，皇后分别放在（16837425）第一行第一列，第二行第六列……第八行第五列。
所以输入是按照1-8的**升序排列**。
一句话回答：升序排列，5月秘钥是24683175

![秘钥排列][4]

> 八皇后是一个古老的具有代表性的问题，用计算机求解时的算法也很多，最容易想到的是回溯法，采用一维数组来进行处理。数组的下标i表示棋盘上的第i行，a[i]的值表示皇后在第i行所放的位置。

下面引用一下C++版本的回溯法核心算法，具体算法请参考文章结尾链接。

    while(not_finish) /*not_finish=1:处理尚未结束*/ {
            while(not_finish && i <= NUM) /*处理尚未结束且还没处理到第NUM个元素*/ {
                for(flag = 1,k = 1;flag && k < i;k++) /*判断是否有多个皇后在同一行*/
                    if(a[k] == a[i]) flag = 0;
                for(k = 1;flag && k < i;k++) /*判断是否有多个皇后在同一对角线*/
                    if((a[i] == a[k] - (k - i)) || (a[i] == a[k] + (k - i))) flag = 0;
                if(!flag) /*若存在矛盾不满足要求，需要重新设置第i个元素*/ {
                    if(a[i] == a[i - 1]) /*若a[i]的值已经经过一圈追上a[i-1]的值*/ {
                        i--; /*退回一步，重新试探处理前一个元素*/
                        if(i > 1 && a[i] == NUM)
                            a[i] = 1; /*当a[i]为NUM时将a[i]的值置1*/
                        else if(i == 1 && a[i] == NUM)
                            not_finish = 0; /*当第一位的值达到NUM时结束*/
                        else a[i]++; /*将a[i]的值取下一个值*/
                    }
                    else if(a[i] == NUM) a[i] = 1;
                    else a[i]++; /*将a[i]的值取下一个值*/
                }
                else if(++i <= NUM)
                    if(a[i - 1] == NUM) a[i] = 1; /*若前一个元素的值为NUM则a[i]=1*/
                    else a[i] = a[i - 1] + 1; /*否则元素的值为前一个元素的下一个值*/
            }
            if(not_finish) {
                ++count;
                printf((count - 1) % 3 ? " [%2d]: " : " [%2d]: ",count);
                for(k = 1;k <= NUM;k++) /*输出结果*/
                    printf(" %d",a[k]);
                if(a[NUM - 1] < NUM) a[NUM - 1]++; /*修改倒数第二位的值*/
                else a[NUM - 1] = 1;
                i = NUM - 1; /*开始寻找下一个足条件的解*/
            }
    }



其实八皇后问题早都列入了小学奥数，是的，母亲大人曾给我买过一本崭新的奥数竞赛题，我略过一眼。说到严蔚敏的C++算法，也有八皇后的一席之地。所以对于程序猿来说，解题应该不是难事。况且，网络上搜索八皇后，各种java、js、C++等的解法都是现成的。

在这些算法当中，我发现了几个特立独行的，其中一个是**位算法**，是10年前匿名的大神写的。简单的看了一下算法原理，它有别于传统的数组判断模式，非常效率，至少让我长见识了。我在这里只引用核心算法，具体算法可以看文章后面的参考链接。
        
    void test(long row,long ld,long rd)
    {
        if(row != upperlim) {
            long pos = upperlim & ~(row | ld | rd);
            while(pos) {
                long p = pos & -pos;
                pos -= p;
                test(row + p,(ld + p) << 1,(rd + p) >> 1);
            }
        } else
            sum++;
    }
    

线索四：get破译工具
---------------------

![网易云信][5]

- 头脑风暴：怎么知道是哪种加密算法呢？
一句话回答：关注公众平台试试

虽然已知是对称加密，可是对称加密的种类很多，比如说CryptoJS(crypto.js)为JavaScript提供了各种各样的对称加密算法。目前已支持的常见算法包括：DES、TripleDes、AES、RC4、Rabbit等。再比如说Java版本的AES加密和JS版本的加密有区别，原因在于算法的占位方法实现不同。具体的不同参考文章末尾的链接。

![公众平台][6]

没有头绪的时候，随手关注了下**公众平台**，竟然get到了破译工具。幸福来得太突然了，离真相只差一步了！

![破译工具][7]

好吧，一个一个试吧，把密文复制进文本框，点击解密，竟然第一次就成功了。

> 来自艾泽拉斯的密码信传递的答案是： 网易云信请万人看魔兽电影

撒花！撒花！撒花！

总结
--
- AES

既然答案是是**AES**加密，那我就稍微了解下这个技术吧。

> AES（The Advanced Encryption
> 　Standard）是美国国家标准与技术研究所用于加密电子数据的规范。它被预期能成为人们公认的加密包括金融、电信和政府数字信息的方法。
近些年DES使用越来越少，原因就在于其使用56位密钥，比较容易被破解，逐渐被AES替代，AES已经变成目前对称加密中最流行算法之一。

**CryptoJS**是一个纯**javascript**写的加密类库，我们使用它只需要加入相关的引用即可：

     <script type="text/javascript" src= "http://www.osctools.net/js/CryptoJS/components/core-min.js" > 
    </script>
    < script type= "text/javascript" src= "http://www.osctools.net/js/CryptoJS/rollups/aes.js" > 
    </script>
    < script type= "text/javascript" >
        var pwd = "我的密码";
        var mi = CryptoJS.AES.encrypt("你好，欢迎来到开源中国在线工具，这是一个AES加密测试",pwd);   
        alert("你好，欢迎来到开源中国在线工具，这是一个AES加密测试----密文:" + mi);    
        var result = CryptoJS.AES.decrypt(mi,pwd).toString(CryptoJS.enc.Utf8);    
        alert("解密结果：" + result);
    </script>

 - 捎带脚说一下**base64**

提到CryptoJS，其实我先想到的是base64。base64主要不是加密，它主要的用途是把某些二进制数转成普通字符用于网络传输。

工作原理大概是：`canvas.toDataURL()`首先把图像转成PNG数据，然后再把得到的二进制的PNG数据转成纯ASCII的base64编码的字符串。由于这些二进制字符在传输协议中属于控制字符，不能直接传送，所以需要转换一下，这就用到了base64。


> 图片的下载始终都要向服务器发出请求，但是base64可以让图片的下载不用向服务器发出请求，而是随着 HTML的下载同时下载到本地。
base64最有用的一点是解决了跨域问题。

 - 我想要手办，我想要手办，我想要手办！

听说网易云信的Amao仅用1分钟就撸开了这段密文，感叹大神无处不在。我肯定进不了解题前3名了，凑个热闹拼人品吧。大不了给你们当分母，我也不吃亏，至少学到了加密解密的各种方法。
 


参考资料：
-----

 - [八皇后问题][8]
 - [八皇后位算法][9]
 - [八皇后C++算法][10]
 - [Crypto-JS首页][11]
 - [AES加密算法][12]
 - [AES动态演示][13]
 - [Base64编码][14]
 - [在线加密解决工具][15]



----------


**to网易云信的小伙伴：感谢你们这一次寓教于乐的创意，让我学到了很多东西，我很喜欢你们的产品。本文只是个人观点，如有雷同，不胜荣幸。本文不代表官方立场。我特意在31号发文，就是不想跟你们的活动造成影响。如果造成了困扰，我深表歉意。如需修改或删文，请联系sanyuancap@foxmail.com。**


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/2.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/4.gif?raw=true
  [3]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/1.png?raw=true
  [4]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/3.png?raw=true
  [5]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/6.png?raw=true
  [6]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/7.jpg?raw=true
  [7]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/WOW/5.png?raw=true
  [8]: http://www.kuqin.com/tiku/20080424/7621.html
  [9]: http://bbs.csdn.net/topics/80489768
  [10]: http://blog.csdn.net/justme0/article/details/7540425
  [11]: http://www.oschina.net/p/crypto-js?fromerr=5I2QL6Zf
  [12]: http://blog.csdn.net/searchsun/article/details/2516191
  [13]: http://coolshell.cn/wp-content/uploads/2010/10/rijndael_ingles2004.swf
  [14]: http://www.tuicool.com/articles/IbYJvin
  [15]: http://tool.oschina.net/encrypt


----------

## 文章列表


<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


