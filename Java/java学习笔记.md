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

## 构造方法与匿名对象

```java
public class Person {
    public String name; // 姓名
    public int age; // 年龄

    // 定义构造方法，为属性初始化
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 获取信息的方法
    public void tell() {
        System.out.println("姓名：" + name + "，年龄：" + age);
    }

    public static void main(String[] args) {
        new Person("张三", 30).tell(); // 匿名对象
    }
}
```

# this

当前类中的属性：this.属性

当前类中的方法（普通方法、构造方法）：this()    this.方法名称()

描述当前对象：使用this调用当前类中的属性



对于简单java类而言，其核心的开发结构如下：

类名称一定要有意义，可以明确的描述某一类事物；

类之中的所有属性都必须使用private进行封装，同时封装后的属性必须提供setter getter方法

类之中可以提供有无数多个构造方法，但是必须要保留有无参构造方法

类之中不允许出现任何的输出语句，所有内容的获取必须返回



# static

在一个类之中，所有的属性一旦定义了实际上内容都交由各自的堆内存空间所保存。

```java
class Person{
    private String name;
    private int age;
    String country = "中华民国";
    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
    public String getInfo(){
        return this.name + this.age  + this.country
    }
}

public class JavaDemo {
    public static void main(String args[]){
        Person perA = new Person("张三"， 10);
        Person perB = new Person("李四"， 10);
        Person perC = new Person("王五"， 11);
        perA.country = "中华人民共和国";
        //只有perA的country改变
    }
}

class Person{
    private String name;
    private int age;
    // 公共属性
    static String country = "中华民国";
    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
    public String getInfo(){
        return this.name + this.age  + this.country
    }
}

public class JavaDemo {
    public static void main(String args[]){
        Person perA = new Person("张三"， 10);
        Person perB = new Person("李四"， 10);
        Person perC = new Person("王五"， 11);
        perA.country = "中华人民共和国";
        //所有对象中的country都发生改变
    }
}
```



static方法只允许调用static属性或static方法

非static方法允许调用static属性或static方法

# 数组的定义与使用

数组的动态初始化：

​	声明并初始化数组：

​		数据类型 数组名称[] =  new 数据类型[长度];

​		数据类型[] 数组名称 =  new 数据类型[长度];

数组的静态初始化：在数组定义的时候就为其设置好了里面的内容

​	数据类型 数组名称[] = {数据1，数据2，数据3};

​	数据类型 数组名称[] = new 数据类型[] {数据1，数据2，数据3};

![image-20221114224056349](pic\image-20221114224056349.png)

## 二维数组

数组的动态初始化：

​	数据类型 数组名称[ ] [ ]= new 数据类型[行个数] [列个数];

数组的静态初始化：在数组定义的时候就为其设置好了里面的内容

​	数据类型 数组名称[] = {数据1，数据2，数据3};

​	数据类型 数组名称[] = new 数据类型[ ] [ ] {{数据，数据，...},{数据，数据，...},{数据，数据，...}};

## 数组排序

```java
int data[] = new int[]{8,9,0,2,3,5,10,7,6,1};
for(int j=0; j < data.length - j; j++) {
    // 最后一个一定是最大的数，所以-j
    for(int i=0; i < data.length - j - 1; i++) {
        if (data[i] > data[i+1]) {
            int temp = data[i];
            data[i] = data[i+1];
            data[i+1] = temp;
        }
	}
}
```

## 数组转置

```java
// 逆序
int data[] = new int[] {1,2,3,4,5,6,7,8,9};

// 方法1
int result[] = new int[data.length];
int index = result.length-1;
for(int i=0; i < data.length; i++){
    result[index--] = data[i];
}
data = result;

// 方法2
int count = data.length / 2;
int head = 0;
int tail = data.length - 1;
for(int i=0; i<data.count; i++) {
    int temp = data[head];
    data[head] = data[tail];
    data[tail] = temp;
    head ++;
    tail --;
}
```

方法1循环次数较多，产生垃圾；方法2时间复杂度较低，提升性能

## 数组相关类库

数组排序：java.util.Arrays.sort(data)

数组拷贝：System.arraycopy(源数组，源数组开始点，目标数组，目标数组开始点，拷贝长度)

## 方法可变参数

int ...data 本质是数组

## 对象数组

动态初始化：类 对象数组名称[] = new 类[长度]，每一个元素的内容都是null

静态初始化：类 对象数组名称[] = new 类[]｛实例化对象，实例化对象，...｝

缺陷：长度是固定的

优势：数据线性保存，根据索引访问，速度较快（时间复杂度为1）



# String类特点分析

## 字符串比较

```
String A = "A";
String B = "B";
A.equals(B);
```

==是数值比较，比较的是两个内存的地址数值；

equals()可以直接进行字符串内容的判断。

将字符串的常量写在前面可以回避空的判断："A".euqals(A);

## String类实例化

String A = "ABCD";

在采用直接赋值的处理过程中，字符串可以实现池数据的自动保存，再有相同的数据定义时可以减少对象的产生，提升操作性能.



String str = new String("wdwd");

采用构造方法实例化String类对象时不会自动保存到池数据中

## String对象常量池

静态常量池：指的是程序(*.class)在加载的时候会自动讲此程序之中保存的字符串、普通的常量、类和方法的信息等等，全部进行分配

运行时常量池：当一个程序(*.class)加载之后，里面可能有一些变量，这个时候提供的常量池



# 继承

## 继承的实现

class 子类 extends 父类{}

## 子类对象实例化流程

即使没有进行父类对象实例化，也会由系统自动调用父类的构造方法，自动化实例化父对象



# 重写

优化父类的功能

```
class Channel{
	public void connect(){
		return "dad";
	}
}

class DatabaseChannel extends Channel{
	public void connect(){
		return "son";
	}
}
```

属性覆盖无法进行子类覆盖父类中的私有属性

final：定义不能被继承的类，不能被复写的方法、属性



# 多态

## 方法的多态

```
pubilc void print(){
	System.out.println("print");
}

pubilc void print(String str){
	System.out.println("print:" + str);
}
```

## 对象向上转型

```
class Message{
	public void print(){
		System.our.println("连接");
	}
}

class DataBaseMessage extend Message{
	public void print(){
		System.our.println("数据库连接");
	}
}

public class JavaDemo{
	public static void main(String[] args){
		Message msg = new DataBaseMessage();
		msg.print();
	}
}
```

## 对象向下转型

```
class Message{
	public void print(){
		System.our.println("连接");
	}
}

class DataBaseMessage extend Message{
	public void print(){
		System.our.println("数据库连接");
	}
}

public class JavaDemo{
	public static void main(String[] args){
		// 向上转型
		Message msg = new DataBaseMessage();
		msg.print();
		// 向下转型
		DataBaseMessage dmsg = (DataBaseMessage) msg;
	}
}
```

## instanceof关键字

判断某个实例是否是某个类的对象

对象 instanceof 类



# Object类

不能有继承关系

equals可以进行所有类型比较



## 抽象类的定义与使用

抽象类的主要作用在于对子类中覆盖写法进行约定，在抽象类里面可以去定义一些一些抽象方法。抽象方法的是使用了abstract关键字定义的并且没有提供方法体的方法，而抽象方法所在的类必须为抽象类，抽象类必须使用abstract关键字来定义。



```java
abstract class Message{
	private String type;
    public abstract String getConnectInfo();
}
```



相关说明

1.在定义抽象类的时候绝对不能使用final关键字来进行定义，抽象类必须有子类，final定义的类没有子类

2.抽象类是作为一个普通类的加强版出现的（抽象类的组成就是在普通类的基础上扩展而来的，只是追加了抽象方法）

3.抽象类中允许没有抽象方法，但是即使没有抽象方法，也无法直接使用关键字new实例化抽象类对象

4.抽象类中可以提供有static方法，并且该方法不受到抽象类对象的局限。



## 包装类

```java
class Int{
    private int data;
    public Int(int data){
        this.data=data;
    }
    public int intValue(){
        return this.data;
    }
}

public class demo{
    public static void main(String args[]){
        // 装箱：将基本数据类型保存在包装类中
        Int temp = new Int(10);
        // 拆箱：从包装类对象中获取基本数据
        int x = temp.intValue();
    }
}
```

