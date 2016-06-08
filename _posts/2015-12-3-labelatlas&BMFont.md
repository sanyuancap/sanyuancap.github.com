---
layout: post
title: "cocos2d-js学习之创建位图字体"
description: ""
category: cocos2d-js
tags: [位图字体]
---
{% include JB/setup %}


有了glyphDesigner之后，创建位图字体的过程相对轻松，试着调节GlyphDesigner中各种旋钮、按钮和颜色可以看到不同效果。对位图字体感到满意后，可以保存整个项目，以便能够还原原来的设置。

![截图][1]
  
为了以cocos2d可用的格式保存字体，需要通过`File | Export以.fnt(cocos2d Text)`格式保存它。然后可以在Xcode项目中添加使用GlyphDesigner创建的FNT和PNG文件，并在CCLabelBMFont类中使用FNT文件。


        this.lbScore = new cc.LabelBMFont("Score: 0", res.arial_14_fnt);
        this.lbScore.attr({
            anchorX: 1,
            anchorY: 0,
            x: this._visibleSize.width / 2,
            y: this._visibleSize.height / 2,
            scale: 1
        });
        this.lbScore.textAlign = cc.TEXT_ALIGNMENT_RIGHT;
        this.addChild(this.lbScore, 1000);
        self.lbScore.setString(55648);
        
        //图片文字 labelatlas
        var label1 = new cc.LabelAtlas("0123456789", res.s_fnTuffyBoldItalicCharmapPng, 48, 64, ' ');
        self.addChild(label1,999999);
        label1.setString("798798798798");
        label1.x = 300;
        label1.y = 300;

ps：如果使用CCLabelBMFont显示.fnt，文件中不可用的字符，这些字符将被跳过，不会显示出来。例如，如果使用语句[label setString:@"Hello, World!"]，但是位图字体中只包含小写字母，不包括标点符号字符，那么显示的将是字符串"ello orld"。

[参考资料][2]

  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/glyphDesigner.jpg?raw=true
  [2]: http://book.2cto.com/201210/6610.html
