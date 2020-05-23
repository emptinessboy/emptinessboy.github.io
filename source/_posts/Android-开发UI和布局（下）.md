---
title: Android 开发UI和布局（下）
date: 2020-04-05 02:51:58
category: Android
tags:  安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/04/android.png
---

## Constraint Layout 布局

Google I/O 2016 上发布了 Constraint Layout，Constraint 就是约束的意思。

约束帮助保持控件对齐. 你可以使用锚点(约束手柄)来确定各控件之间的对齐规则。

### 创建手工约束

> 有一个像磁铁一样的小图标，打开和关闭用于切换自动/手动创建约束。
<!--more-->

要创建一个约束, 你需要在指定手柄上点击并按住鼠标, 然后拖到另一个控件的约束手柄. 一旦锚点变绿, 就可以松开鼠标完成约束创建.

[![contraintLayOut.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/contraintLayOut.gif)](https://up.media.everdo.cn/image/JZKS)

#### 创建

如下所示创建一个 TextView 上锚点和 ImageView 底锚点之间的约束。

[![contraintLayOut2.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/contraintLayOut2.gif)](https://up.media.everdo.cn/image/JG2Q)

#### 调整元素尺寸

此外，约束模式支持点击拖动角以调整图片大小：

[![contraintLayOut1.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/contraintLayOut1.gif)](https://up.media.everdo.cn/image/JKmJ)

#### 定位布局

我们还可以使用左和右侧边约束锚定 ImageView 在布局中间：

[![contraintLayOut3.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/contraintLayOut3.gif)](https://up.media.everdo.cn/image/JLwy)

#### 基线约束

要连接控件的基线, 鼠标悬浮在空间上, 等几秒钟, 基线约束出现然后就可以连接了。

[![contraintLayOut4.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/contraintLayOut4.gif)](https://up.media.everdo.cn/image/Jand)

### Inspector 工具

ViewInspector.Inspector 在 UI 生成器上的右边. 除了列出所选控件的属性, 它还展示了 View 是如何对齐的以及所有的约束。

[![Inspector.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/Inspector.jpg)](https://up.media.everdo.cn/image/JgQl)

Inspector 显示出控件控件所在的区域

#### **Margins：**

控件外部的左右上下就是 margin. 可以点击 margin 的值并设置成另一个值来改变它. 

#### **相对约束定位控件：**

当一个控件上有至少两个对立的连接时, 比如上和下, 或者左和右, 你可以看到一个可以让你沿着对立连接的轴调整控件位置的滑块. 这也被称为横向或纵向偏量. 调整纵向和横向偏量然后改变方向, 可以看到偏量依然保留. 另外也可以通过移动控件到目标目标位置实现这一点.

[![aeb88b5a9ecddd7ed2da4a96effb3095.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/aeb88b5a9ecddd7ed2da4a96effb3095.gif)](https://up.media.everdo.cn/image/JlT0)

#### **控件内部尺寸: **

控件内部的线允许你控制它的尺寸。

[![size.png](https://media.everdo.cn/tank/pic-bed/2020/04/09/size.png)](https://up.media.everdo.cn/image/P44D)

这是 Inspector 中一个控件的放大视图. 点击 Inspector 面板控件内部的线, 会循环切换以下选项

[![size1.png](https://media.everdo.cn/tank/pic-bed/2020/04/09/size1.png)](https://up.media.everdo.cn/image/PPL2) **Fixed:** 此选项允许你指定控件的高和宽.

[![size2.png](https://media.everdo.cn/tank/pic-bed/2020/04/09/size2.png)](https://up.media.everdo.cn/image/PHYL) **AnySize:** 此选项让控件占用所有可用空间以适应约束. 换句话说, 这更像是匹配约束. 与 match_parent 不同, 后者占用父 View 的所有可用空间.AnySize 与容器无关. 如果 ImageView 约束于一个 Button, 设置为 AnySize 只会扩展它适应 button.

[![size3.png](https://media.everdo.cn/tank/pic-bed/2020/04/09/size3.png)](https://up.media.everdo.cn/image/PJzc) **Wrap Content:** 此选项仅扩展至所含元素(如 text 或者 drawable)填充满 widget.

#### 擅用辅助线

单击辅助线位置上的标记，可以在 dp 和百分比之间切换。可以将控件基于辅助线创建约束。

#### DEMO

这里为了后面的学习，我使用 Constraint Layout 绘制了一个看起来还不错的登录界面。最终效果图如下：

[![login.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/login.jpg)](https://up.media.everdo.cn/image/Ph2Z)

布局细节：（因为水平有限，外层 Constraint Layout，中间部分嵌套了 LinerLayout）

[![login1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/login1.jpg)](https://up.media.everdo.cn/image/Pnmk)

##### 顶部透明状态栏

通过修改 ```res/values/styles.xml```

```xml
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
         <!-- 透明部分. -->
        <item name="windowActionBar">false</item>
        <item name="windowNoTitle">true</item>
        <item name="android:windowTranslucentStatus">true</item>
        <item name="android:windowDrawsSystemBarBackgrounds">true</item>
        <item name="android:statusBarColor">@android:color/transparent</item>

    </style>

</resources>
```

主题色 ```res/values/colors.xml```

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#505050</color>
    <color name="colorPrimaryDark">#303030</color>
    <color name="colorAccent">#FF9800</color>
</resources>
```

##### 自定义的按钮

顶部两个灰色按钮和下方的登录按钮使用了 imgButton 和 普通按钮的集合：

> 使用 selector 改变 Button 点击时和非点击时的背景，实现点击按钮改变颜色的触摸反馈。

1. 在 drawable 中新建两个 xml 文件，使用 shape 定义背景。（```shape_normal.xml``` 和 ```shape_pressed.xml```）
2. 在 drawable 中新建 ```button_selector.xml``` 文件。
3. 使用 item 中的 ```android:state_pressed``` 属性指定点击时和非点击时使用的效果文件。
4. 在 Button 中添加 ```android:background="@drawable/button_selector"``` 属性

主布局文件处修改：

```xml
<ImageButton
   android:id="@+id/buttonClose"
   android:layout_width="35dp"
   android:layout_height="35dp"
   android:background="@drawable/imgbutton_selector"/>
<!--按钮内部分代码省略，主要修改了background-->
<Button
   android:id="@+id/buttonReg"
   android:layout_width="58dp"
   android:layout_height="31dp"
   android:background="@drawable/button_selector"
   android:text="@string/reg"
   android:textColor="#FFFFFF"
   android:textColorHint="#505050"/>
<!--按钮内部分代码省略，主要修改了background-->
```

由于修改了默认的背景样式，导致按钮不能继承默认主题的样式，所以会失去点击触发效果。因此这里给按钮增加选择器：

```xml
<!--res/drawable/button_selector.xml-->
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true"
        android:drawable="@drawable/shape_pressed"/>
    <item android:state_pressed="false"
        android:drawable="@drawable/shape_normal"/>
</selector>

<!--res/drawable/imgbutton_selector.xml-->
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true"
        android:drawable="@drawable/imgbutton_circlepressed"/>
    <item android:state_pressed="false"
        android:drawable="@drawable/imgbutton_circlenormal"/>
</selector>
```

创建上面所引用的四个 xml 文件：（由于另外三个代码部分基本相同就不再展示）

```xml
<!--res/drawable/imgbutton_circlenormal.xml-->
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" android:shape="rectangle" >
    <solid android:color="#60000000" />
    <!--    <stroke android:width="1dip" android:color="#3F3F3F"/>-->
    <!--     圆角-->
    <corners android:radius="100dp" />
    <!--     边距-->
    <padding
        android:bottom="3dp"
        android:left="3dp"
        android:right="3dp"
        android:top="3dp" />
</shape>
```

##### 按钮触摸反馈动画

使用系统自带的两个 Ripple 波纹效果

```java
//有边界
?android:attr/selectableItemBackground
//无边界 （要求API21以上）
?android:attr/selectableItemBackgroundBorderless 
```
使用时只需要把上面这两个值作为 View 的 ```android:background="" 或 android:foreground=""``` 即可（如果已经有背景， 可以设置到前景属性中）。

想要效果显示出来要保证 View 的 ```android:clickable="true"```。
这里的颜色是系统默认的，可以在 theme 里更改默认的波纹颜色：

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
    <!-- API 21 theme customizations can go here. -->
    <item name="android:colorControlHighlight">#ff0000</item>
</style>
```

##### 字间距

通过设置 ```android:letterSpacing``` 这个属性就可以非常方便的设置水平方向文本的字间距。

```java
// 在XML中：
android:letterSpacing="0.05"
// 在代码中动态设置，如下：
textView.setLetterSpacing(0.05);
```

## Popup Window 控件

PopupWindow 是一个可以在 Activity 之上显示任意 View 的控件。在 Android 经常使用，效果跟 Dialog 效果类似，不同点在于可以控制显示的位置，比如底部显示等。

特性：浮动弹出自定义窗体，并可设置弹出位置。

方法名称|描述
---|---
PopupWindow|构造函数，常用参数表：contentView – 弹窗界面内容 width – 弹窗宽度 height – 弹窗高度 focusable – 能否聚焦
setTouchable|是否支持点击操作
showAtLocation|按指定位置弹出显示自定义视图
showAsDropDown|下拉弹出显示自定义视图

### 定义弹出的布局

这里采用新建布局文件 XML 的形式添加弹出控件：（以登录界面 DEMO 为例）：

此处新建了一个 popup_content.xml 的布局文件：

[![popupwindow.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/popupwindow.jpg)](https://up.media.everdo.cn/image/P7OB)

并在里面添加了两组按钮。

[![popupwindow1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/popupwindow1.jpg)](https://up.media.everdo.cn/image/PRnt)

```java
PopupWindow regWindow = new PopupWindow(regView, LinearLayout.LayoutParams.MATCH_PARENT,LinearLayout.LayoutParams.WRAP_CONTENT,true);
```

上述代码设置了弹出 regView 的界面，宽高自适应父容器，允许聚焦。

#### LayoutInflater 作用及使用

作用：
1. 对于一个没有被载入或者想要动态载入的界面, 都需要使用 inflate 来载入. 
2. 对于一个已经载入的 Activity，就可以使用实现了这个 Activiyt 的findViewById 方法来获得其中的界面元素。

LayoutInflater 这个类的作用类似于 findViewById(),不同点是 LayoutInflater 是用来找 layout 下 xml 布局文件，并且实例化！而 findViewById() 是找具体 xml 下的具体 widget 控件。

最简单的使用方法：

```java
View regView = LayoutInflater.from(MainActivity.this).inflate(R.layout.popup_content,null,false);
```

LayoutInflater.from 从给定的上下文获取 LayoutInflater。

.inflate 方法从指定的 xml 资源中添加新的视图层次结构。InflateException 如果有错误则抛出。最后该方法会返回一个 View。

第一个参数 resource	int：要加载的XML布局资源的 ID（例如，R.layout.main_page）。第二个参数 root ViewGroup：作为生成层次结构的父级的可选视图，此值可能是 null。第三个参数 boolean attachToRoot 控制是否将第一个参数所指定的 View 添加到 root 中。

### 设置允许触摸

```java
regWindow.setTouchable(true);
```

### 设置弹出位置

- showAsDropDown(View anchor)：相对某个控件的位置（正左下方），无偏移
- showAsDropDown(View anchor,int xoff,int yoff)：相对某个控件的位置，有偏移
- showAtLocation(View parent,int gravity,int x,int y)：相对于父控件的位置（例如正中央Gravity.CENTER，下方Gravity.BOTTOM等），可以设置偏移或无偏移

```java
regWindow.showAtLocation(v, Gravity.BOTTOM,0, 0);
//regWindow.showAtLocation(getWindow().getDecorView(), Gravity.BOTTOM,0, 0);
```

到这一步的时候，点击右上角注册按钮，已经可以正常弹出注册对话框了。

[![popupwindow2.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/popupwindow2.jpg)](https://up.media.everdo.cn/image/Pjqx)

修改样式加以美化：

[![popupwindow3.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/popupwindow3.jpg)](https://up.media.everdo.cn/image/PoXI)

### 添加动画（参考网络）

首先在 res/src 下创建 anim 文件夹

创建 pophide.xml 隐藏时的动画参数

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    
     <translate
        android:duration="1000"
        android:fromYDelta="0"
        android:toYDelta="50%p" />

    <alpha
        android:duration="1000"
        android:fromAlpha="1.0"
        android:toAlpha="0.0" />
</set>
```

创建 popshow.xml 显示时的动画

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
     <translate
        android:duration="1000"
        android:fromYDelta="100%p"
        android:toYDelta="0" />

    <alpha
        android:duration="1000"
        android:fromAlpha="0.0"
        android:toAlpha="1.0" />
</set>
```

然后在主题配置文件 style.xml 里创建

 <!-- 设置pop由下自上的动画 -->
<style name="mypopwindow_anim_style">
        <item name="android:windowEnterAnimation">@anim/popshow_anim</item>
        <!-- 指定显示的动画xml -->

        <item name="android:windowExitAnimation">@anim/pophidden_anim</item>
        <!-- 指定消失的动画xml -->
</style>

最后在activity中调用

```java
// 设置popWindow的显示和消失动画
popupWindow.setAnimationStyle(R.style.mypopwindow_anim_style);
```

[![popupwinow.gif](https://media.everdo.cn/tank/pic-bed/2020/04/09/popupwinow.gif)](https://up.media.everdo.cn/image/PF4X)

## AlertDialog 控件

AlertDialog 用于弹出警告窗体，提示重要信息，提示用户再次确认操作。可设置确认、取消按钮等事件。

### AlertDialog 窗体的常用方法

方法名称|描述
---|---
show|显示警告窗体
isShowing|判断警告窗体是否处于显示状态
setTitle|设置警告窗体标题
setIcon|设置图标
setMessage|设置警告内容正文
setButton|设置操作按钮

### AlertDialog.Builder 构造器的常用方法

方法名称|描述
---|---
AlertDialog.Builder|警告窗体构造器的构造函数
builder.create|创建警告窗体

### DEMO

这里我们为登录案例的退出按钮添加一个警告对话框，在创建监听器后，编写警告窗体实例：

```java
public void onClick(View v) {
    //创建警告窗体实例
    AlertDialog quitConfirm = new AlertDialog.Builder(MainActivity.this).create();
    //设置内容
    quitConfirm.setIcon(R.drawable.close);
    quitConfirm.setMessage("您确定要离开么？");
    quitConfirm.setButton(AlertDialog.BUTTON_POSITIVE, "确认", new DialogInterface.OnClickListener() {
        @Override
        public void onClick(DialogInterface dialog, int which) {
        //确认按钮后执行的内容
            android.os.Process.killProcess(android.os.Process.myPid()); //退出程序代码
        }
    });
    quitConfirm.setButton(AlertDialog.BUTTON_NEGATIVE, "取消", new DialogInterface.OnClickListener() {
        @Override
        public void onClick(DialogInterface dialog, int which) {
            //点击取消后执行的代码
        }
    });
    quitConfirm.show();
}
```

运行效果：

[![AlertDialog.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/09/AlertDialog.jpg)](https://up.media.everdo.cn/image/P3bi)

点击退出后，整个 APP 退出。

## 自定义对话框 CustomDialog

如果 AlertDialog 不能满足一些较为复杂的程序设计需求，那么可以使用 CustomDialog 进行高级的定制：

> 开发者可以设计继承于 android.app.Dialog 的自定义对话框派生类（有时习惯命名为 CustomDialog）来弹出自定义界面的对话框，用户可在对话框进行下一步操作输入输出界面、操作按钮事件等均可自定义

### 常用方法

方法|描述
---|---
构造函数|实例化过程中的初始化程序，可自定义参数表传入用户自定义参数
onCreate|对话框初始化
show|显示对话框

简单的自定义对话框类的成员结构 (类名：CustomDialog)：

```java
//构造函数：

CustomDialog(Context context, String content, CustomDialog.OnCustomDialogListener customDialogListener)
```

```java
//按钮事件功能的定义：

interface OnCustomDialogListener {
    public void func1(String data); //回调功能
    public void func2(String data); //回调功能
    //可以定义一个或多个回调功能…
}
```

```java
//初始化：

onCreate(Bundle savedInstanceState) {
    …
    setContentView(R.layout.custom_dialog);  //调用自定义对话框布局设置 
    …    
    //按钮1单击事件调用customDialogListener.func1功能
    //按钮2单击事件调用customDialogListener.func2功能
    …
} 
```

对自定义对话框类的调用：
```java
CustomDialog dialog = new CustomDialog(MainActivity.this,"对话框提示内容",
     new CustomDialog.OnCustomDialogListener() {
        @Override
        public void func1(String data) { … }  //编写按钮1的事件实现程序
        @Override
        public void func1(String data) { … }  //编写按钮2的事件实现程序
    }
);  //自定义对话框的实例化

dialog.show();  //显示自定义对话框
```

### 添加布局设计

在 res/layout 下新建 custom_dialog.xml

[![custom_dialog_layout.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_layout.jpg)](https://up.media.everdo.cn/image/PA04)

绘制用户协议的基本布局：

[![custom_dialog_tos.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_tos.jpg)](https://up.media.everdo.cn/image/PDLM)

### 新增自定义类

这里创建一个 CustomDialog 的派生类

[![custom_dialog_class.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_class.jpg)](https://up.media.everdo.cn/image/PYFY)

```java
package com.emptinessboy.logindemo;

import android.app.Dialog;

public class customDialog extends Dialog {  //这里我们将这个自定义类继承于 android.app.Dialog
    
}
```

### 生成方法

[![custom_dialog_constructor.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_constructor.jpg)](https://up.media.everdo.cn/image/Pbma)

这里我们使用系统自带模板生成构造函数：

[![custom_dialog_constructor1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_constructor1.jpg)](https://up.media.everdo.cn/image/Pi73)

[![custom_dialog_constructor2.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_constructor2.jpg)](https://up.media.everdo.cn/image/PrqG)

同时用生成器生成一个重载的方法 onCreat()

[![custom_dialog_constructor3.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/10/custom_dialog_constructor3.jpg)](https://up.media.everdo.cn/image/PQX9)

```java
package com.emptinessboy.logindemo;

import android.app.Dialog;
import android.content.Context;
import android.os.Bundle;

import androidx.annotation.NonNull;

public class customDialog extends Dialog {

    public customDialog(@NonNull Context context) {
        super(context); //生成的构造函数
    }

    @Override
    //onCreate()用作对话框的初始化
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); //生成的方法重载

        setContentView(R.layout.custom_dialog); //调用样式

    }

}
```

最后完整的代码 custonDialog 类代码：

```java
public class customDialog extends Dialog {

    private onCustomDialogListener CustomDialogListener;    //将实例化的对象保存

    public customDialog(@NonNull Context context,onCustomDialogListener CustomDialogListener) { //第二个参数用来传入已经实例化的对象
        super(context); //生成的构造函数
        this.CustomDialogListener = CustomDialogListener;
    }

    //用于调用的接口
    public interface onCustomDialogListener {
        //定义回调事件
        //按钮点击事件
        public void buttonConfirmTosClicked();

    }

    @Override
    //onCreate()用作对话框的初始化
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); //生成的方法重载

        setContentView(R.layout.custom_dialog); //调用样式
        
        Button buttonConfirmTos = findViewById(R.id.buttonConfirmTos);
        buttonConfirmTos.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                CustomDialogListener.buttonConfirmTosClicked(); //此处回调接口的方法，具体触发的事件由接口在主函数中定义
            }
        });
    }

}
```

#### 禁用EditText（DEMO）

代码如下

```java
editText.setEnabled(false);//简单粗暴

editText.setFocusable(false);//不可编辑
editText.setFocusableInTouchMode(false);//触摸不可编辑
editText.setKeyListener(null);//不可粘贴，长按不会弹出粘贴框
editText.setClickable(false);//不可点击，但是这个效果我这边没体现出来，不知道怎没用
```

因此修改后增加下面的代码：(在自定义类的 onCreat方法中)：

```java
//这段代码定义了宽度
Window window = this.getWindow();
WindowManager.LayoutParams lp = window.getAttributes();
lp.width = WindowManager.LayoutParams.MATCH_PARENT;
lp.height = 1800;
this.getWindow().setAttributes(lp);

EditText tos = findViewById(R.id.Tos);
tos.setFocusable(false);//不可编辑
```

那么现在要做的就是从主函数调用接口了，在主函数中，使用 regTos 函数进行调用。调用过程中需要创建一个继承类：

```java
void regTos(){
    //调用customDialog
    customDialog dialog = new customDialog(MainActivity.this, new tosConfirm());
    dialog.show();
}

public class tosConfirm implements customDialog.onCustomDialogListener{
    public void buttonConfirmTosClicked() {
        Toast.makeText(MainActivity.this,"需要先同意协议才能注册哦！",Toast.LENGTH_SHORT).show();
    }
}
```

#### 回调参数（DEMO）

这里还需要增加是否阅读协议的判断，可以为接口添加传入参数：

先修改接口
```java
这里是 custonDialog 类 接口部分

//用于调用的接口
public interface onCustomDialogListener {
    //定义回调事件
    //按钮点击事件
    public void buttonConfirmTosClicked(boolean isRead);
}

......

下面是 custonDialog 类按钮监听事件下的 OnCreat 函数部分

public void onClick(View v) {
    CheckBox checkBoxConfirmTos = findViewById(R.id.checkBoxConfirmTos);
    boolean isRead = false;
    if(checkBoxConfirmTos.isChecked())
        isRead = true;
    CustomDialogListener.buttonConfirmTosClicked(isRead); //此处回调接口的方法，具体触发的事件由接口在主函数中定义
}

```

这里是 MainActivity 修改回调传入参数部分：

```java
void regTos(){
    //调用customDialog
    customDialog dialog = new customDialog(MainActivity.this, new tosConfirm());
    dialog.show();
}

public class tosConfirm implements customDialog.onCustomDialogListener{
    @Override
    public void buttonConfirmTosClicked(boolean isRead) {
        if(isRead){
            Toast.makeText(MainActivity.this,"注册还没开放哦！",Toast.LENGTH_SHORT).show();
        }
        else{
            Toast.makeText(MainActivity.this,"需要先同意协议才能注册哦！",Toast.LENGTH_SHORT).show();
        }
    }
}
```

最终完成效果：

[![loginfinish.gif](https://media.everdo.cn/tank/pic-bed/2020/04/10/loginfinish.gif)](https://up.media.everdo.cn/image/PxHj)
