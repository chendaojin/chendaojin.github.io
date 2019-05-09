---
title: Java自己实现枚举
date: 2019-3-2 14:00
updated: 2019-3-2 15:00
tags: [Java,Enum]
categories: Java
mathjax: true
description: 
---

# Java枚举实现

枚举的实现类似于单例模式, 本文从无参构造, 有参构造和包含抽象方法的三种情况

<!--more-->

## 无参构造

```java
public class Month {
    public static final Month Jan = new Month();

    private Month() {}
}
```

## 有参构造

```java
public class Month_1 {
    public static final Month_1 Jan = new Month_1("一月");
    private String name;
    private Month_1(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

## 包含抽象方法

```java
public abstract class Month_2 {
    public static final Month_2 Jan = new Month_2("一月") {
        @Override
        public void show() {
            System.out.println("Moth_2 一月");
        }
    };
    private String name;

    private Month_2(String name) {
        this.name = name;
    }

    public abstract void show();
}
```

