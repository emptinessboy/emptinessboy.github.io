---
title: Android 开发UI和布局（上）
date: 2020-04-04 02:15:00
category: Android
tags:  安卓学习
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/04/android.png
---

[![uibujv.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/uibujv.jpg)](https://up.media.everdo.cn/image/JRl6)

## LinearLayout 布局

LinearLayout 是线性布局控件，它作为容器将其包含的子控件以横向或纵向的方式排列。

### 布局方向

[![LinearLayout-new.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/LinearLayout-new.jpg)](https://up.media.everdo.cn/image/J2fS)

子元素被排列成一行或一列，并使用 orientation 属性设置方向。horizontal 为横向水平排列，vertical 为垂直纵向排列

<!--more-->

### 布局定位：

- layout_gravity：元素在容器中的位置
- gravity：元素所包含的内容或子元素在元素中的位置。

<br>

### DEMO

下面是一个具体案例：

新建项目后，删除默认控件后，修改布局为 LinearLayout，

[![convert-linerlayout.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/convert-linerlayout.jpg)](https://up.media.everdo.cn/image/JFGQ)

然后将 LinerLayout 主界面设置为 vertical 纵向排列。

[![convert-linerlayout-ver.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/convert-linerlayout-ver.jpg)](https://up.media.everdo.cn/image/JAoJ)

尝试添加文本框部件，并修改默认显示文字 hint 属性值：

[![LinearLayout-text.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/LinearLayout-text.jpg)](https://up.media.everdo.cn/image/JDNy)

添加一个嵌套的 LinerLayout 布局（设置为 horizontal），并添加 button 控件：

[![linerlayout-button.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/linerlayout-button.png)](https://up.media.everdo.cn/image/JVtd)

至此，布局完成，模拟器显示界面和设计一致：

[![LinearLayout-ok.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/LinearLayout-ok.jpg)](https://up.media.everdo.cn/image/JbIl)

## RelativeLayout 布局

RelativeLayout 布局下，元素在相对位置显示，可避免嵌套，保持简洁的层次结构。

[![RelativeLayout.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/RelativeLayout.jpg)](https://up.media.everdo.cn/image/Jdr0)

### 相关属性

属性名称|描述
---|---
layout_alignParentTop|父元素顶部对齐（true）
layout_alignParentBottom|父元素底部对齐（true）
layout_alignParentStart|父元素左侧对齐（true）
layout_alignParentEnd|父元素右侧对齐（true）
layout_centerHorizontal|水平居中（true）
layout_centerVertical|垂直居中（true）
layout_marginTop|距离顶部
layout_marginBottom|距离底部
layout_marginStart|距离左侧
layout_marginEnd|距离右侧
layout_above|底部置于给定元素之上
layout_below|顶部置于给定元素之下
layout_alignTop|顶部与给定元素顶部对齐
layout_alignBaseline|baseline 与给定元素的 baseline 对齐
layout_alignBottom|底部与给定元素底部对齐
layout_alignStart|左侧对齐给定元素
layout_alignEnd|右侧对齐给定元素
layout_toStartOf|右侧对齐给定元素开始的位置
layout_toEndOf|左侧对齐给定元素结束的位置

### DEMO

下面是一个具体案例：

[![RelativeLayout-cj.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/RelativeLayout-cj.png)](https://up.media.everdo.cn/image/JeyD)

设定布局模式为 RelativeLayout 后，将上方工具栏的磁吸工具开启，然后向屏幕内拖放控件。

[![RelativeLayout-demo.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/RelativeLayout-demo.jpg)](https://up.media.everdo.cn/image/JilL)

调整完后，重新设置相对关系：

[![move.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/move.png)](https://up.media.everdo.cn/image/JQVc)

至此，布局完成，模拟器显示界面和设计一致：

[![RelativeLayout-run.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/RelativeLayout-run.jpg)](https://up.media.everdo.cn/image/Jqs2)

## FrameLayout 布局

FrameLayout 是帧布局控件，可以使子元素逐个叠加在栈中。（最后添加的元素位于视图的最上层，也可以理解为图层堆叠的形态）

两个属性:

- android:foreground:*设置改帧布局容器的前景图像
- android:foregroundGravity:设置前景图像显示的位置

[![FrameLayout.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/05/FrameLayout.jpg)](https://up.media.everdo.cn/image/JChG)

## View 控件（顶层）

View，TextView，Button 与 EditText 的关系：

[![view-tree.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/view-tree.jpg)](https://up.media.everdo.cn/image/J9hx)

[![view.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/view.jpg)](https://up.media.everdo.cn/image/JNkB)

### TextView 控件（父类）

显示文字，只读，可设置字体、字号、颜色、链接等样式。

[![textview.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/textview.jpg)](https://up.media.everdo.cn/image/J6ok)

#### EditText 控件（子类）

显示和编辑文字，可编辑，可设置软键盘类型。

[![eidt-text.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/eidt-text.jpg)](https://up.media.everdo.cn/image/Jktt)

## Button 控件（EditText 子类）

### 继承关系：

[![tree.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/tree.jpg)](https://up.media.everdo.cn/image/J1KY)

### 事件：

- 单击事件：通过触屏或鼠标点击按钮所激发的事件
- 长按事件：通过触屏或鼠标按下按钮控并保持不放开所激发的事件

单点事件定义方法：

- Button 控件提供了 onClick 属性
- 事件监听器绑定方法通过调用控件的 setOnClickListener 绑定相应方法

下面是一个具体案例：（简单 BMI 计算器）

先构造 UI 布局，这里采用了 LinerLayout 线性布局。然后向视图内摆放 UI 控件。（为了美观，可以设置下 LayoutMargin 进行布局排版）

[![bmi-creat.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/bmi-creat.png)](https://up.media.everdo.cn/image/JEQI)

这里需要将 textView 的 inputType 设置为 numberDecline 类型（软键盘类型，增强用户体验）

[![bmi-numberdecline.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/bmi-numberdecline.png)](https://up.media.everdo.cn/image/JcyX)

这里我们在 MainActivity.java 文件中编写我们的代码：

先构造一个简单的函数 btnCalBmi()，并将其绑定到 button 的 onClick 事件中。

[![bmi-onclick.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/bmi-onclick.png)](https://up.media.everdo.cn/image/JzY4)

我们把函数写完整：

```java
public void btnCalBmi(View v){
    //引用控件（定义两个变量）
    EditText inHeight = findViewById(R.id.inputHeight);
    EditText inWeight = findViewById(R.id.inputWeight);
    TextView textBmi = findViewById(R.id.textBmi);
    Double height = Double.parseDouble(inHeight.getText().toString());
    Double weight = Double.parseDouble(inWeight.getText().toString());
    //体质指数（BMI）=体重（kg）÷身高^2（m）
    //最理想的体重指数是22， BMI指数为18.5～23.9时属正常，具体分类如下：
    //过轻：低于18.5
    //正常：18.5-23.9
    //过重：24-27
    //肥胖：28-32
    //非常肥胖, 高于32
    Double bmi = weight/Math.pow(height/100,2);
    if(bmi<18.5){
        textBmi.setText("您的 MBI 为："+bmi+" 您的体型为有一丢丢瘦");
    }
    else if(bmi>=18.5&&bmi<24){
        textBmi.setText("您的 MBI 为："+bmi+" 您的体型为正常体型");
    }
    else if(bmi>=14&&bmi<28){
        textBmi.setText("您的 MBI 为："+bmi+" 您的体型为微微发胖");
    }
    else if(bmi>=18&&bmi<32){
        textBmi.setText("您的 MBI 为："+bmi+" 您的体型为肥胖！！");
    }
    else{
        textBmi.setText("您的 MBI 为："+bmi+" 您简直是一个超级大胖次！");
    }
}
```

这里补上一段使用事件监听的简单框架：

```java
Button Cal = findViewById(R.id.buttonCal);
Cal.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
    //之前函数 btnCalBmi(View v) 内的代码
    }
});
```

> OnClickListener 会比直接绑定按钮事件拥有更好性能。

[![bmi-function.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/bmi-function.png)](https://up.media.everdo.cn/image/Jfui)

到这里，我们就可以运行程序了，输入我的身高 178.5CM 体重 53.gKG，点击计算按钮后获得我的 BMI 为 16.79 （好吧，我偏瘦了，要多吃肉肉 /dog

[![bmiRun.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/04/bmiRun.jpg)](https://up.media.everdo.cn/image/J0sM)

### CompoundButton（Button 子类）

#### RadioButton（子类）

单项选择的实现，通过分组容器对 RadioButton 进行分组。

下面是上面 BMI计算器 案例的进阶：

[![raido-group.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/raido-group.png)](https://up.media.everdo.cn/image/Jvoa)

这里我们先创建 RadioGroup 组件，然后在 RadioGroup 中添加三个 RadioButton 按钮控件。

为了使选框进行横向排列，我们需要将 RadioGroup 的 orientation 设置为 horizontal。

我们在 btnCalBmi() 函数中新引入 RadioButton 控件。

```java
RadioButton asia = findViewById(R.id.stdAsia);
RadioButton who = findViewById(R.id.stdWho);
RadioButton cn = findViewById(R.id.stdCn);
```

使用 **```.isChecked()```** 方法来判断选框有没有选中。

改版后函数为：

```java
public void btnCalBmi(View v){
    //引用控件（定义两个变量）
    EditText inHeight = findViewById(R.id.inputHeight);
    EditText inWeight = findViewById(R.id.inputWeight);
    RadioButton asia = findViewById(R.id.stdAsia);
    RadioButton who = findViewById(R.id.stdWho);
    RadioButton cn = findViewById(R.id.stdCn);
    TextView textBmi = findViewById(R.id.textBmi);
    Double height = Double.parseDouble(inHeight.getText().toString());
    Double weight = Double.parseDouble(inWeight.getText().toString());
    //计算
    Double bmi = weight/Math.pow(height/100,2);
    //判断选中
    if(who.isChecked()){    
    //who标准
    else if(asia.isChecked()){
    //亚洲标准
    }
    else if(cn.isChecked()){
    //中国标准
    }
    else{
        textBmi.setText("请先选择一个标准！");
    }
}
```

编写完成后，调试应用程序：

[![bmi-plus.png](https://media.everdo.cn/tank/pic-bed/2020/04/04/bmi-plus.png)](https://up.media.everdo.cn/image/Jyks)

这时候如果没有输入身高体重，APP会闪退，这里修复空指针闪退，并添加重置功能：

```java
//空字符串问题修复
if(TextUtils.isEmpty(inHeight.getText().toString())){
    textBmi.setText("请输入身高！");
}
else if(TextUtils.isEmpty(inWeight.getText())){
    textBmi.setText("请输入体重！");
}
else{
    Double height = Double.parseDouble(inHeight.getText().toString());
    Double weight = Double.parseDouble(inWeight.getText().toString());
    calBmi(height,weight,textBmi);
}
```

```java
//重置按钮点击事件
Reset.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
    EditText inHeight = findViewById(R.id.inputHeight);
    EditText inWeight = findViewById(R.id.inputWeight);
    inHeight.setText("");
    inWeight.setText("");
    }
});
```

[![bmi_final.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/05/bmi_final.jpg)](https://up.media.everdo.cn/image/JTw3)

#### CheckBox（子类）

用处：核选项的实现，多项选择的实现。

使用方法和 radioButton 相似。使用 **```.isChecked()```** 方法来判断选框有没有选中

## Toast 控件

Toast 是消息提示控件，该控件用于弹出提示消息（小气泡），可设置弹出时间长度。

### 方法

方法名称|描述
---|---
makeText|定义消息内容
setGravity|设置布局位置（改变提示位置）
getView|获取Toast视图
show|显示

### 简单样例

纯文字提示代码示例：

```java
Toast.makeText(MainActivity.this,"提示文字",Toast.LENGTH_SHORT).show();
```

makeText 方法分别调用了三个参数，分别传入运行对象，显示内容，和停留时长

setGravity 方法并不直接返回 Toast 对象，所以没法使用链式方法。

```java
Toast sg = Toast.makeText(MainActivity.this,"请输入身高",Toast.LENGTH_SHORT);

//使用setGravity() 方法设置设置 Toast 在屏幕上的位置，第一个参数设置重力位置，有 TOP. BOTTOM. START 和 END 等值，第二.三个参数用于水平和垂直方向上的偏移量
sg.setGravity(Gravity.CENTER,0,0);
sg.show();
```

### 图文样例

getView 方法可以用来自定义带图片信息的提示：（进阶）

```java
//新建 Toast 控件 zj
Toast zj = Toast.makeText(MainActivity.this,"震惊 ！！",Toast.LENGTH_SHORT);
//设置控件位置（底部向上偏移160dp）
zj.setGravity(Gravity.BOTTOM,0,160);

//使用 getView() 方法得到 Toast 的 View
LinearLayout zjView = (LinearLayout)zj.getView();
                
//创建一个 ImageView
ImageView zjImg = new ImageView(getApplicationContext());
//设置图像
zjImg.setImageResource(R.drawable.zhenjing);
                
//使用 LinearLayout.LayoutParams 方法设置图片大小和图片在 LinerLayout 里的位置
LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(150,150);
params.setMargins(0,30,0,-20);
zjImg.setLayoutParams(params);

//调整 Toast 的 View 的 LinerLayout 的内部布局
zjView.setGravity(Gravity.CENTER);
zjView.setOrientation(LinearLayout.VERTICAL);
                
//图像添加到 zjView 里面，第二个参数决定了显示顺序（图片和文字的先后）
zjView.addView(zjImg,0);
                
//显示 Toast
zj.show();
```

上面的案例的最终效果是显示一个 Toast，其中第一行是一个震惊的可爱小图片，第二行是文字 “震惊 ！！”

我们把这段代码添加到我们在上一篇文章中的 BMI 计算器中，为大胖子加入震惊效果（dog

[![bmi-addzj.png](https://media.everdo.cn/tank/pic-bed/2020/04/05/bmi-addzj.png)](https://up.media.everdo.cn/image/JSQ9)

### 外挂布局文件（复杂 ！）

如果 Toast 的样式非常复杂，包含了一大堆奇形怪状的东西，可以为 Toast控件 单独建立一个 Layout.xml

1. 在 .res/layout 路径下，新建 toast_01.xml
2. 把视图和控件摆放完毕
3. 为控件设置独立 ID
4. 在函数中调用布局
   - 将 Toast 实例化 **```Toast zj = Toast.makeText(MainActivity.this,"震惊 ！！",Toast.LENGTH_SHORT);```**
   - 加载布局文件 **```View view = LayoutInflater.from(MainActivity.this).inflate(R.layout.toast_01, null);```**
   - 修改布局内显示的元素（查找ID）**```TextView 随便写 = (TextView)view.findViewById(R.id.布局内元素ID);```**
5. Toast 关联我们创建的 View **```toast.setView(view);```**
6. 设置显示在屏幕中的位置 **```zj.setGravity(Gravity.CENTER, 0,0);```**
7. 显示 **```toast.show();```**
