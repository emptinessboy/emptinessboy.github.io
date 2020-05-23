---
title: Android开发之 Activity与Intent 入门
date: 2020-04-17 21:25:42
category: Android
tags: 安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/04/android.png
---

可以与用户交互的一个单独的屏幕（页面）称为 Activity。

Activity 用来管理需要显示的各种组件，例如，按钮、输入框、文本框等等。

一个应用程序一般由多个 Activity 构成，此外 Activity 具有生命周期。

##  Activity 概述

创建 Activity 的内部流程（AndroidStudio 会自动帮我们完成的）：

1. 创建一个继承 Activity 类或 Activity 派生类的子类
2. 实现回调方法 onCreadte()，并调用 setContentView(int LayoutResID) 方法，加载布局文件。
3. 在 AndroidManifest.xml 中声明 Activity

### 继承关系

在 AndroidStudio 选中 MainActivity 使用快捷键 ctrl+H 即可查看这个类的父类层级：

[![activity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/17/activity.jpg)](https://up.media.everdo.cn/image/P99Q)

模板代码：

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

> 现在默认系统会自动将 MainActivity extends AppCompatActivity，如果使用旧版 MainActivity extends Activity 直接继承父类，则会不显示 ToolBar，生成一个非常干净的空白页面。

## Intent 与 IntentFilter

Intent 的中文意思是“意向、意图”。Android 中提供了 Intent 机制来协助应用间的交互和应用程序内部的 activity, service 和 broadcast receiver 之间的交互。即使用 Intent 实现程序的“调用意图”。

### Intent 属性

Intent 包括如下的属性，用于完成执行的意图：

1. action（动作）: 用来表示意图的动作，如：查看，发邮件，打电话
2. category（类别）: 用来表示动作的类别。
3. data（数据）: 表示与动作要操作的数据。如：查看指定的联系人
4. type（数据类型）: 对data类型的描述。
5. extras（附件信息）: 附件信息。如：详细资料，一个文件，某事。
6. component（目标组件）: 目标组件。

### IntentFilter 属性

IntentFilter 是 Intert 的过滤器。 Android 操作系统使用过滤器来指定一系列活动、服务和广播接收器处理意图，需要借助于意图所指定的动作、类别、数据模式。

“过滤”大多情况下不在 java 代码中设置，而是在应用的 manifest 文件中作为 ```<intent-filter>``` 元素的方式声明。在 manifest 文件中使用  ```<intent-filter>``` 元素在活动，服务和广播接收器中列出对应的动作，类别和数据类型。

下面是 menifest 文件 ```<intent-filter>``` 部分展示：

```xml
 <application
    <!-- 此处不是重点，省略... -->
    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <!-- 定义打开应用后最先执行的方法/组件 -->
            <category android:name="android.intent.category.LAUNCHER" />
            <!-- 设置过滤器动作类别，此行表示在程序列表看到此应用图标 -->
        </intent-filter>
    </activity>
</application>
```

## Activity 间的跳转

Intent（意图） 分为 显式Intent 和 隐式Intent。

**显式Intent：**

显式意图经常用于连接应用程序的内部世界。例如，在一个应用中，需要从一个 Activity 跳转到另外一个 Activity。

**隐式Intent：**

隐式意图经常用于激活其他应用程序的组件。例如，启动浏览器打开一个网页，启动拨打电话界面等。

### 显式 Intent 跳转 Activity 

实现同一个 APP 内两个 Activity 间互相跳转，最简单的方法是使用显式 Intent。

通过名称启动目标组件的步骤：
     
1. 实例化 Intent 对象。其中一个Intent构造方法：**Intent(Context  Context, Class<?> cls)**
2. 调用 **Activity.startActivity(Intent intent)** 方法，启动一个 Activity

> Intent构造方法中第一个参数：Context 是当前 Activity 的上下文对象。第二个参数 cls 是要跳转的目标 Activity 的类名。

示例代码：

```java
// 通过指定类名的显式意图
Intent intent=new Intent(MainActivity.this,SecondActivity.class);
// 启动目标活动
startActivity(intent);
```

#### 实验

新建一个 Activity：second activity

[![activity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/activity.jpg)](https://up.media.everdo.cn/image/PEUJ)

修改一个好记的名字：

[![activity1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/activity1.jpg)](https://up.media.everdo.cn/image/Pf7y)

```xml
在 AndroidManifest.xml 中组件声明处新增 lable，方便后续查看

<activity android:name=".SecondActivity" android:label="Second Activity"></activity>
```

在 MainActivity 添加按钮，并添加点击事件监听：

[![7905609c89e96e63287ad2e02071ba29.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/7905609c89e96e63287ad2e02071ba29.jpg)](https://up.media.everdo.cn/image/Psxd)

完整按钮以及 Intent 使用的代码：

```java
Button gotoSecAct = findViewById(R.id.gotoSecAct);
gotoSecAct.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        startActivity(intent);
    }
});
```

运行效果：

[![IntentActivity.gif](https://media.everdo.cn/tank/pic-bed/2020/04/18/IntentActivity.gif)](https://up.media.everdo.cn/image/PzXl)

### 隐式 Intent 启动不确定的目标：

当无法确定意图目标，即目标组件名称时，使用隐式 Intent 启动。通常用于启动其他应用的组件。

####  A 启动默认浏览器：

```java
//准备Intent的data属性数据
Uri uri = Uri.parse("https://coding.emptinessboy.com");
//设置Intent的action属性和data属性
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
//启动目标意图
startActivity(intent);
```

##### 实验：

增加打开浏览器的按钮：

[![3d9f7d3c347a49dab125758ef45c7a3c.md.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/3d9f7d3c347a49dab125758ef45c7a3c.md.jpg)](https://up.media.everdo.cn/image/P1H0)

增加按钮监听事件：

```java
Button gotoBrowser = findViewById(R.id.gotoBrowser);
gotoBrowser.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Uri emptinessboy = Uri.parse("https://coding.emptinessboy.com/");
        //设置Intent的action属性和data属性
        Intent intEmptinessboy = new Intent(Intent.ACTION_VIEW,emptinessboy);
        //启动目标意图
        startActivity(intEmptinessboy);//启动目标意图
    }
});
```

运行效果（成功打开浏览器）：

[![IntentBrowser.gif](https://media.everdo.cn/tank/pic-bed/2020/04/18/IntentBrowser.gif)](https://up.media.everdo.cn/image/PMdD)

####  B 注册自定义“浏览器”：

这个例子将一个自定义应用注册为浏览器，并配置可以接收另一个应用的传入值：

先新建一个测试 APP（自定义浏览器）

1.向自定义浏览器的 AndroidManiFest.xml 文件添加过滤器配置

```xml
<intent-filter>
    <!-- 赋予具备查看的功能 -->
    <action android:name="android.intent.action.VIEW" />
    <!-- 赋予默认类别和浏览类别的数值 -->
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <!-- 传递这两个开头网址，就被过滤器筛选出 -->
    <data android:scheme="http" />
    <data android:scheme="https" />
</intent-filter>
```

2.在 MainAcitivity 中获取网页地址

```java
//获取Intent对象
Intent intent=getIntent();
//获取intent对象中data属性的字符串数据
String uriStr=intent.getDataString();
```

```java
//进行显示
TextView t = findViewById(R.id.TextView);

/**可能产生空指针异常
if(!uriStr.isEmpty()){
    t.setText(uriStr);
}
*/
if(uriStr != null){
    t.setText(uriStr);
}
```

运行效果，可以看到单击按钮后，看到了我们创建的“浏览器应用”

[![133a08fe6b871673d63b926003b04abb.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/133a08fe6b871673d63b926003b04abb.jpg)](https://up.media.everdo.cn/image/Pv0L)

点击我们创建的“浏览器”后，可以正确显示传入网址：

[![f4812890cb4f1caaa3253a9c847d98a4.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/f4812890cb4f1caaa3253a9c847d98a4.jpg)](https://up.media.everdo.cn/image/Py8c)


##### 直接启动自定义“浏览器”：

1.在自定义浏览器的AndroidManifest.xml中增加过滤器action属性值。

```java
<intent-filter>
    ……
    <action android:name="com.emptinessboy.testbrower.start" />
    ……
</intent-filter>
```

2.通过在测试 APP 调用自定义浏览器设定的 action 动作：“com.emptinessboy.testbrower.start”，直接启动自定义浏览器:

```java
//准备Intent的data属性数据
Uri uri = Uri.parse("https://coding.emptinessboy.com");
//旧的 Intent intEmptinessboy = new Intent(Intent.ACTION_VIEW,uri;
Intent intent = new Intent("com.emptinessboy.testbrower.start",uri);
startActivity(intent);
```

运行效果：

[![IntentBrowserdefault.gif](https://media.everdo.cn/tank/pic-bed/2020/04/18/IntentBrowserdefault.gif)](https://up.media.everdo.cn/image/PX32)

