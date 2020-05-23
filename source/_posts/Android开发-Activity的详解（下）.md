---
title: Android开发 Activity的详解（下）
date: 2020-04-19 12:46:09
category: Android
tags: 安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/04/android.png
---

## Activity 的启动模式

在 Android 中每个界面都是一个 Activity，切换界面操作其实是多个不同 Activity 之间的实例化操作。在 Android 中 Activity 的启动模式决定了 Activity 的启动运行方式。

Activity启动模式设置（src/main/AndroidManifest.xml）：

```xml
<activity android:name=".MainActivity" android:launchMode="standard" />
```

Activity 的四种启动模式：

1.Standard 2.singleTop 3.singleTask 4.singleInstance

### Standard 默认模式

默认启动模式，每次激活 Activity 时都会创建 Activity，并放入任务栈中。

**实验：**

创建一个全新的应用程序，在 MainActivity 添加一个按钮，点击后的 Intent 为再启动一个 MainActivity。

```java
public class MainActivity extends AppCompatActivity {

    private static final String TAG = "MainActivity";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Log.d(TAG, "onCreate: "+MainActivity.this.toString());

        Button buttonGo = findViewById(R.id.buttonGo);
        buttonGo.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //点击按钮后再启动一个 MainActivity
                Intent intent = new Intent(MainActivity.this,MainActivity.class);
                startActivity(intent);
            }
        });
    }
}
```

运行后，不断点击按钮测试：

[![StandardMode.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/StandardMode.jpg)](https://up.media.everdo.cn/image/IPJ9)

可以看到输出的日志中，每次启动的 MainActivity 的编号都不一样，意味着每次都有新的 MainActivity 被放入栈中。

### singleTop 栈顶模式

如果在任务的栈顶正好存在该 Activity 的实例， 就重用该实例，否者就会创建新的实例并放入栈顶（即使栈中已经存在该 Activity 实例，只要不在栈顶，都会创建实例）。 


> singleTop模式分3种情况:
> 
> 当前栈中已有该 Activity 的实例并且该实例位于栈顶时，不会新建实例，而是复用栈顶的实例，并且会将 Intent 对象传入，回调 onNewIntent 方法
> 
> 当前栈中已有该 Activity 的实例但是该实例不在栈顶时，其行为和 standard 启动模式一样，依然会创建一个新的实例
> 
> 当前栈中不存在该 Activity 的实例时，其行为同 standard 启动模式

**实验：**

修改 Manifest：

```xml
<activity android:name=".MainActivity" android:launchMode="singleTop">
```

重复之前的点击按钮，启动当前 Activity

[![SingleTop.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/SingleTop.jpg)](https://up.media.everdo.cn/image/IIej)

这次并不会有 Activity 切换的动画，并且日志不再输出。

进一步试验，我们创建了 SecondActivity，在 SecondActivity 添加按钮，事件为打开 MainActivity。

[![SingleTop.gif](https://media.everdo.cn/tank/pic-bed/2020/04/19/SingleTop.gif)](https://up.media.everdo.cn/image/Ih1O)

可以看到，因为在启动 SecondActivity 后，处于栈顶端的就不是 MainActivity 了，因此当点击 SecondActivity 的按钮启动 MainActivity 的时候，就又被 onCreat 了一个新的 Activity。

### singleTask 单任务模式

如果在栈中已经有该 Activity 的实例，就重用该实例。重用时，会让该实例回到栈顶，因此在**它上面的实例将会被移除栈**。如果栈中不存在该实例，将会创建新的实例放入栈中。 

**实验：**

为 MainActivity 添加 onRestart 重写方法，打印日志。再为 SecondActivity 添加 onDestory 重写方法，打印被销毁日志，

在没有改变 Manifest 之前，还是和以前一样，只有 onCreat 信息被打印。

而在改变 MainActivity 为 singleTask 后，可以看到点击 SecondActivity 的按钮启动 MainActivity 时，因为之前有 MainActivity 在栈中，因此 SecondActivity 被挤出栈了。

[![SingleTask.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/SingleTask.jpg)](https://up.media.everdo.cn/image/Ina6)

### singleInstance 模式

**！！不同于前面的所有模式，但凡使用 singleInstance 模式的 Activity 在实例化的时候，安卓都会为其独立创建一个全新的栈。**

在一个新栈中创建 Activity 实例，并让多个应用共享栈中的唯一这个 Activity 实例。任何应用再激活该 Activity 时，都会重用该栈中的实例，其效果相当于多个应用程序共享一个Activity。

一旦此模式的 Activity 的实例存在于某个栈中，任何应用再激活改 Activity 时都会重用该栈中的实例，其效果相当于多个应用程序共享一个应用，不管谁激活该 Activity 都会进入同一个应用中。

**实验：**

我们创建 MainActivity SecondActivity ThirdActivity，然后将 SecondActivity 设置为 singleInstanse 模式。

```xml
<activity android:name=".ThirdActivity" android:label="ThirdActivity" />
<activity android:name=".SecondActivity" android:label="SecondActivity" android:launchMode="singleInstance"/>
<activity android:name=".MainActivity" android:label="MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

最后设置在每个 APP 启动后，都使用 log 输出对应的 TaskID

```java
Log.d(TAG, "TaskID: "+getTaskId());
```

运行 APP 并点击按钮切换的效果如下图：

[![SingleInstance.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/SingleInstance.jpg)](https://up.media.everdo.cn/image/IBAn)

可以看到，MainActivity 和 ThirdActivity 因为是默认启动模式，所以使用同一个栈。而 SecondActivity 使用了一个新的栈。

这里用一个动图完整呈现过程，在依次开启三个 Activity 后，点击返回键直到 APP 退出。

[![SingleInstance.gif](https://media.everdo.cn/tank/pic-bed/2020/04/19/SingleInstance.gif)](https://up.media.everdo.cn/image/IRES)

可以看到，出栈顺序是先 **ThirdActivity --> MainActivity --> SecondActivity**

也就是说，主栈先全部出栈了，singleInstance 才进行出栈。

## 补充：extends 和 implements

> 补充： implements 与 Extends 的不同在于，extends 可以实现父类，也可以调用父类初始化  this.parent()。而且会覆盖父类定义的变量或者函数。implements 实现父类，子类不可以覆盖父类的方法或者变量。即使子类定义与父类相同的变量或者函数，也会被父类取代掉。
> 
> 这样的好处是：架构师定义好接口，让工程师实现就可以了。整个项目开发效率和开发成本大大降低。
> 
> 若同时用到 extends 和 implements 的时候，extends 必须放在 implements 关键字之前。如： class A extends B implements C.

## 完善 Demo

这里完善之前的登录界面 DEMO，用新学的 Activity 相关知识增加注册页面。此 demo 之前的部分参考我前面的文章。

先创建一个新的 RegActivity，修改其对应的布局文件。

[![e65a1f8ed51f9b9cdbbe96fe0d3a5992.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/20/e65a1f8ed51f9b9cdbbe96fe0d3a5992.jpg)](https://up.media.everdo.cn/image/IjZQ)

### 难点 使用另一个 Style

因为设计注册界面时，希望能够保留顶栏 ActionBar，因此与主界面在主题上需要做分离：(这里将首页的沉浸式布局独立出来)

Manifest 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.emptinessboy.logindemo">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity
            android:name=".Register"
            android:label="用户注册"/>
        <activity android:name=".MainActivity" android:theme="@style/FullPageTheme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

重写两个独立的 Style，AppTheme 为带 ActionBar 的，FullPageTheme 为不带 ActionBar 的。

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <!-- 有ActionBar的主题-->
    <!-- Customize your theme here. -->
    <item name="colorPrimary">@color/colorPrimaryNormal</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDarkNormal</item>
    <item name="colorAccent">@color/colorAccentNormal</item>
</style>

<style name="FullPageTheme" parent="Theme.AppCompat.Light.NoActionBar">
    <!-- Customize your theme here. -->
    <item name="colorPrimary">@color/colorPrimary</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
    <item name="colorAccent">@color/colorAccent</item>

    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
    <item name="android:windowTranslucentStatus">true</item>
    <item name="android:windowDrawsSystemBarBackgrounds">true</item>
    <item name="android:statusBarColor">@android:color/transparent</item>
</style>
```

完成后效果：

[![1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/20/1.jpg)](https://up.media.everdo.cn/image/I2RJ)

### 难点 返回时自动关闭弹窗

接下来在 MainActivity 新建对象，实例化 customDialog 和 PopupWindow：

```java
public class regdiaLog{
    customDialog dialog;
    PopupWindow regWindow;
    int regCode;
}
```

之所以实例化的原因是为了在后面 Activity 返回的时候，自动关闭这些弹窗。关闭这两个弹窗的方法，这里采用了重写 onPause() 方法：

```java
@Override
protected void onPause() {
    super.onPause();
    regdialog.dialog.dismiss();
    regdialog.regWindow.dismiss();
}
```

运行效果（进入下个 Activity 之前，弹窗已经自动关闭）：

[![7598843e1898a6be52f51c069977c591.gif](https://media.everdo.cn/tank/pic-bed/2020/04/20/7598843e1898a6be52f51c069977c591.gif)](https://up.media.everdo.cn/image/IDJl)

接下来，继续完善点击右上角注册按钮后的代码：

```java
//注册按钮
Button buttonReg = findViewById(R.id.buttonReg);
buttonReg.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        View regView = LayoutInflater.from(MainActivity.this).inflate(R.layout.popup_content,null,false);
        regdialog.regWindow = new PopupWindow(regView, LinearLayout.LayoutParams.MATCH_PARENT,LinearLayout.LayoutParams.WRAP_CONTENT,true);
        regdialog.regWindow.setTouchable(true);
        regdialog.regWindow.setAnimationStyle(R.style.pop_anim);
        regdialog.regWindow.showAtLocation(v, Gravity.BOTTOM,0, 0);
        //绑定popupWindow的视图对象
        Button buttonUseEmail = regView.findViewById(R.id.buttonUseEmail);
        regdialog.dialog  = new customDialog(MainActivity.this, new tosConfirm());
        buttonUseEmail.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //调用customDialog
                regdialog.regCode=1;//注册方式1
                regdialog.dialog.show();
            }
        });
        Button buttonUseName = regView.findViewById(R.id.buttonUseName);
        buttonUseName.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //调用customDialog
                regdialog.regCode=2;//注册方式2
                regdialog.dialog.show();
            }
        });
    }
});
```

重点：regdialog.dialog.show(); 之后，当用户点击同意用户协议后，需要跳转到 Register 类：

这里使用 Intent 跳转，并携带整数（传递用户的注册方式，邮箱或用户名）

```java
public class tosConfirm implements customDialog.onCustomDialogListener{
    @Override
    public void buttonConfirmTosClicked(boolean isRead) {
        if(isRead){
            Intent reg = new Intent(MainActivity.this,Register.class);
            reg.putExtra("mode",regdialog.regCode); //传递注册方式
            startActivity(reg);
            //Toast.makeText(MainActivity.this,"注册还没开放哦！",Toast.LENGTH_SHORT).show();
        }
        else{
            Toast.makeText(MainActivity.this,"需要先同意协议才能注册哦！",Toast.LENGTH_SHORT).show();
        }
    }
}
```

Registart.java 里面需要对注册进行处理，这里预先定义了存放用户名密码的类 USER_POOL.AddUser(u,p) 这里直接调用；此外，这之前还额外定义了 popUpWndow 的样式：

```java
Button reg = findViewById(R.id.buttonReg);
reg.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        EditText editTextEmail = findViewById(R.id.editTextEmail);
        EditText editTextPassword = findViewById(R.id.editTextPassword);
        try {
            String u = editTextEmail.getText().toString();
            String p = editTextPassword.getText().toString();
            if (u.length()<3||p.length()<6){

                View regView = LayoutInflater.from(Register.this).inflate(R.layout.popup_regfail,null,false);
                TextView err = regView.findViewById(R.id.textViewReg);

                //透过 popUpWindow 的样式文件进行查找 ID

                err.setText("注册失败,用户名或密码太短");
                final PopupWindow regResult = new PopupWindow(regView, LinearLayout.LayoutParams.MATCH_PARENT,LinearLayout.LayoutParams.WRAP_CONTENT,true);
                regResult.setTouchable(true);
                regResult.setAnimationStyle(R.style.pop_anim);
                regResult.showAtLocation(v, Gravity.BOTTOM,0, 0);

            }else{
                USER_POOL.AddUser(u,p); //新增用户名密码

                View regView = LayoutInflater.from(Register.this).inflate(R.layout.popup_regsuccess,null,false);
                final PopupWindow regResult = new PopupWindow(regView, LinearLayout.LayoutParams.MATCH_PARENT,LinearLayout.LayoutParams.WRAP_CONTENT,true);
                regResult.setTouchable(true);
                regResult.setAnimationStyle(R.style.pop_anim);
                regResult.showAtLocation(v, Gravity.BOTTOM,0, 0);

                //倒计时函数
                CountDownTimer timer = new CountDownTimer(2000, 10) {
                    @Override
                    public void onTick(long millisUntilFinished) {
                    }
                    @Override
                    public void onFinish() {
                        finish();   //自动回到登录界面
                    }
                };
                timer.start();
            }

        } catch (Exception e) {
            //此处省略
                }
            }
        });
    }
```

简易的通过字符串数组存放密码的用户类，临时存放用户名密码（测试用途，数据不能持久化，正常使用应该用数据库，或者将请求发送到服务器）

```java
public final class UserPool {
    private static final String[][] UserPass = new String[100][2];
    
    private int index = -1;
    UserPool(){
        AddUser("hxf","123456");
    }
    void AddUser(String u,String p){    //增加用户函数
        index++;
        UserPass[index][0]=u;
        UserPass[index][1]=p;
    }
    boolean Login(String u,String p){ //登录函数
        for(int i=0;i<=index;i++){
            if( u.equals(UserPass[i][0]) && p.equals(UserPass[i][1]) ){
                return true;
            }
        }
        return false;
    }
}
```

### 难点 通过非当前 View 查找 id

透过 popUpWindow 的样式文件进行查找 ID

此举主要是动态修改（通过外挂布局定义的 popUpWindow）注册成功或失败弹出的提示文字而不需要重写创建布局文件。

```java
View regView = LayoutInflater.from(Register.this).inflate(R.layout.popup_regfail,null,false);
TextView err = regView.findViewById(R.id.textViewReg);
//透过 popUpWindow 的样式文件进行查找 ID
err.setText("注册失败,用户名或密码太短");
```

当然，基础的布局还是要定义的

[![e8540353413f94020ef3f8a27f717747.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/20/e8540353413f94020ef3f8a27f717747.jpg)](https://up.media.everdo.cn/image/IFWy)

这一步实现效果：

[![1068a93b8d1db89f0c135d09886fccc2.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/20/1068a93b8d1db89f0c135d09886fccc2.jpg)](https://up.media.everdo.cn/image/I3Sd)

### 难点 倒计时关闭 Activity

此举主要是实现注册成功后自动返回主界面以增强用户体验，注册失败则留在原地不动。

```java
//倒计时函数
CountDownTimer timer = new CountDownTimer(2000, 10) {
    @Override
    public void onTick(long millisUntilFinished) {
    }
    @Override
    public void onFinish() {
        finish();   //自动回到登录界面(倒计时结束执行的代码)
    }
};
timer.start();
```

实现效果：

[![db9d73168a853f2ffd38fa82025f3aff.gif](https://media.everdo.cn/tank/pic-bed/2020/04/20/db9d73168a853f2ffd38fa82025f3aff.gif)](https://up.media.everdo.cn/image/IVe0)

### 难点 自动关闭软键盘

这里我搬运了网上 dalao 的代码，自己水平不够，暂时先不自己造轮子了：

```java
package com.emptinessboy.logindemo;

import android.app.Activity;
import android.content.Context;
import android.os.IBinder;
import android.view.MotionEvent;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.widget.EditText;

public class HideKeyBroadUtils {

    private HideKeyBroadUtils(){

    }

    /**
     * 隐藏软键盘
     * @param activity
     * @param ev
     */
    public static void hide(Activity activity, MotionEvent ev){
        if (ev.getAction() == MotionEvent.ACTION_DOWN) {
            View view = activity.getCurrentFocus();
            if (isHideInput(view, ev)) {
                HideSoftInput(activity,view.getWindowToken());
            }
        }
    }

    // 判定是否需要隐藏
    private static boolean isHideInput(View v, MotionEvent ev) {
        if (v != null && (v instanceof EditText)) {
            int[] l = { 0, 0 };
            v.getLocationInWindow(l);
            int left = l[0], top = l[1], bottom = top + v.getHeight(), right = left
                    + v.getWidth();
            if (ev.getX() > left && ev.getX() < right && ev.getY() > top
                    && ev.getY() < bottom) {
                return false;
            } else {
                return true;
            }
        }
        return false;
    }
    // 隐藏软键盘
    private static void HideSoftInput(Activity activity, IBinder token) {
        if (token != null) {
            InputMethodManager manager = (InputMethodManager)
                    activity.getSystemService(Context.INPUT_METHOD_SERVICE);
            manager.hideSoftInputFromWindow(token,
                    InputMethodManager.HIDE_NOT_ALWAYS);
        }
    }
}
```

使用这个类的方法很简单：

```java
只需重写 activity 里的 dispatchTouchEvent 方法，然后调用如下
@Override
public boolean dispatchTouchEvent(MotionEvent ev){
        HideKeyBroadUtils.hide(this,ev);
        return super.dispatchTouchEvent(ev);
}
```

实现效果：

[![b3f81e805d8d2ed98cd95b625b21510b.gif](https://media.everdo.cn/tank/pic-bed/2020/04/20/b3f81e805d8d2ed98cd95b625b21510b.gif)](https://up.media.everdo.cn/image/IYMD)
