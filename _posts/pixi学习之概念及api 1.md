# pixi学习之概念及api 1

与cocos对比看，有相似之处，也有不同：

 - 相同:

Sprite、Texture、Text、对齐方式、九宫格、anchor属性、position位置等概念和基本操作。

 - 不同：
 
        1、不是每个类都有anchor，目前支持anchor的只有Sprite、Text、BitmapText等。
        2、坐标系统：左上角是坐标原点，x轴向右是正方向，y轴向下是正方向。
        3、对齐align方式，都支持左对齐、右对齐、居中对齐等。
        4、定时器、动作系统、适配方式不够完善。
        5、没有按钮的定义，按钮需要自己来实现监听，设置interactive和buttonMode等。
