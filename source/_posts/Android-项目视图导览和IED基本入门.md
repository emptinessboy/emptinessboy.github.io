---
title: Android 项目视图导览和IED基本入门
date: 2020-04-02 22:35:53
category: Android
tags: 安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/04/android.png
---

Android Studio 包含用于构建 Android 应用所需的所有工具

## 视图

Android Studio 提供了多种项目管理视图，项目窗口在 Gradle 同步完成后，默认显示的是 Android 视图

[![Android.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/Android.jpg)](https://up.media.everdo.cn/image/HlDM)

在点击切换按钮后，我们可以切换到 Project 项目视图获得更细致的内容：

[![project.png](https://media.everdo.cn/tank/pic-bed/2020/04/02/project.png)](https://up.media.everdo.cn/image/HufY)

App目录展开细节如下：

[![app.png](https://media.everdo.cn/tank/pic-bed/2020/04/02/app.png)](https://up.media.everdo.cn/image/J45a)


## app/build.gradle文件

不用于 Eclipse，Android Studio 是采用 Gradle 来构建项目的。Gradle 是一个非常先进的项目构建工具，它使用了一种基于 Groovy 的领域特定语言（DSL）来声明项目设置，摒弃了传统基于 XML（如Ant和Maven）的各种繁琐的配置。

项目中有两个 build.gradle 文件，一个是在最外层目录下的，一个是在 app 目录下的。这两个文件对构建 Android Studio 项目都起到了至关重要的作用。

下面是 HELLO WORLD 项目下的内层APP目录下的 build.gradle文件：

```json
apply plugin: 'com.android.application'

android {
    compileSdkVersion 29
    buildToolsVersion "29.0.3"  //编程所用的 API 版本

    defaultConfig {
        applicationId "com.emptinessboy.helloworld" //应用程序包名
        minSdkVersion 21    //最低兼容的 API 版本
        targetSdkVersion 29 //面向的 API 版本
        versionCode 1   //当前软件版本号
        versionName "1.0"   //当前软件版本名

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false //是否在编译时混淆代码（发布用）
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }

}

dependencies {  //指明项目中的第三方函数库
    implementation fileTree(dir: 'libs', include: ['*.jar'])

    implementation 'androidx.appcompat:appcompat:1.0.2'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
}
```
对于项目 API 版本的设置，按照下面的原则是比较推荐的：

> ompileSdkVersion ≥ targetSdkVersion ≥ minSdkVersion

## AndroidManifest.xml

> 详细文档： https://developer.android.com/guide/topics/manifest/manifest-intro

此文件位于 app\src\main\AndroidManifest.xml

AndroidManifest.xml 文件可以理解为 Android 整个应用程序的配置清单文件，用于向Android系统提供关于应用程序的配置信息。（包含： 包名、组件、权限等信息。）

下面是 HELLO WORLD 项目下的 AndroidManifest.xml 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.emptinessboy.helloworld">  <!--项目的包名-->

    <application
        android:allowBackup="true"  /*是否允许备份应用的数*/
        android:icon="@mipmap/ic_launcher"  /*图标（方形）*/
        android:label="@string/app_name"    /*应用程序标题*/
        android:roundIcon="@mipmap/ic_launcher_round"   /*图标（圆形）*/
        android:supportsRtl="true"  /*支持从右到左布局*/
        android:theme="@style/AppTheme">    /*主题界面风格*/
        <activity android:name=".MainActivity">  <!--组件声明-->
            <intent-filter>     <!--过滤器-->
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

### 安卓四大组件

Android 四大组件：

- Activity（活动） ```<activity android:name="">......</activity>```
- Service（服务） ```<service android:name="">......</service>```
- ContentProvider（内容提供者） ```<provider android:name= "">......</provider>```
- BroadcastReceiver（广播接收者） ```<receiver android:name="">......</receiver>```

> 注意：启动一个没有在AndroidManifest.xml文件中声明过的组件，会抛出异常

### 权限标签

> 具体文档： https://developer.android.com/reference/android/Manifest.permission

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.emptinessboy.helloworld">
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
</manifest>
```

## IED 相关

### 配置自动包导入：（实用）

[![androidstudio-auto-import.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/androidstudio-auto-import.jpg)](https://up.media.everdo.cn/image/JJjs)

### 配置文件字符显示

[![androidstudio-uft8.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/androidstudio-uft8.jpg)](https://up.media.everdo.cn/image/JPN3)

### 日志工具使用

Log 是 Android 提供的用来输出日志的工具类 (android.util.Log)

Log 常用的方法：

1. Verbose：最为繁琐、意义最小的信息
2. Debug：调试信息
3. Info：比较重要的数据
4. Warn：警告信息
5. Error：错误信息

通过 Logcat 监视器，查看 Android 应用运行时输出的日志信息：

[![logcat.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/logcat.jpg)](https://up.media.everdo.cn/image/JIpG)

可以在上方导航栏切换当前调试设备，日志输出的应用，日志级别，也可以针对性过滤隐藏日志。

### 调试程序时输出 log 到 logcat

这一步操作效果等同于 java 语言的 System.out.print();

```java
import android.util.Log;    //导入log包
public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MainActivity";   //声明标签变量（常用类名）
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Log.d(TAG, "onCreate: 已经在运行");    //使用log打印输出
    }
}
```

[![logcat-logd.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/02/logcat-logd.jpg)](https://up.media.everdo.cn/image/JnI9)

当日志过多时，可以用在搜索框用 Tag 进行过滤（支持正则）。

#### 快速生成日志代码

```
logt 声明标签 \ logd 打印输出
```

### 快捷键

#### **提示和生成代码**

- **Ctrl + Alt+ Space** 代码提示
- **Ctrl + P** 提示参数
- **Ctrl + J** 快捷代码提示
- **Ctrl + Alt + T** 为选择的代码，添加 if 、for、try/catch 等语句
- **Alt + Insert** 弹出自动生成代码对话框
- **Ctrl + O** 弹出类中可重写的方法对话框
- **Alt + 回车** 可以触发代码联想

#### **编辑代码快捷键**

- **Ctrl + Shift + Up/Down** 移动当前行代码
- **Ctrl + D** 复制当前行代码到下行
- **Ctrl + W** 选中代码，连续按会有不同的选中效果
- **Ctrl + Alt + L** 代码格式化

#### **替换和查找**

- **Ctrl + F** 查找
- **Ctrl + R** 替换

#### **查看代码**

- **Ctrl + N** 输入类名，快速打开—个指定的类
- **Ctrl + H** 查看父类层级
- **Ctrl + U** 查看当前类的父类
- **Ctrl + Alt + Left/Right** 光标返回上—次停留的位置
- **Alt + Up/Down** 光标在类方法间快速移动
- **Ctrl + "+"** 光标所在方法展开
- **Ctrl + "-"** 光标所在方法折叠收起
- **Ctrl + Shift + "+"** 当前类所有方法展开
- **Ctrl + Shift + "-"** 当前类所有方法折叠收起
- **Ctrl + Shift +［或** 选择大括号间的全部代码
- **Ctrl + Alt + H** 查看—个方法被调用的位置
