---
title: Android开发 Activity的详解（上）
date: 2020-04-18 16:16:51
category: Android
tags: 安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/04/android.png
---

## Activity 的传值

### 方法一：直接把数据添加到 Intent 对象

先将数据添加到 Intent 对象，第二个界面再把数据从 Intent 中取出来。

1.MainActivity 启动 SecondActivity，传递 extra_data：
<!--more-->

```java
String data="Hi, SecondActivity";
Intent intent=new Intent(MainActivity.this,SecondActivity.class);
//向intent对象添加数据
intent.putExtra("extra_data ", data );
startActivity(intent);
```

> ```putExtra("A",B)``` 中，AB为键值对，第一个参数为键名，第二个参数为键对应的值。

2.在 SecondActivity 接收 extra_data：

```java
//获取Intent对象
Intent intent=getIntent();
//获取传递过来的String类型的数据
String data=intent.getStringExtra("extra_data ");
```

> ```getStringExtra("A")``` 中，参数 A 为上一个 Activity 传递的键名。

#### 实验：

新建 App，在主界面添加一个按钮，随后设置如下点击事件：

```java
//MainActivity部分代码
Button buttonGoTransfer = findViewById(R.id.buttonGoTransfer);
buttonGoTransfer.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        String data="Hi,I am EmptinessBoy!";
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        intent.putExtra("hello",data);
        startActivity(intent);
    }
});
```

在第二个页面获取 Intent

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_second);
    Intent intent = getIntent();
    String hello = intent.getStringExtra("hello");
    Toast.makeText(SecondActivity.this,hello,Toast.LENGTH_SHORT).show();
}
```

运行效果：

启动 Activity 并传递参数：

[![Activity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/Activity.jpg)](https://up.media.everdo.cn/image/PSUk)

SecondActivity 接收到参数并使用 Toast 显示：

[![SecondActivity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/SecondActivity.jpg)](https://up.media.everdo.cn/image/PC9Z)

### 方法二：把数据添加到 Bundle（大篮子）对象

由于第一种方法，每次传递数据都需要存入取出，在多个 Activity 中连续传递时会显得很麻烦。如图：

[![a535232df7aada6dd334099c8a797beb.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/a535232df7aada6dd334099c8a797beb.jpg)](https://up.media.everdo.cn/image/PtBB)

因此使用 Bundle 可以很好的解决这个问题

Bundle 类用作携带数据，它类似于 Map，用于存放 key-value 名值对形式的值

1.MainActivity 向 SecondActivity 传递 bubdle 对象：

```java
//实例化bundle对象
Bundle bundle = new Bundle();
//向bundle对象添加数据
bundle.putString("name", "张三" );
bundle.putInt("age", 20);
Intent intent = new Intent(MainActivity.this,SecondActivity.class);
//向intent对象bundle
intent.putExtras(bundle);
startActivity(intent);
```

2.在 SecondActivity 接收 bubdle 对象：

```java
//获取bundle对象
Bundle bundle = getIntent().getExtras();
//通过key为“name”来获取value即 nameString.
String name=bundle.getString("name");
int age=bundle.getInt("age");
```

#### 实验：

修改上一个示例的按钮点击事件，使用 bundle 来传递多个数据：

```java
buttonGoTransfer.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Bundle bundle = new Bundle();
        bundle.putString("name","Emptinessboy");
        bundle.putInt("age",19);
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        intent.putExtras(bundle);
        startActivity(intent);
    }
});
```

SecondActivity 修改接收参数的方法并使用 Toast 显示：

```java
Intent intent = getIntent();
Bundle bundle = intent.getExtras();
String name = bundle.getString("name");
int age = bundle.getInt("age");
Toast.makeText(SecondActivity.this,"姓名："+name+" 年龄："+age,Toast.LENGTH_SHORT);
```

运行效果（bundle已经被正常传递）：

[![TransferSuccess.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/TransferSuccess.jpg)](https://up.media.everdo.cn/image/Pwxt)

## Activity 接收返回值

### **大致流程：**

1. MainActivity 通过调用 startActivityForResult() 跳转到 OtherActivity。
2. OtherActivity 在自己关闭之前，通过 setResult() 方法返回数据给 MainActivity。
3. MainActivity 通过复写 onActivityResult() 方法来取得回传值。

```java
首先在 MainActivity 中调用
startActivityForResult(Intent intent, int requestCode);
```

```java
然后在 SecondActivity 返回
setResult(int resultCode, Intent data);
```

```java
最后在 MainActivity 中调用接口来获取数值
onActivityResult(int requestCode, int resultCode, Intent data);
```

> 1、调用 startActivityForResult 方法可以开启一个获取返回值的 activity，在第一个 activity 中重写 onActivityResult 方法来接收返回的值。 
> 
> 2、请求码：请当同一个 activity 多次使用 startActivityForResult 方法获取返回值后，通过请求码 requestCode 来区分是哪次请求。
> 
> 3、结果码：当返回多个结果时，用来区分结果。


### 示例代码：

MainActivity：

```java
// 返回的结果码
public final static int REQUEST_CODE = 1; 
//创建intent对象
Intent intent=new Intent(this,OtherActivity.class);
//启动OtherActivity，并发送请求码
startActivityForResult(intent,REQUEST_CODE);
```

SecondActivity：

```java
EditText editText=findViewById(R.id.editText);
//数据是使用Intent返回
Intent intent = new Intent();
//把返回数据存入Intent
intent.putExtra("result", editText.getText().toString());
//设置返回数据
setResult(0,intent);
//关闭当前窗口
finish();
```

MainActivity 实现接口：

```java
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    ……
    switch (requestCode){
        case REQUEST_CODE:
            textView.setText(data.getStringExtra("result");break;
        default:
            result="未获取到数据。";
    }
}
```

#### 实验：

简单设计 MainActivity 的布局：

[![MainActivity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/MainActivity.jpg)](https://up.media.everdo.cn/image/PZJI)

编写代码：

```java
public class MainActivity extends AppCompatActivity {
    public final static int REQUEST_CODE = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button initSecAct = findViewById(R.id.buttonInitSecAct);
        initSecAct.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //发起需要结果的请求
                Intent intent = new Intent(MainActivity.this,SecondActivity.class);
                startActivityForResult(intent,REQUEST_CODE);
            }
        });
    }
}
```

简单设计 SecondActivity 的布局：

[![SecActivity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/SecActivity.jpg)](https://up.media.everdo.cn/image/P5dX)

编写代码：

```java
Button buttonSubAndBack = findViewById(R.id.buttonSubAndBack);
buttonSubAndBack.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        //获取输入文字
        EditText editTextTextPersonName = findViewById(R.id.editTextTextPersonName);
        String inputValue = editTextTextPersonName.getText().toString();
        //创建Intent
        Intent intent = new Intent();
        intent.putExtra("inputValue",inputValue);
        //返回intent
        setResult(1,intent);
        //返回上一级
        finish();
    }
});
```

返回 MainActivity 重写 onActivityResult()：

[![faf223ccc7575a190ac944ed61dc8b90.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/faf223ccc7575a190ac944ed61dc8b90.jpg)](https://up.media.everdo.cn/image/PG1i)

使用 IED 进行自动生成

[![1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/18/1.jpg)](https://up.media.everdo.cn/image/PKa4)

补全代码：

```java
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    TextView textViewHello = findViewById(R.id.textViewHello);
    switch (resultCode){
        case 1:
            textViewHello.setText(data.getStringExtra("inputValue"));
            break;
        default:
            textViewHello.setText("返回码异常");
            break;
    }
}
```

最后运行效果：

[![d0fc250f47624c10691abda9b78e1392.gif](https://media.everdo.cn/tank/pic-bed/2020/04/18/d0fc250f47624c10691abda9b78e1392.gif)](https://up.media.everdo.cn/image/POCx)

> 一般情况下不论有没有操作 SecondActivity 里的按钮，只要从这里返回了 MainActivity，接口都会返回相同的 requestCode。

## Activity 生命周期

Task 就是一个存放 Activity 栈 (A task is a stack of activities.) ，这个栈里面存放了很多 Activity ，它遵循着后进先出的原则。栈有两个动作：进栈（把对象压入到栈当中）和出栈（把栈中的第一个对象从栈里面拿出来）。

当我们将 Activity 创建好，放入栈中，先放的位于下方，后进入的位于上方。（顺序：先进后出）

### 四种状态

Activity在进栈与出栈的过程中，一般意义上有四种状态：

1. 【运行】当 Activity 位于栈顶时，此时正好处于屏幕最前方，此时处于运行状态；（最不会被系统回收）
2. 【暂停】当 Activity 失去了焦点但仍然部分可见（如栈顶的 Activity 是透明的或者栈顶 Activity 并不是铺满整个手机屏幕），此时处于暂停状态；（系统也不会轻易回收这样的活动，除非是内存极低的情况）
3. 【停止】当 Activity 被其他 Activity 完全遮挡，此时此 Activity 对用户不可见，此时处于停止状态；（内存中保留Activity对象，当内存较低时系统会回收这样的活动）
4. 【非活动】当 Activity 由于人为或系统原因（如低内存等）被销毁，此时处于销毁状态。

### 七个回调方法

在每个不同的状态阶段，Adnroid 系统对 Activity 内相应的方法进行了回调。因此，我们在程序中写 Activity 时，一般都是继承 Activity 类并重写相应的回调方法。

1. **onCreate()** 当Activity第一次被创建时调用，完成活动的初始化操作。
2. **onStart()** 当用户可以看到这个Activity时调用。
3. **onResume()** 当获得了用户的焦点时,就是用户点击了屏幕。
4. **onPause()** 当系统准备启动或回复另一个活动时调用。
5. **onStop()** 当活动完全不可见时调用，当新启动的活动是对话框式的，还处于可见时，该方法不会被调用。
6. **onDestroy()** 活动被销毁时调用。
7. **onRestart()** 当活动由停止状态变为运行状态时调用。

#### 示意图

[![Activity.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/Activity.jpg)](https://up.media.everdo.cn/image/P83M)

## 三种生命周期

**1.完整生命周期：** 活动在 onCreate() 方法和 onDestroy() 方法之间所经历的，就是完整生命周期。一般情况下，一个活动会在onCreate()方法中完成各种初始化， onDestroy()方法中完成释放资源的操作。

**2.前台生命周期：** 活动在 onResume() 方法和 onPause() 方法之间所经历的就是前台生命周期。在前台生命周期内，活动总是处于运行状态，此时的活动可以与用户进行交互。

**3.可视生命周期：** 活动在 onStart() 方法与 onStop() 方法之间所经历的，就是可视生命周期。在可视生命周期内，活动对于用户是可见的，但可能无法和用户进行交互。

[![Activityd7df6b607bd46a0b.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/Activityd7df6b607bd46a0b.jpg)](https://up.media.everdo.cn/image/PaEY)

### 实验

重写生命周期的方法，并打印输出日志

**完整生命周期实验：**

> 启动 Activity 后 onCreate() --> onStart() --> onResume()
> 按 Back 键 --> onPause() --> onStop() --> onDestroy()

[![4aa5dbc22c5e50176385722a1bc62063.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/4aa5dbc22c5e50176385722a1bc62063.jpg)](https://up.media.everdo.cn/image/PgUa)

这里重写了 HelloWorld程序 完整生命周期的所有方法

运行后，程序启动时打印了前三条日志，按下返回键后打印了后三条日志：

[![f7f1b1767ea717942071267daa914add.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/19/f7f1b1767ea717942071267daa914add.jpg)](https://up.media.everdo.cn/image/PuBs)

**前台生命周期实验：**

新建一个 TestActivity，并在 MainActivity 中设置按钮点击跳转。

在 AndroidManifest.xml 中，将第二个 Activity 的样式设为 dialog 对话框，来实现半遮挡效果：

```xml
<activity
    android:name=".TestActivity"
    android:theme="@style/Theme.AppCompat.Dialog"
    android:label="TestActivity"/>
```

运行程序测试：

[![2e5e7200f2bbd9af9aa3f8e992fce67e.gif](https://media.everdo.cn/tank/pic-bed/2020/04/19/2e5e7200f2bbd9af9aa3f8e992fce67e.gif)](https://up.media.everdo.cn/image/I4W3)

可以看到，当点击按钮后，MainActivity 被遮挡时，输出 onPause 的日志，按下返回键返回 MainActivity 时，输出 onResume 日志。 

**可视生命周期实验：**

不改变示例程序，我们在程序运行时呼入电话：

[![1.gif](https://media.everdo.cn/tank/pic-bed/2020/04/19/1.gif)](https://up.media.everdo.cn/image/IHCG)

可以看到：

```
2020-04-19 01:47:25.803 30014-30014/com.emptinessboy.testlifecycle D/MainActivity: onPause: 被暂停
2020-04-19 01:47:27.089 30014-30014/com.emptinessboy.testlifecycle D/MainActivity: onStop: 被停止
```

挂掉电话后则输出了（图略）：

```
2020-04-19 01:47:48.733 30014-30014/com.emptinessboy.testlifecycle D/MainActivity: onStart: 正在运行
2020-04-19 01:47:48.734 30014-30014/com.emptinessboy.testlifecycle D/MainActivity: onResume: 被重新开始
```
