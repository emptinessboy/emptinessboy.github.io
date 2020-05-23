---
title: JAVA入坑之JDK环境安装到HelloWorld
date: 2020-02-26 20:39:45
category: JAVA学习
tags: java
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/02/26/java.jpg
---
受疫情影响，只好在家上网课了。这学期面向对象的程序设计教的是JAVA，因此开发环境第一波走起。

<br>

## 什么是JDK ？

JDK是用于使用Java编程语言构建应用程序和组件的开发环境。

JDK是整个java开发的核心，它包含了JAVA的运行环境（JVM+Java系统类库）和JAVA工具。

因此想要进行 JAVA 开发，安装 JDK 就是第一步

<br>

## 下载 JDK

JDK 可以从它的开发公司 Oracle（甲骨文） 网站上下载。目前的最新版本是 13.0.2 ，由于之前老师分享的 JDK绿色版 ~~貌似有问题~~ 我环境变量配置的锅，因此去官网下载了最新版本。

>下载地址：[JDK下载](https://www.oracle.com/java/technologies/javase-downloads.html)

选定我们需要的版本，Windows64位可执行的exe版本，然后下载。由于甲骨文网站在国外，下载速度可能比较慢，必要的时候还得科学下。

![jdk1.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk1.png)

下载完成后直接运行安装程序即可。这里有个坑提前说下，如果你的电脑之前已经安装过 JAVA (JRE) 或者其他版本的 JDK 这里可以先卸载一波，以免导致后面 JDK 和 JRE版本不一致的问题。*具体表现为 JAVAC 编译的二进制文件无法被 JAVA 命令直接运行。*

<br>

## 安装 JDK

安装很简单，基本上一路 NEXT 即可，这里我把 JDK安装路径设置到 D:\JAVA\jdk

[![jdk2.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk2.png)](https://up.media.everdo.cn/image/Rn9)

这一步选择安装路径

![jdk3.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk3.png)

然后静静等待进度条跑完即可

![jdk4.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk4.png)

如果看到下面的提示，则表示 JDK 的所有文件已经全部成功解压到对应路径了。

![jdk5.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk5.png)

当然这一步使用非直接运行的压缩包版本也是可以的，两者的区别可能就是 EXE 版本系统会自动注册环境变量，并添加注册表项，方便后续卸载等。

<br>

## 配置环境变量

如果是采用安装程序安装的 JDK ，理论上系统应该会自动配置环境变量。但是很不幸，在我的电脑上自动环境变量没有生效。所以手动配置一波。

环境变量的设置在 **此电脑** 右键--> **属性** --> **高级系统设置** --> **环境变量** 里。

### JAVA_HOME 变量

打开后，我们先新增 JAVA_HOME 变量

变量名|变量值
---|---
JAVA_HOME|D:\Java\jdk-13.0.2

[![jdk6.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk6.png)](https://up.media.everdo.cn/image/3bn)

由于我的 JDK 安装目录为 *D:\Java\jdk-13.0.2* 所以此处 JAVA_HOME 变量值为我的安装路径

### CLASS_PATH 变量

此处 CLASS_PATH 变量同样是新增。由于我们已经配置了 JAVA_HOME 此处变量即可引用 %JAVA_HOME% 这样在以后升级 JDK 的时候可以很方便的切换到最新的版本。

变量名|变量值
---|---
CLASS_PATH|.;%JAVA_HOME%\lib\;

[![jdk9.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk9.png)](https://up.media.everdo.cn/image/DLQ)

注意：JDK8 在配置 CLASS_PATH 的时候则配置为 

```
.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
```

### path 变量

做完了这两步，我们还有最关键的 path 变量。不同于前两条的新建。 path 变量的添加则是在系统已经存在在变量值后面追加两条。一条定位到 JDK 安装目录下面的 bin ，另一条定位到 JRE 目录下面的 bin 。

```
%JAVA_HOME%\jre\bin
%JAVA_HOME%\bin
```

[![jdk7.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk7.png)](https://up.media.everdo.cn/image/YFJ)

选中 path 后双击追加变量值

[![jdk8.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk8.png)](https://up.media.everdo.cn/image/AzS)

添加这两行后直接保存即可。

<br>

## 生成 JRE

什么？！！！为什么在 CMD 输入java 报错？但 javac 却正常？！！

其实到这里我们的 JRE 还没有生成，所以 java 命令是不能运行的。

那么 jre 到底是什么？

>Java运行环境（Java Runtime Environment，简称JRE）是一个软件，由太阳微系统所研发，JRE可以让计算机系统运行Java应用程序。JRE的内部有一个Java虚拟机 JVM 以及一些标准的类别函数库（Class Library）

Oracle 的 JDK 在 13.0 版本默认不自动安装 JRE 。因此我们现在在 JDK 安装路径下看不到 JRE 这个文件夹。

[![jdk10.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk10.png)](https://up.media.everdo.cn/image/bmy)

大概就是我现在这个亚子的

而想要让 JDK13 生成 JRE 的很简单。只需要在 %JAVA_HOME% 下面运行下面的 powershell 命令即可

```powershell
bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre
```
[![jdk11.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk11.png)](https://up.media.everdo.cn/image/dOd)

要注意的是，运行前要CD到 JDK 安装目录。运行后就可以看到，JDK 的安装目录下面有了 JRE 文件夹

[![jdk12.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk12.png)](https://up.media.everdo.cn/image/inl)

这时候，再次运行 JAVA 命令，可以看到有输出结果了

[![jdk13.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk13.png)](https://up.media.everdo.cn/image/rq0)

同样运行 JAVAC 测试下

[![jdk14.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk14.png)](https://up.media.everdo.cn/image/QXD)

查看下两者的版本是否一致

[![jdk15.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk15.png)](https://up.media.everdo.cn/image/x4L)

另外说明下，之前我尝试过从官网下载 jre 然后解压到 jdk 的目录下。这种情况 java 和 javac 都可以正常运行。但是由于 jdk 和 jre 版本不同（sdk不同），很可能出现javac 编译的程序不能被 jre 运行。

<br>

## Hello World !!!

现在到了最振奋人心的 Hello World 时刻了。

来首 Hello World 压压惊。【滑稽】

打开文本编辑器，这里我用的 vstudio ，粘贴下面的 Hello World 代码，保存为 HelloWorld.java （这里文件名要和代码里的 class 一致，包括大小写）

[![jdk16.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk16.png)](https://up.media.everdo.cn/image/Wbc)

代码如下，可直接复制：

```java
class HelloWorld{ 
 public static void main(String[] arr){ 
 System.out.print("HELLO WORLD");
 }
}
```

保存为文件后，我们执行两个命令。(需要先 cd 进入到对应的文件夹)

```powershell
cd c:\users\huxia\desktop

javac HelloWorld.java
```

*吐槽下，沙雕微软为什么把邮箱的前几个字母做文件夹名*


如果你和我一样，看到桌面上多出来一个 HelloWorld.class 的二进制文件，那么恭喜你，HelloWorld 程序已经编译成功啦！！

最后我们执行命令 

```powershell
java HelloWorld
```

[![jdk17.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/jdk17.png)](https://up.media.everdo.cn/image/602)


看到成功输出欢迎信息。WOW，干杯！！

<br>

---

## 更新

到了今天 4月15日 其实 jdk 的 14.0.1 版本已经放出来了。更新过程很简单，一样下载安装后，记住解压缩路径。然后修改 JAVA_HOME

```
%JAVA_HOME% 改为 D:\Java\jdk-14.0.1
```

最后只要在 IED 根据需要更新项目使用的 JDK 即可！

<br>

***原创文章！转载请联系！！！***