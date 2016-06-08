---
layout: post
title: "c++箭头和点和双冒号操作符"
description: ""
category: C++
tags: []
---
{% include JB/setup %}

    class PS { 
        public: 
        int ca_var; 
        int add(int a, int b); 
        int add(int a); 
    };
    PS *p;
    p是指针,p->function();
    PS p;
    p是对象,p.function();


双冒号::只用在类成员函数和类成员变量中，例如在实现这个函数时，必须这样书写：

    int CA::add(int a, int b) 
    { 
        return a + b; 
    }

另外，双冒号也常常用于在类变量内部作为当前类实例的元素进行表示，比如:

    int CA::add(int a) 
    { 
        return a + ::ca_var; 
    }

