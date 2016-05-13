---
layout: post
title: "结构和类的区别struct and clas"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##结构(struct)与类(class)的区别

##区别： 

 * 默认继承权限。如果不明确指定，来自class的继承按照private继承处理，来自struct的继承按照public继承处理； 
 * 成员的默认访问权限。class的成员默认是private权限，struct默认是public权限。 
除了这两点，class和struct基本就是一个东西。语法上没有任何其它区别。

##相同：

 * 都可以有成员函数；包括各类构造函数，析构函数，重载的运算符，友元类，友元结构，友元函数，虚函数，纯虚函数，静态函数； 
 * 都可以有一大堆public/private/protected修饰符在里边； 
 * 虽然这种风格不再被提倡，但语法上二者都可以使用大括号的方式初始化：A a = {1, 2, 3};不管A是个struct还是个class，前提是这个类/结构足够简单，比如所有的成员都是public的，所有的成员都是简单类型，没有显式声明的构造函数。 
 * 都可以进行复杂的继承甚至多重继承，一个struct可以继承自一个class，反之亦可；一个struct可以同时继承5个class和5个struct，虽然这样做不太好。 
 * 如果说class的设计需要注意OO的原则和风格，那么没任何理由说设计struct就不需要注意。