---
title: AndroidStudio 入门之环境搭建和第一个程序
date: 2020-04-02 15:22:19
category: Android
tags: 安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/06/AndroidStudio.jpg
---

前言：开发安卓项目有许多不同的方式，不同语言，不同IED。

1. Google App Inventor 
2. ADT Bundle （Eclipse）
3. Android Studio

面向入门者的 App Inventor 是由 Google 开发的一款可视化的 Android 开发工具。不需要掌握高深的语言基础就可以简单实现基本的 App。对于传统或者标准的安卓开发则是基于 Java 和 Kotlin 语言。

ADT Bundle 是一个已经打包好的开发套件，包含了 Eclipse、ADT插件 和 SDK Tools，是已经集成好的 IDE，只需安装好 Jdk即可开始开发，不用再折腾开发环境。

最后在 Google 的开发文档中，推荐用 Android Studio，（对于新手而言不友好）。本篇文章就开始从 Android Studio 开始到第一个 HelloWorldApp，一点点踩坑并记录笔记。

## 安装 JAVA 开发环境 JDK

在之前的文章里已经很详细的记录了如何在 Windows 环境下安装配置 JDK 13。可以参考下面的链接：

- [JAVA入坑之 JDK环境安装到 HelloWorld](https://coding.emptinessboy.com/2020/02/JAVA%E5%AD%A6%E4%B9%A0%E4%B9%8BJDK%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85/)

当然，Android 不需要那么高的 JDK 版本，常用的 1.8 就够用。

## 下载 Android Studio

在 Google 的安卓开发者官网，可以很轻松的下载到 Android Studio （不需要翻'wall） 而且速度很快。

- [https://developer.android.com/studio](https://developer.android.com/studio)

这里直接下载默认的 exe 可执行文件就可以了。

[![androidstudio.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/androidstudio.jpg)](https://up.media.everdo.cn/image/HmM6)

下载完成后，直接双击运行。

## 安装汉化 Android Studio

安装 Android Studio 的过程和我们安装其他软件没有太多的不同：在看到安装向导的时候一路 Next 就可以了。

[![AndroidStudio_1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/AndroidStudio_1.jpg)](https://up.media.everdo.cn/image/HcAS)

选择标准一般不会出什么问题

[![AndroidStudio_2.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/AndroidStudio_2.jpg)](https://up.media.everdo.cn/image/HfcQ)

选择主题（Android Studio 的 ui 非常棒，个人比较喜欢暗色）：

[![AndroidStudio_3.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/AndroidStudio_3.jpg)](https://up.media.everdo.cn/image/Hs5J)

在下面系统会自动从网络下载所需要的包并自动完成安装。

### 中文语言包

下载地址：[来自pingfangX大佬](https://github.com/pingfangx/TranslatorX) [DriLink](https://github.com/pingfangx/jetbrains-in-chinese/tree/master/AndroidStudio)

下载汉化语言包 resources_zh_CN_AndroidStudio_3.5_r1.jar，

将 resources_zh_CN_*.jar ，放到 AndroidStudio 的 **安装路径** 下的 **lib** 目录中，重启软件即可。

## 启动并下载 SDK：

安装完成后，双击桌面的 Android Studio 图标就可以启动了。

启动的第一步，就是安装我们所需要使用的安卓 SDK 版本，现在是 2020 年的 4 月，目前最新的 SDK 版本是 API-29 的 Android Q（安卓10）：

[![sdkmanager.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/sdkmanager.jpg)](https://up.media.everdo.cn/image/H16d)

勾选完自己需要使用的 SDK 版本后，系统会自动进行下载和安装（如果因为网络原因失败，可以多尝试几次）。

### 排错 01

如果你和我一样，在第一次启动时遇到了下图那样的 Cannot lock system folder 的报错。

[![8634b7a20ac1f157b1833d4db5e15905.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/8634b7a20ac1f157b1833d4db5e15905.jpg)](https://up.media.everdo.cn/image/H9gn)

只需要在 PowerShell（管理员） 中执行一句命令然后重启电脑就可以了。

```cmd
netsh winsock reset
```

[![dc93347f197d483e08102401967cfecb.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/dc93347f197d483e08102401967cfecb.jpg)](https://up.media.everdo.cn/image/H0Ry)

如果到这里，你和我后来遇到的一样，又出现这个问题了，恭喜你，下面的一定可以帮到你：

#### **4月6日补充：**

在使用 Android Studio 几天后，发现经常性的还是会遇到这样的错误：

[![can-not-bind.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/06/can-not-bind.jpg)](https://up.media.everdo.cn/image/JtuO)

运行上面的重置 winsock 命令并重启后，马上运行 Android Studio 则正常，若等一段时间再运行开发工具就会弹出一样的错误。

开始的时候，以为是开发工具的 bug，在 百度 和 CSDN 下搜索也得不出有效答案。emm，开始想偷懒，打算就这么凑合用吧。可是当我打开 pyCharm 的时候，发现 IED 报了同样的错误。（这么多软件报错，那本宝宝不能忍呀！！

经过测试，发现在我的电脑上 JetBrains 家的全部软件均出现了这样的问题。更新 Android Studio 和 pyCharm 也还是问题复现。也考虑过会不会是 jdk 的问题，不过在进行更新 JDK 后发现问题依旧。

最后无比艰难的上 Google 一通搜索后，在 JetBrains 开发者社区找到了答案。下面让我借此做一个问题查找过程的回顾：

定位到我们启动 IED 时的报错：

```java
nternal error. Please refer to https://code.google.com/p/android/issues

java.util.concurrent.CompletionException: java.net.BindException: Address already in use: bind
```

可以看到产生 winsock 报错的主要原因是 bind 失败了。

> 来自论坛外国 dalao 的解释：
> 
> To lock folders IDE is starting a server on localhost, it tries to bind on the first available port between 6942 and 6991, this exception is thrown if IDE was not able to bind on any of the ports in this range. All 50 ports are unlikely to be already used on a machine, so it appears to be a networking issue or some security software which doesn't permit IDE to bind on any port in this range even on localhost interface.

看到这个我们就知道了，在 JetBrains 的 IED 启动的时候，会尝试监听 6942 到 6991 的任意端口。而现在我们遇到的情况是监听失败了。

而在这之前，我已经使用命令 ```netstat -no | findstr``` 排除了端口被占用的问题。根据老外的分析，则有可能是网络故障。

在继续搜索的时候，我看到 GitHub docker-for-win 下面的 issue 有人遇到和我一样的问题。

https://github.com/docker/for-win/issues/3171

经过判断，初步定位问题可能是由 hyper-v 造成的，在使用命令 ```dism.exe /Online /Disable-Feature:Microsoft-Hyper-V``` 禁用 hyper-v 并重启后，一切都正常了！！

可是在我的笔记本电脑也启用了 hyper-v 服务，而且 Android Studio 在我的笔记本上，运行一切正常。（总不能简单粗暴阉 hyper-v 吧

继续浏览发现：出现这个问题的大多是在 Windows 开发者预览版系统上，而我，恰巧前阵子手贱，把系统升级到了预览版（手动狗头

[![yvlanban.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/07/yvlanban.jpg)](https://up.media.everdo.cn/image/JOY6)

那么为什么预览版系统的 hyper-v 会造成这个问题呢？其实这个并不是微软故意弄出来的 bug，而是预览版的 WSL （Windows下的Linux子系统）版本升级到了 WSL2。而 WSL2 是使用 hyper-v 运行 Linux 内核的。在 WSL2 上，hyperv 会将一些端口列入系统排除端口避免被其他进程使用。这就导致了明明端口没被占用却无法监听的问题了。

最后我是按照下面的解决方案解决的（来自 github @enashed）

> I ran ```netsh int ipv4 show dynamicport tcp``` 
> Ran ```netsh int ipv4 set dynamic tcp start=49152 num=1638``` to reset it to something sane
> Also ran ```reg add HKLM\SYSTEM\CurrentControlSet\Services\hns\State /v EnableExcludedPortRange /d 0 /f``` for good measure as netsh int ipv4 show excludedportrange protocol=tcp showed a lot of excluded ports

在这样一波操作后，运行命令检查端口：

[![paichu-duankou.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/07/paichu-duankou.jpg)](https://up.media.everdo.cn/image/JUzn)

可以看到保留端口范围已经避开了 IED 使用的范围。添加的注册表项用于禁止 hyper-v 保留反射端口。

重启电脑，问题秒杀之。又可以开开心心撸代码了！！

*其实，为了这个问题真的折腾了我一下午加一晚上。卸载杀毒软件，更新系统，升级IED，重置网络等等。。。原来到底还是 WSL 的锅。还是希望微软爸爸或者 JetBrains 哥哥可以体谅下我这样菜鸡的程序 ~~猿~~，在后面的更新解决这个冲突（手动狗头。*

参考文章： [01](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360004973960-Critical-Internal-Error-on-Startup-of-IntelliJ-IDEA-Cannot-Lock-System-Folders-) / [02](https://intellij-support.jetbrains.com/hc/en-us/community/posts/206193909-Address-already-in-use) / [03](https://dandini.wordpress.com/tag/administered-port-exclusions/)

## AVD 虚拟机 和 环境变量

下载完 SDK 后，我们还要为接下来的安卓项目调试做准备。要确保 AVD 虚拟机可以正常的工作。

点击 Configure ，进入 AVD manager。然后新建一个虚拟设备。在选择设备模板的页面我们可以根据需要选择安卓电视设备，手机，平板，可穿戴等等。

[![avd-select.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/avd-select.jpg)](https://up.media.everdo.cn/image/HMSl)

下一步，我们要为设备选择安卓的版本（SDK版本），然后系统会根据需要，下载系统镜像。

[![avd-selectimg.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/avd-selectimg.jpg)](https://up.media.everdo.cn/image/HyP0)

这里我已经下载好了安卓Q和安卓PIE两个镜像。准备完这一切，配置好具体参数，就可以正式启动模拟设备了。

[![acd-confirm.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/acd-confirm.jpg)](https://up.media.everdo.cn/image/HTiD)

这时，系统会在 “我的文档” 下的 .Android/AVD 里面存放虚拟系统的磁盘和系统配置文件。

[![avd-path.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/avd-path.jpg)](https://up.media.everdo.cn/image/HCgc)

最后，虚拟设备成功启动：

[![avd-success.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/avd-success.jpg)](https://up.media.everdo.cn/image/HXML)

emm，AVD 系统自带 GooglePlay 全家桶，美妙又清新。（先上波 YouTube 看看 Tom & Jerry

[![avd-youtube.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/avd-youtube.jpg)](https://up.media.everdo.cn/image/HtcZ)

### 排错 02

如果你又和我一样不幸，出现了下面这样令人尴尬的报错：

```
Emulator: PANIC: Cannot find AVD system path. Please define ANDROID_SDK_ROOT
或者：Broken AVD system path. Check your ANDROID_SDK_ROOT value
```

这个问题多半出现在 Windows系统环境变量 上面，我这里所作的，就是删掉多余的无关变量，仅仅将 Android Home 指向 SDK 存放的路径。

[![windows-path.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/windows-path.jpg)](https://up.media.everdo.cn/image/HpD2)

## 第一个安卓程序

又到了令人兴奋的 Hello World 环节，不过好像又没那么容易，让我喝杯水冷静下。

### 创建安卓项目

Hello World 大法的第一步当然是创建安卓项目了。点击加号 + Start a new Android Studio project 

这里 Google 为我们提供了许多自带的 UI 模板，我们先选择最简单的 Empty Activity。

[![select-form.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/select-form.jpg)](https://up.media.everdo.cn/image/HUjB)

选择完成后，进入确认项目页面：

[![configure-project.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/configure-project.jpg)](https://up.media.everdo.cn/image/Hw5k)

这里 Name 栏目表示应用程序名字，Package 包名一般是网址倒着写，因此这里包名就是 com.emptinessboy.com.helloworld

SelectLocation 栏目选择项目存放位置（实测存放在中文路径会报错）， Language 可以选择 Java 或者 kotlin。最小 SDK 选择兼容的最低安卓版本。

### 进入编辑器

如果一切顺利，（我是在经历99八十一难后），终于看到了 Android Studio 的编辑器：

[![into-editor.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/into-editor.jpg)](https://up.media.everdo.cn/image/HKII)

可以看到 Android Studio 已经为控制布局的 activity_main.xml 自带了一个设计窗口，右边是自动打开的主函数文件 MainActivity.java

这里试着修改文字 HelloWorld,I am Emptiness Boy!

[![eitd-words.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/eitd-words.jpg)](https://up.media.everdo.cn/image/HLiX)

### Hello World!

#### 模拟器调试

然后点击绿色的运行按钮！

[![android-helloworld.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/android-helloworld.jpg)](https://up.media.everdo.cn/image/H8vi)

可以看到 第一个HelloWorld应用 已经在模拟器中成功跑起来了。

#### 真机调试

既然有模拟器了，为什么不试试物理机？果断抄起了我久经沙场的 OnePlus5，在手机上开启开发者模式后，投屏到电脑。

[![oneplus-helloworld.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/oneplus-helloworld.jpg)](https://up.media.everdo.cn/image/Hal4)

可以看到 AndroidStudio 已经成功识别我的手机，并通过 ADB 成功安装了 HelloWord 应用。

### 排错 03

今天真是运气太背了，已经是第三个坑了。在 Hello World 关键阶段出现的问题是 Gradle 一直在 sync ，并且好长时间后还是失败了。

[![Gradle-sync-fail.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/Gradle-sync-fail.jpg)](https://up.media.everdo.cn/image/HZ6t)

一直以为是 qiang‘guo 的原因，所以折腾了好久路由器。可是最后却发现情况来的有点蹊跷。

经过一番检查，发现原来是 Gradle 下面的一个配置文件在做怂（果断抄起 notepad++ 干掉之）：

[![fix-gradle-sync.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/fix-gradle-sync.jpg)](https://up.media.everdo.cn/image/H5px)

将里面的 HTTPproxy 都注释掉，再尝试重新 sync，问题解决之。

### 排错 04

这是今晚最后一个坑了。就是在调试时遇到的 Can't bind to local 8600 for debugger 问题。

开始时查阅网上教程，以为是端口被其他程序占用的问题，如 Eclipse。可是通过命令行

```cmd
netstat -aon|findstr 8600
```

却一无所获，就更不要说什么 kill 掉占用进程了。

```cmd
taskkill /pid ????-t -f
```

最后惊讶的发现问题出在之前被我动过的系统 hosts，因为 hosts 里 localhost 栏被我注释掉了。因此 ADB 工具自然无法找到 localhost 的地址了。

打开 hosts 文件，补上下面一行

```
127.0.0.1 localhost
::1       localhost
```

问题就这样消失了，WTF!!（小声BB
