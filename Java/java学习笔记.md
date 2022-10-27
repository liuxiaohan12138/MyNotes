[TOC]



# 类与对象

## 面向对象简介

java是面向对象语言

## 面向对象设计的三个特征

封装性：内部的操作对外部而言不可见，当内部的操作都不可直接使用的时候才是最安全的；

继承性：在已有结构的基础上继续进行功能的扩充

多态性：类型的转换处理

## 类与对象简介

类是对某一类事物的共性的抽象概念，而对象描述的是一个具体的产物。

类是一个模板，而对象才是类可以使用的实例，先有类再有对象

在类之中一般都会有两个组成：成员属性、操作方法

```java
class Person {
    private String name;
    private int age;
    public void tell(){
        System.out.println(name + "今年已经" + age +"岁了!")
    }
}
```

如果需要类产生对象，使用以下语法格式：

声明并实例化对象： 类名称 对象名称 = new 类名称()



Step 1 声明对象：类名称 对象名称 = null;

Step 2 实例化对象：对象名称 = new 类名称()



调用类中的属性：实例化对象.成员属性

调用类中的方法：实例化对象.方法名称()

## 对象内存分析

堆内存：保存的是对象的具体信息

栈内存：保存的是一块堆内存的地址，即通过地址找到堆内存，而后找到对象内容

## 对象引用分析

同一块堆内存空间被不同的栈内存所指向，也可以更换指向

```java
Person per1 = new Person(); //声明并实例化对象
per1.name = "张三";
per1.age = 18;
Person per2 = per1; //引用传递
per2.age = 80;
per1.tell(); //进行方法的调用
```

## 引用与垃圾产生分析

![image-20221023233220536](pic\image-20221023233220536.png)

所谓的垃圾空间指的就是没有任何栈内存所指向的堆内存空间，所有的垃圾将被GC不定期进行回收并且释放无用内存空间，但是如果垃圾过多，一定将影响到GC的处理性能，从而降低整体的程序性能。实际开发之中，对于垃圾的产生应该越少越好。

一个栈内存只能够保存有一个堆内存的地址数据，如果发生改变，则之前的地址数据将从此栈内存中彻底消失。

## 成员属性封装

设置或取得属性可以使用setXxx()、getXxx()方法

```java
class Person{
    private String name;
    private int age;
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
    public void setName(String n){
        name = n;
    }
    public void setAge(int a){
        age = a;
    }
    public String getName(){
        return name;
    }
    public int getAge(){
        return ages;
    }
}
```

类中的所有属性都必须使用private封装，并且属性进行访问提供setter、getter方法