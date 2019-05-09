---
title: 设计模式
date: 2019-03-16 15:00
updated: 2019-03-16 16:00
tags: [设计模式,Java,C++]
categories: 设计模式
mathjax: true
description: 
---
常见设计模式 C++/Java实现
<!--more-->

# 创建型模式

## 单例模式

单例模式创建有三个步骤, 

- 将构造函数私有化, 防止程序创建其他实例化对象
- 创建**静态**和**私有**的实例化对象, 注意: 在C++中, 非常量的静态对象需要在外部初始化, 以保证每个静态成员变量只被定义一次
- 创建公有的实例化对象获取函数

下述代码是基于C++的实现的**饿汉式**单例模式

```c++
class Test {
public:
    static Test *getInst () {
        return t;
    }

private:
    Test () {};
    static Test *t;
};
Test* Test::t = new Test();
```

