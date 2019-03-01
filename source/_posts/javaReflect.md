title: Java反射机制
date: 2019-3-1 14:00
updated: 2019-3-1 15:00
tags: [Java,反射]
categories: Java
mathjax: true
description: 

# Java反射机制

Java反射机制使程序运行时能动态加载类对象, 并能够获得该类的字段和方法. 对于一些通过多态和动态绑定的程序, 我们可以通过读取配置文件, 再利用Java反射实现的方式来替换.

## 常见应用

- 反射机制常用于框架开发 
- Eclipse等IDE获取类的方法
- 动态代理
- 跳过泛型检查

## 主要操作

1. 获取class, 有三种方式: 

```java
Person p = new Person("cdj", 23);
Class clazz1 = p.getClass();

Class clazz2 = Person.class;
Class clazz = Class.forName("me.forz.javaReflect.path.Person");
```

2. 获取Constructor

```java
// 分两种, 有参和无参
Constructor c1 = clazz.getConstructor(); // 无参构造器
Constructor c2 = clazz.getConstructor(String.class, int.class); // 有参
Person p = (Person) c2.newInstance("constru", 23);
```

3. 获取Field

```java
// 分两种, 是否是private
// Field f = clazz.getField(fieldName);
Field f = clazz.getDeclaredField(fieldName);// Field名称
f.setAccessible(true); //私有字段需要设置此项
f.set(obj, val);
```
4. 获取Method

   同Field, Method也分成是否是private两种, 此处不再赘述. 下面展示一种利用反射跳过泛型检查的例子:

```java
ArrayList<Integer> al = new ArrayList<Integer>();
al.add(1);
al.add(2);
System.out.println(al); //[1, 2]

Class clazz = Class.forName("java.util.ArrayList");
Method m = clazz.getDeclaredMethod("add", Object.class);
m.invoke(al, "a");
System.out.println(al); // [1, 2, a]
```

## 使用

### 动态代理

只能针对接口做代理; 需要实现`InvocationHandler`接口

假设有一个`Fruit`接口, 包含一个`eat()`方法, `FruitImpl`是一个实现

```java
public class Test {
    public static void main(String[] args) {
        FruitImpl fi = new FruitImpl();
        fi.eat();// 输出: eating

        MyInvocationHandler mih = new MyInvocationHandler(fi);
        Fruit f = (Fruit) Proxy.newProxyInstance(fi.getClass().getClassLoader(), fi.getClass().getInterfaces(), mih);
        f.eat(); // 输出 befor\n eating\n after
    }
}
```

```java
public class MyInvocationHandler implements InvocationHandler {
    private Object target;

    public MyInvocationHandler(Object obj) {
        this.target = obj;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("befor");
        method.invoke(target, args);
        System.out.println("after");
        return null;
    }
}
```

