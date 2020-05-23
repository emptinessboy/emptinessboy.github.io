---
title: Java 异常处理（转）
date: 2020-04-21 13:37:20
category: JAVA学习
tags: java
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/02/26/java.jpg
---

> 本文转载自 CSDN 泰斗贤若如 这位dalao
> 
> 这篇文章将异常处理讲解的很细致，作为学习资料，在此收藏了！

## 异常的简介

在 Java 中，异常就是 Java 在编译、运行或运行过程中出现的错误。

### 产生异常原因

程序错误分为三种：编译错误、运行时错误和逻辑错误

1. 编译错误：因为程序没有遵循语法规则，编译程序能够自己发现并且提示我们错误的原因和位置，这个也是新手在刚接触编程语言时经常遇到的问题。

2. 运行时错：因为程序在执行时，运行环境发现了不能执行的操作。如除零

3. 逻辑错误：因为程序没有按照预期的逻辑顺序执行。异常也就是指程序运行时发生错误，而异常处理就是对这些错误进行处理和控制。

下面看一段代码：

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(1/0);    //0不能做除数
    }
}
```

运行后的结果为：

[![1.png](https://media.everdo.cn/tank/pic-bed/2020/04/21/1.png)](https://up.media.everdo.cn/image/IbaL)

我们发现程序出了错，而图中的错误信息告诉我们两个信息：

出了什么错 / 出错的位置

### 异常产生的过程

以上面的代码为例，程序在运行过程中，先运行 main 方法，然后执行到 1/0 时，程序就会报错，程序先会创建一个错误对象，然后把这个错误对象丢出来，我们都知道我们的程序是运行在 Java 虚拟机 (JVM) 上，程序丢出来的错误对象就会被 JVM 捕获到。当然，JVM 捕获到错误对象后，它也不知道该怎么办，它不可能帮你调错，JVM 会把错误信息给你打印出来。

总结：

- 上例中出现的异常是运行时异常（异常是错误）
- 程序会创建一个错误对象，然后把错误对象丢出来（抛异常）
- 默认由JVM把错误信息进行捕获，打印出来（捕获异常）

<br>

### 为什么不能直接让JVM获取异常

> 答：会造成程序中断

先看下面代码：

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(1/0);    //0不能做除数
        System.out.println("你好");
    }
}
```

[![2.png](https://media.everdo.cn/tank/pic-bed/2020/04/21/2.png)](https://up.media.everdo.cn/image/IeAc)

从上面代码和运行结果中，我们不难看出在控制台没有打印出你好。出现这种情况，是因为在 JVM 捕获到异常后，程序会终止。换句话说，在由 JVM 来处理错误的时候，此时，程序会终止，因此异常之后的代码就无法运行了。我们可以根据生活实例想想，什么时候百度会因为搜不到东西停服务，肯定是不会的，因此我们后面要做的就是如何在异常到达JVM之前把异常拦下来，自己单独处理，就不要麻烦 JVM 了。

### 异常的分类

在上面实例中我说过程序会创建错误对象，说到对象，我们都知道对象是由类创建的，那异常对象肯定是通过异常类来创建的。下面图中就是 Java 给我们提供的异常类：

[![3.png](https://media.everdo.cn/tank/pic-bed/2020/04/21/3.png)](https://up.media.everdo.cn/image/Iic2)

从图中我们能看出 Throwable 是所有异常的根，所有的异常类都继承自 Throwable，就像面向对象里面所有的类都继承自 Object。

下面我来说一下异常的分类：

- RuntimeException：运行时异常，一般不手动处理，出问题了再处理。
- 其他Exception：必须要经过手动处理。
- Error：一般指的是系统级错误。

我再用生活例子解释一下这三种异常，便于新手理解：

假设我们现在开车上山，开车的过程中发现山上有许多小石头，但我们不可能把所有小石头都处理了，这时候我们依旧正常开，什么时候小石头把车胎给弄坏了，我们再下来，换备胎，这就是 运行时异常

开车的过程中发现前面有一个很大的石头挡住了路，这时候你必须下车先把这石头挪走，你才能继续上山，这也就是 其他Exception。

开车上山的过程中山塌陷了，你又无法处理，必须要等到山好了你才能继续出发，也就是 Error，就是这种错误我们一般的程序员是处理不了的。

## 异常的处理方法

### try···catch处理

语法：

```java
try{
    //尝试执行的代码
        }catch(Exception e){
    //处理异常的代码
        }finally{
    //最终的
}
```

下面我将文中案例进行改造：

```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println(1/0);
            //0不能做除数
        }catch (Exception e){
            e.printStackTrace();
            //打印错误信息，给程序员看的
            System.out.println("系统出现错误，请联系管理员");
            //给客户看的
        }finally {
            //一般做收尾工作
            System.out.println("你好");
        }

    }
}
```

运行结果：

[![a.png](https://media.everdo.cn/tank/pic-bed/2020/04/21/a.png)](https://up.media.everdo.cn/image/IWSt)

其中：

try： 用于监听。将要被监听的代码(可能抛出异常的代码)放在 try 语句块之内，当 try 语句块内发生异常时，异常就被抛出。

catch： 用于捕获异常。catch 用来捕获 try 语句块中发生的异常。

finally： finally 语句块总是会被执行。它主要用于回收在 try 块里打开的物力资源(如数据库连接、网络连接和磁盘文件)。

### throws 和 throw处理

- throws 表示方法准备要扔出来一个异常
- throw 表示向外抛出异常

举例说明：

```java
public class Test1 {
    public static void chu(int a,int b) throws Exception{
        if (b==0){
            throw new Exception("除数不能为0");
        }else {
            System.out.println(a/b);
        }
    }

    public static void main(String[] args) throws Exception{
        chu(1,0);
    }
}
```
[![4.png](https://media.everdo.cn/tank/pic-bed/2020/04/21/4.png)](https://up.media.everdo.cn/image/IrZZ)

以上这两种方法都是处理异常的，如果这个异常你可以处理，就用 try···catch 方法捕获并处理异常，如果这个异常你不能处理，就用 throws 方法抛出异常，但作为程序员的我们要始终记住一句话：**产生的错误尽可能的自己处理，少向外抛出异常。**

### 自定义异常

到这可能有的朋友要问了，为什么要自定义异常，Java 给的那么多还不够用吗？我可以告诉你，当然不够用，比如在生活中，我们都知道外面的澡堂子里边是分男女澡堂的，如果有男顾客走进了女澡堂或有女顾客走进了男澡堂，就坏事了，这算是一个大异常吧，那大家想，jdk 会给我们提供跟性别还有澡堂子有关的异常吗？肯定是不可能的，那此时就需要我们自定义异常。我以澡堂子为例，写一个程序，供大家参考。

> 我的解读是，有些东西在系统看来不属于异常，但对我们程序逻辑来说是有问题的，这个没法用系统自动捕获抛出

**自定义异常：直接继承 Exception 或者 RuntimeException 来是实现自定义异常**

Person 类：

```java
public class Person {
    String name;//姓名
    String gender;//性别

    public Person(String name, String gender) {
        this.name = name;
        this.gender = gender;
    }
}
```

ZaoTangZi 类:

```java
public class ZaoTangZi {
    public void man(Person p) throws GenderException{
        if (p.gender=="男"){
            System.out.println("欢迎光临");
        }else {
            //需要抛出一个异常
            throw new GenderException("性别错误，这里是男澡堂子");
        }
    }
}
```
GenderException 类:

```java
public class GenderException extends Exception{
    //自己定义的异常必须要继承Exception或RuntimeException

    public GenderException(String msg){
        super(msg);//调用父类的构造方法，Exception(msg)
    }
}
```

Test 类:

```java
public class Test {
    public static void main(String[] args) throws GenderException{
        Person p1 = new Person("张三","男");
        Person p2 = new Person("小花","女");

        ZaoTangZi z = new ZaoTangZi();
        z.man(p2);
    }
}
```

运行结果：

[![b.png](https://media.everdo.cn/tank/pic-bed/2020/04/21/b.png)](https://up.media.everdo.cn/image/INPx)

文末，我们应该明白以下几个问题：什么是异常，出现异常如何处理，如何自定义异常。
