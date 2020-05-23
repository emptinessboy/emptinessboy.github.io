---
title: Python 学习笔记01（基本语法）
date: 2020-04-24 15:36:12
category: python入门
tags: python
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/24/python-pic.jpg
---

> ！Python 程序各行开头的空白区称为缩进，这在 Python 中非常重要，Python 使用缩进来确定各行的级别和分组。处于同一级别的语句行的缩进必须是一致的。

## 注释

Python 的单行注释以 **#** 井号 开头，注释从井号开始到行结束的所有字符。多行注释使用三个单引号 **'''注释内容'''** 来进行标记。

## 标识符

标识符是为了给例如变量、函数这些对象命名，命名标识符的规则如下：

- 第一个字符为字母表中的字母或下划线
- 其他字符可包括字母、数字或下划线
- 标识符区分大小写
- 命名标识符不要和 Python 保留字同名

## 变量及赋值

Python 中的变量不需要显示声明，当对一个变量名第一次赋值的时候，就是它被创建的时候。

```python
a = b = z = 1
Python 中给多个变量同时赋值的方法：
a, b, c = 1, 2, 3
Python 中交换两个变量的方法：
a, b = b, a
```

可以通过 type() 查看变量数据类型，id() 可以输出变量地址。**Python变量名只是Python对象的标签，其本质是地址引用。对于小整数，系统已经预先分配内存空间。**

> 内置函数可以被我们覆盖！！
> 
> 如 ```sum([1,2,3])``` 的输出为 6，而如果我们给 sum 赋值 ```sum = 1```
> 
> 那么这时 sum 的函数功能就失效了
> 
> 若要恢复，则需要 ```del(sum)```

## 输入

input 函数的作用是从键盘输入得到一个字符串并返回

input 函数可以无参数（小括号里为空），也可以给出提示性的文本，该文本会在运行的时候首先输出。**input 函数的返回必然是一个字符串。**

**方式一：** 可以使用 eval() 函数将用户输入的数字字符串转换成数字。eval 函数的作用是执行一个字符串表达式，并返回这个表达式的值。

**方式二：** 强制类型转换 使用 int() 函数可以强制转换为整型

### 直接切割输入

```python
x1,y1 = eval(input("请输入x1,y1坐标："))
a,b,c = eval(input())
```

### split 对输入进行切割

```python
# a,b以斜线分割输入
a,b = input().split("/")
# 强制类型转换需要使用 map 映射
a,b,c=map(int,input().split(" "))
```

##  print 函数

print 是一个 Python 的内置函数，它的作用是输出一个或者多个对象的文本表示。print 默认向交互窗口输出。

```python
print("HelloWorld!")
```

> 无参数的 print 输出一个空行
> 
> print 函数输出对象的文本表示，因此整数 100 和字符串 ”100” 的文本表示是一样的。
> 
> 当 print 参数包含多个对象时，则依次输出每一个对象的文本表示，默认使用空格分隔。

对 print 对 end 参数进行设置，可以去除换行，例如：

```python
print(666,end="")
```

## turtle 库

使用：

```python
import turtle
```

turtle 中包含了很多个函数，官方文档：https://docs.python.org/3.8/library/turtle.html

### **画笔运动命令**

函数名|功能
---|---
turtle.forward(distance)|向当前画笔方向移动 distance 像素长度
turtle.backward(distance)|向当前画笔相反方向移动 distance 像素长度
turtle.right(degree)|顺时针转动 degree°
turtle.left(degree)|逆时针转动 degree°
turtle.pendown()|移动时绘制图形，缺省时也为绘制
turtle.penup()|提起笔移动，不绘制图形，用于另起—个地方绘制
turtle.goto(x,y)|将画笔移动到坐标为 x,y 的位置（画笔未提起时按直线移动并绘制）
setx()|将当前x轴移动到指定位置
sety()|将当前y轴移动到指定位置
setheading(angle)|设置当前朝向为angle角度
home()|设置当前画笔位置为原点，朝向东。
dot(r)|绘制一个指定直径和颜色的圆点

### **画笔控制命令**

函数名|功能
---|---
turtle.color(color1, color2)|同时设置pencolor=color1, fillcolor=color2
turtle.fillcolor(colorstring)|绘制图形的填充颜色
turtle.begin_fill()|准备开始填充图形
turtle.end_fill()|填充完成
turtle.filling()|返回当前是否在填充状态
turtle.hideturtle()|隐藏画笔的 turtle 形状
turtle.showturtle()|显示画笔的 turtle 形状
turtle.write(s, [font])|写文本，s为文本内容，font是字体的参数
turtle.circle(radius,extent,step)|radius表示半径，正值时逆时针旋转；extent 表示度数，用于绘制圆弧；step 表示边数，可用于绘制正多边形；（extent 和 step 参数可有可无。）
turtle.pensize()|设置画笔粗细，小于10的数

### **画笔全局命令**

函数名|功能
---|---
turtle.clear()|清空turtle窗口，但是turtle的位置和状态不会改变
turtle.reset()|清空窗口，重置turtle状态为起始状态
turtle.undo()|撤销上一个turtle动作
turtle.isvisible()|返回当前turtle是否可见
stamp()|复制当前图形
turtle.speed(speed)|画笔动画速度（0-10）
turtle.tracer(False)|是否显示动画

> turtle.done() **/** 用来停止画笔绘制，但绘图窗体不关闭。

**DEMO 画十字**

```python
import turtle
turtle.write("Welcometoturtle!")
turtle.penup()
turtle.goto(-100,0)
turtle.pendown()
turtle.goto(100,0)
turtle.penup()
turtle.goto(0,100)
turtle.pendown()
turtle.goto(0,-100)
turtle.done()
```

[![turtle.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/24/turtle-.jpg)](https://up.media.everdo.cn/image/ILil)

**DEMO 画五角星**

```python
import turtle
for i in range (5):
    turtle.forward(100)
    turtle.right(144)
turtle.done()
```
[![turtle.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/24/turtle.jpg)](https://up.media.everdo.cn/image/I8v0)

**DEMO 画奥迪车标**

```python
import turtle
turtle.penup()
turtle.goto(-140,0)
turtle.pendown()
for i in range(4):
    turtle.circle(50)
    turtle.penup()
    turtle.forward(80)
    turtle.pendown()
turtle.done()
```

[![turtlelogo.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/24/turtlelogo.jpg)](https://up.media.everdo.cn/image/IalD)

**DEMO 正六边形**

```python
import turtle
turtle.right(36)
turtle.color("orange","orange")
turtle.begin_fill()
turtle.circle(100,360,5)
turtle.end_fill()
turtle.hideturtle()
turtle.done()
```

[![turtlebaa66bd7ff2b7d56.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/24/turtlebaa66bd7ff2b7d56.jpg)](https://up.media.everdo.cn/image/IlDL)
