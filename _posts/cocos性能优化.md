(https://blog.csdn.net/u011004567/article/details/79156899)
1. 降低节点复杂度

节点树越复杂刷新的成本越高（也就是节点树的深度尽量浅）。

2. 减少添加和删除节点操作

当前版本的cocos（1.7.2）中的节点树刷新机制是：

节点普通操作（setActive、设置position、rotation）将刷新该节点及其子节点

节点特殊操作（addChild、removeFromParent）将刷新整个节点树。

所以要尽量少使用 node.addChild() 和 node.removeFromParent()操作。

3. 遮盖剔除优化

cocos默认是开启遮盖剔除的，但如果我们项目中的节点结构较为复杂，那么遮盖剔除就会很消耗性能(需要计算多层级的节点位置的累计来判定是否在摄像机的视野中，层级越复杂计算量就越大)。

是否使用cocos自带的遮盖剔除要看实际情况，如果节点结构较为复杂，遮盖剔除消耗大以及节点大小较为容易的等效为一个圆则可以关闭cocos自带的遮盖剔除并可以考虑自己来写一套遮盖剔除，这里等效圆是因为圆与圆之间的关系能够很容易计算（计算两个圆心的距离和圆的半径就可以轻易得出）。

设置遮盖剔除：cc.macro.ENABLE_CULLING = true/false;

设置节点渲染：node._sgNode.visible=true/false;

这里要注意cc.macro.ENABLE_CULLING管理的不包括TiledMap的遮盖剔除。

设置TiledMap遮盖剔除：cc.macro.ENABLE_TILEDMAP_CULLING = true/false;

4. Draw Call
(https://www.jianshu.com/p/f28de1834be2)

1默认字体的每一个label都会产生一个drawcall.所以不能使用默认字体，需要使用bmfont工具制作位图字体。

2修改图片默认颜色会增加drawcall

3图片类型为九宫格会增加drawcall

4修改图片默认透明度会增加drawcall

5默认的纯色图片会增加drawcall

在每次调用Draw Call之前，CPU需要向GPU发送很多内容，包括数据，状态，命令等。在这一阶段，CPU需要完成很多工作，例如检查渲染状态等。而一旦CPU完成了这些准备工作，GPU就可以开始本次的渲染。GPU的渲染能力是很强的，渲染300个和3000个三角网格通常没有什么区别，因此渲染速度往往快于CPU提交命令的速度。如果Draw Call的数量太多，CPU就会把大量时间花费在提交Draw Call命令上，造成CPU的过载。

(https://blog.csdn.net/zzx023/article/details/85319733)
目前creator的自动图集批处理机制为，根据节点renderCmd的顺序，将相邻顺序的所需纹理放入到同一个批次进行处理。实际表现的话大致可以理解为节点树中相邻的节点会进入同一批次。

```
├── node
│   ├── icon
│   ├── label
│   ├── icon

├── node
│   ├── icon
│   ├── icon
│   ├── label
```

渲染buffer必须为MeshBuffer类型的资源才能批处理。可以查看引擎关于各个renderComponent的源码。
像bmfont label和sprite都是MeshBuffer，所以它们可以进入到批处理中。而像9ScaleSprite，Spine这些所使用的为QuadBuffer，因此没办法进行批处理。

|         | bmfont | sprite | 9scalesprite | color | opacity | ttflabel | spine
| :------: | :------: | :------: | :------: | :------: | :------: | :------: | :------: |
| 2.0 | ○ | ○ | x | x | x | x | x |
| 2.1 | ○ | ○ | ○ | ○ | ○ | x | x |

5. 静态资源的内存管理
静态资源指的是场景中直接或间接引用到的所有资源（脚本动态加载的资源不算在内）

在场景资源的属性编辑器中可以勾选“自动释放资源”选项，从而在切换场景时，会自动将旧场景使用的静态资源释放掉，从而节省内存的占用

6. 动态资源的内存管理

7. 引擎裁切

没使用到的引擎功能可以不勾选，以减小发布包中cocos2d-js-min.js的大小

8. 富文本与mask占用drawcall比较多，减少使用。

9. gzip压缩原理
(https://segmentfault.com/a/1190000012571492)
(https://www.cnblogs.com/imgss/p/9348650.html)
(https://www.cnblogs.com/imgss/p/9348650.html)
不是每个浏览器都支持gzip的，如果知道客户端是否支持gzip呢，请求头中有个Accept-Encoding来标识对压缩的支持。客户端http请求头声明浏览器支持的压缩方式，服务端配置启用压缩，压缩的文件类型，压缩方式。当客户端请求到服务端的时候，服务器解析请求头，如果客户端支持gzip压缩，响应时对请求的资源进行压缩并返回给客户端，浏览器按照自己的方式解析，在http响应头，我们可以看到content-encoding:gzip，这是指服务端使用了gzip的压缩方式。




