
var pFrame = cc.spriteFrameCache.getSpriteFrame("explosion_01.png");
 // explosion batch node
cc.spriteFrameCache.addSpriteFrames(res.explosion_plist);
var explosionTexture = cc.textureCache.addImage(res.explosion_png);
this._explosions = new cc.SpriteBatchNode(explosionTexture);
this._explosions.setBlendFunc(cc.SRC_ALPHA, cc.ONE);
this.addChild(this._explosions);


