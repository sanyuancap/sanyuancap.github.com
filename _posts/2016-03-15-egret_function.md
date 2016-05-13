---
layout: post
title: "new post"
description: ""
category: 
tags: []
---
{% include JB/setup %}


new common.Loading(Modules.HOME, this.createScene, this);

module common {
    export class Loading {

		public constructor(groupName: string, complete: () => void, container:egret.DisplayObjectContainer) {}

}

complete: () => void
函数命名方式