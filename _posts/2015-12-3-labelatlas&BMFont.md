


//造字 glyphDesigner bmfont
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


        this._btn_pop.hitTest(cc.p(1,1));