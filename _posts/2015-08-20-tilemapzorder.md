---
layout: post
title: "cocos2d-lua学习之tilemapZorder"
description: ""
category: cocos2d-lua
tags: [cocos2d-lua]
---
{% include JB/setup %}

cocos2d-lua学习之tilemapZorder
============

## 设置障碍物

	bool HelloWorld::isPositionBlock(CCPoint position)
	{
	     CCPoint tileCoord = this->tileCoordForPosition(position);
	     int tileGid = _metaLayer->tileGIDAt(tileCoord);
	     
	     CCDictionary *properties = _tileMap->propertiesForGID(tileGid);
	     
	     if (properties)
	     {
	         CCString* collision = const_cast<CCString*>(properties->valueForKey("block"));
	         
	         if ( 0 == strcmp(collision->getCString(), "true") )
	         {
	             return true;
	         }
	     }
	     
	     return false;
	}

## Zorder实现原理

  * 在tilemap编辑器中新建多个对象层或者图形层
  * 在游戏场景中监听主角Y坐标
  * 比对层级Y坐标位置，reorder主角
