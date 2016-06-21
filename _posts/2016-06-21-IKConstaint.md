---
layout: post
title: "Egret学习之IK约束"
description: ""
category: Egret
tags: [Egret]
---
{% include JB/setup %}


IK是反向动力学`Inverse Kinematics`的缩写，FK为正向动力学的缩写。DragonBones Pro 从 4.5.0 开始支持IK约束功能。通常情况下，父骨骼带动子骨骼运动即为正向动力学FK。例如，大臂带动小臂，大腿带动小腿。IK与FK相反，用来实现由下而上的驱动。例如，做俯卧撑时，手撑住地面，支起身体，骑单车等。

![didanche][1]


 - IK约束的特性：

 1. 绑定了IK约束的骨骼外框显示为红色 
 2. 作为IK约束目标的骨骼整体显示为红色 
 3. 单根骨骼可以绑定IK约束 
 4. 两根连续父子骨骼可以绑定IK约束
 5. 两个以上骨骼无法绑定IK约束 
 6. 非连续父子骨骼无法绑定IK约束 
 7. 非父子骨骼无法绑定IK约束
 8. 所选骨骼的直接或间接子骨骼不能手动指定为IK约束目标骨骼
 9. 关闭“旋转”继承的骨骼无法绑定IK约束
 10. 绑定了Ik约束的骨骼不能关闭“旋转”继承


 - 添加IK约束

添加IK约束需要在DragonBonesPro软件中操作。选中骨骼后在属性面板可以看到两个IK约束按钮，点击便可创建IK约束。

![ruanjian][2]

![ruanjian2][3]


  [1]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/IK.png?raw=true
  [2]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/IK2.png?raw=true
  [3]: https://github.com/sanyuancap/sanyuancap.github.com/blob/master/assets/blogImg/egret1/IK3.png?raw=true