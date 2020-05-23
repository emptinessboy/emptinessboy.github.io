---
title: inteliJ 学习 SwingGui 记录
date: 2020-04-21 14:57:49
category: JAVA学习
tags: java
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/21/intelij.png
---

## GUI 相关工具组件

### AWT

abstract window toolkit 抽象窗口工具包，提供了图形用户界面和图形，直接调用本地系统接口完成。

### Swing

Swing 是建立在 AWT 基础之上的，它利用了 AWT 的底层组件，包括图形、颜色、字体等。增加了界面修饰，使界面更美观，在丌同的操作系统中的显示更为相似。
<!-- more -->

### 基本组件

> 组件是一个可以以图形化的方式显示在屏幕上并能与用户进行交互的对象，例如一个按钮，一个标签等。容器本身也是一个组件，具有组件的所有性质，但是它的主要功能是容纳其它组件和容器。

基本组件|名称|功能
---|---|---
Window类|窗口类|Window 类的实例没有边框和标题,并且不能附加或嵌入到另一个容器中
Frame类|框架类|Frame 类的实例可以有一个菜单条，否则它与 Window 类的对象非常相似
Dialog类|对话框类|Dialog 类的对象只有在一个相关的 Frame 类对象存在时才存在
Panel类|面板类|Panel 类的是实例提供一个可以加入组件的容器，是容器组件的通用容器

AWT 中的基本控件：

Button按钮，Label标签，TextField文本框，TextArea多行文本框，Checkbox复选框，CheckboxGroup单选框，Choice下拉式列表，List列表，Menu菜单
，Scrollbar滚动条

> .pack() 方法可以使组件适应大小调整
> setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 设置默认窗体关闭按钮动作

添加组件非常简单，只需要使用容器的 add 方法，例如 awt 下：

```java
Frame f = new Frame();
f.setLayout(new FlowLayout);
Button b = new Button("ok")
f.add(b)
```

容器 Container 是一个类，实际上是 Component 的子类。容器的各种的组件的大小和位置是由容器的布局管理器进行控制。

> getContentPane() 返回此窗体的 contentPane 对象

Swing 下：

```java
JFrame jf = new JFrame();
Container jframe_content = jf.getContentPane();
jframe_content.setLayout(new FlowLayout);
Button b = new Button("ok");
jframe_content.add(b);
jframe_content.add(new Button("Cancel"))
```

#### 公共属性

```java
public int getWidth() //宽度
public int getHeight() //高度
public void setSize(int width, int height) //宽度和高度
public int getX() //位置的X坐标值
public int getY() //位置的Y坐标值
public void setLocation(int x, int y) //坐标位置，x、y指定组件左上角相对于容器的坐标位置
```

```java
public void setBounds(int x, int y, int width, int height) //坐标位置和宽度、高度
public Color getBackground() //获得组件的背景颜色
public void setBackground(Color c) //设置组件的背景颜色
public Font getFont() //获得组件字体
public void setFont(Font f) //设置组件字体
public void setVisible(boolean b) //设置组件是否显示
```

### 布局管理器

> JFrame 和 JWindow 默认布局管理器为 BorderLayout，而 JPanel 默认的布局管理器为 FlowLayout。

- BorderLayout（边框布局管理器）是 Window、JFrame 和 JDialog 的默认布局管理器。边框布局管理器将窗口分为 5 个区域：North、South、East、West 和 Center。
  
- FlowLayout（流式布局管理器）是 JPanel 和 JApplet 的默认布局管理器。FlowLayout 会将组件按照从从左到右、上到下的放置规律逐行进行定位。（与其他布局管理器不同的是，FlowLayout 布局管理器不限制它所管理组件的大小，而是允许它们有自己的最佳大小。）
  
- CardLayout（卡片布局管理器）能够帮助用户实现多个成员共享同一个显示空间，并且一次只显示一个容器组件的内容。（CardLayout 布局管理器将容器分成许多层，每层的显示空间占据整个容器的大小，但是每层只允许放置一个组件。）
  
- GridLayout（网格布局管理器）为组件的放置位置提供了更大的灵活性。它将区域分割成行数（rows）和列数（columns）的网格状布局，组件按照由左至右、由上而下的次序排列填充到各个单元格中。（提示：GridLayout 布局管理器总是忽略组件的最佳大小，而是根据提供的行和列进行平分。该布局管理的所有单元格的宽度和高度都是一样的。）

- GridBagLayout（网格包布局管理器）是在网格基础上提供复杂的布局，是最灵活、 最复杂的布局管理器。GridBagLayout 不需要组件的尺寸一致，允许组件扩展到多行多列。每个 GridBagLayout 对象都维护了一组动态的矩形网格单元，每个组件占一个或多个单元，所占有的网格单元称为组件的显示区域。（GridBagLayout 所管理的每个组件都与一个 GridBagConstraints 约束类的对象相关。这个约束类对象指定了组件的显示区域在网格中的位置，以及在其显示区域中应该如何摆放组件。除了组件的约束对象，GridBagLayout 还要考虑每个组件的最小和首选尺寸，以确定组件的大小。）

- BoxLayout（盒布局管理器）通常和 Box 容器联合使用。

- SpringLayout 类实现的布局管理器称为弹簧布局管理器。利用该布局管理器管理组件，当改变窗体的大小时，能够在不改变组件间相对位置的前提下自动调整组件大小，使组件依旧布满整个窗体，从而保证了窗体的整体效果。

- 绝对布局，就是硬性指定组件在容 器中的位置和大小，可以使用绝对坐标的方式来指定组件的位置。（用户必须使用Java语言提供的setLocation(),setSize(),setBounds()等方法，为容器中的每个组件设置大小和显示位置，否则将无法看到这些组件。）

## JAVA 事件

### 事件类型

事件类型|事件内容
---|---
ComponentEvent（组件事件）|组件尺寸的变化、移动
ContainerEvent（容器事件）|容器内组件的增加、删除
WindowEvent（窗口事件）|关闭和打开窗口
FocusEvent（焦点事件）|焦点的获得和释放
KeyEvent（键盘事件）|按键的按下，松开
MouseEvent（鼠标事件）|单击鼠标，拖动鼠标
ActionEvent（动作事件）|按钮按下，TextField中按Enter键
ItemEvent（项目事件）|选中项目或放弃选中项目
TextEvent（文本事件）|文本内容改变。

### JAVA 事件监听器（难点）

**1.事件对象：** 一般继承自java.util.EventObject对象,由开发者自行定义.

**2.事件源：** 就是触发事件的源头,不同的事件源会触发不同的事件类型.

**3.事件监听器：** 事件监听器负责监听事件源发出的事件.一个事件监听器通常实现 java.util.EventListener 这个标识接口. 

其整个处理过程是这样的,事件源可以注册事件监听器对象,并可以向事件监听器对象发送事件对象.事件发生后,事件源将事件对象发给已经注册的所有事件监听器. 监听器对象随后会根据事件对象内的相应方法响应这个事件.

**上面的正式说明我看糊涂了，以下为个人粗浅的理解：**

先看一段一段简单的实现按钮点击执行事件的实例代码：

```java
Button b = new Button("button"); //创建按钮
b.addActionListener(new ActionListener() {
    //使用内部匿名事件处理
    @Override
    public void actionPerformed(ActionEvent e) {
        //点击后执行的代码
    }
});
```

首先按钮等组件都会自带一个 addActionListener() 方法，这个方法需要传入一个参数（接口类ActionListener），并且这个类需要实现接口，其中必须写完整方法 actionPerformed(ActionEvent e)。

当 addActionListener() 方法被添加到按钮对象后，系统就会在后台监听事件发生，一旦触发事件（如按钮被点击），就会回调 ActionListener 接口中 actionPerformed() 这个方法，并传入参数 ActionEvent e。ActionEvent e 会包括发生事件的对象以及一些别的信息。

### JDK 源码

官方源代码 JDK1.8：

***java\awt\event\ActionListener.java***

```java
public interface ActionListener extends EventListener {
    /**
     * Invoked when an action occurs.
     */
    public void actionPerformed(ActionEvent e);
}
```

***java\awt\Button.java***

```java
addActionListener(ActionListener l) {
    if (l == null) {
        return;
    }
    actionListener = AWTEventMulticaster.add(actionListener, l);
    newEventsOnly = true;
}
```

***java\awt\AWTEventMulticaster.java***

```java
public void processEvent(AWTEvent e) {
    // when event occurs which causes "action" semantic
    ActionListener listener = actionListener;
    if (listener != null) {
        listener.actionPerformed(new ActionEvent()); //这一步回调了！！！！
    }
}
```

### 实现监听的四种方法

#### 自身类作为事件监听器

适合多个事件执行同一个方法，可以大大减少代码量，但东西多了就会很复杂

```java
class EventListener extends JFrame implements ActionListener {
    //继承JFrame，并继承接口
    private JButton b1, b2;

    public EventListener() {
        //默认构造函数
        ……定义窗体

        b1 = new JButton("button");
        b2 = new JButton("button");

        // 将按钮添加事件监听器
        //这一步就将自己所在的类传入
        b1.addActionListener(this);
        b2.addActionListener(this);

        add(b1);add(b2);setVisible(true);
    }

    // ***********事件处理***********
    @Override
    public void actionPerformed(ActionEvent e) {
        //多个按钮时需要通过传入的参数区分
        if (e.getSource() == b1) {
            //点击b1后执行的代码
        } else if (e.getSource() == b2) {
            //点击b2后执行的代码
        }
    }
}
```

#### 内部类处理

```java
class EventListener extends JFrame {
    private JButton b1, b2;

    // 构造方法
    public EventListener() {
        ……定义窗体

        b1 = new JButton("button");
        b2 = new JButton("button");
        
        // 添加事件监听器对象(面向对象思想)
        b1.addActionListener(new b1Listener());
        b2.addActionListener(new b2Listener());

        add(b1);add(b2);setVisible(true);
    }

    // 内部类b1Listener，实现ActionListener接口
    class b1Listener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            //点击b1后执行的代码
        }
    }

    // 内部类b2Listener，实现ActionListener接口
    class b2Listener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            //点击b2后执行的代码
        }
    }

}
```

#### 匿名内部类处理（inteliJ 默认）

```java
Button b1 = new Button("button");
Button b2 = new Button("button"); 
//创建按钮
b1.addActionListener(new ActionListener() {
    //使用内部匿名事件处理
    @Override
    public void actionPerformed(ActionEvent e) {
        //点击b1后执行的代码
    }
});
b2.addActionListener(new ActionListener() {
    //使用内部匿名事件处理
    @Override
    public void actionPerformed(ActionEvent e) {
        //点击b2后执行的代码
    }
});
```

#### 外部类处理

```java
class EventListener extends JFrame {
    private JButton b1, b2;

    public EventListener() {
        ……定义窗体

        b1 = new JButton("button");
        b2 = new JButton("button");
        // 将按钮添加事件监听器
        b1.addActionListener(new b1Listener(this));
        b2.addActionListener(new b2Listener());

        add(b1);add(b2);setVisible(true);
    }

}

// 外部类b1EventListener，实现ActionListener接口
class b1Listener implements ActionListener {
    private EventListener el;

    @Override
    public void actionPerformed(ActionEvent e) {
        //点击b1后执行的代码
    }
}


// 外部类DialogEventListener，实现ActionListener接口
class b2Listener implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {
        //点击b1后执行的代码
    }
}

public class ActionListenerTest {
    public static void main(String args[]) {
        new EventListener();
    }
}
```

### 安卓中实现

```java
Button Cal = findViewById(R.id.buttonCal);
Cal.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
    //点击后执行的代码
    }
});
```

## 常用属性之类

此处先随便整理些课上讲的：

### 简单控件

text 属性：控件显示的文本

Columns 属性：控件列宽

变量名称 fieldname 属性：设置组件ID

按钮的 action 事件：点击执行的函数

控件的 getText 和 setText 方法：显示和修改文字

```java
jTextField.getText()    //返回 String
```

System.exit方法：结束程序（窗体的三种关闭方式：Exit、Dispose、Hide）

```java
//Exit
System.exit(0);
//Dispose & hide
this.dispose();
this.hide();
```

Lable 的 icon 属性：更改/显示标签的图片

```java
//动态显示图片
String s = System.getProperty("user.dir"); //获取程序所在路径
ImageIcon i = new ImageIcon(s+"/hhh.jpg"); //先设置ImageIcon
jLable.setIcon(i);
```

icon 按比例缩放（用于不确定大小的图片不溢出）

```java
ImageIcon i = new ImageIcon(s);
Image pic = i.getImage().getScaledInstance(200,200,Image.SCALE_DEFAULT);
ImageIcon ico = new ImageIcon(pic);
PicLable.setIcon(ico);
```

### 单选按钮和复选框：

```
JTextArea：文本区域
JRadioButton：单选按钮
ButtonGroup：按钮组
JCheckBox：复选框
```

单选按钮具有 text、selected 属性；ButtonGroup是按钮组，不显示

#### DEMO1

编写如图所示应用程序，选择字体字号后按设置按钮，上面文字按选择的字体和字号进行设置显示，按关闭按钮结束程序。

[![gui1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/gui1.jpg)](https://up.media.everdo.cn/image/ImMX)

在 InteliJ 中，新建 Swing UI Designer，GUI Form

[![hxfgui1.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui1.jpg)](https://up.media.everdo.cn/image/I9gi)

输入类名后系统会自动创建两个文件，一个 form 文件和一个 java 文件。

[![hxfgui2.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui2.jpg)](https://up.media.everdo.cn/image/IcD4)

打开 form 文件，选定布局后即可在上面自由拖拽控件，此时应该将用到的控件添加 fieldname 也就是 ID 属性

[![hxfgui3.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui3.jpg)](https://up.media.everdo.cn/image/IfcM)

在可视化界面，右键控件可以自动生成监听器或快速跳转到监听器，这一步很方便

[![hxfgui4.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui4.jpg)](https://up.media.everdo.cn/image/Is5Y)

创建完布局后，不同于 NetBeans，Idea 不会生成任何关于布局的 java 代码，所有的布局是在编译中直接打包进 class 的，并不是先为我们添加到 java 类文件。（这个很坑，没法偷懒直接拷贝他的代码了

系统就生成了这些：

```java
package com.emptinessboy.learngui1;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class MainForm {
    private JPanel panel;
    private JButton ButtonSetting;
    private JButton ButtonClose;
    private JTextField TextField;
    private JRadioButton SongTiRadioButton;
    private JRadioButton HeiTiRadioButton;
    private JRadioButton a12RadioButton;
    private JRadioButton a18RadioButton;
}
```

在我们添加监听器，并编写完整代码后：

```java
public MainForm() {
    HeiTiRadioButton.setSelected(true);
    a12RadioButton.setSelected(true);
    ButtonSetting.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            System.out.println("设置按钮被点击");
            if (HeiTiRadioButton.isSelected()){
                if (a12RadioButton.isSelected()){
                    TextField.setFont(new Font("黑体",0,12));
                    System.out.println("设置为黑体12号");
                }
                else{
                    TextField.setFont(new Font("黑体",0,18));
                    System.out.println("设置为黑体18号");
                }
            }
            if (SongTiRadioButton.isSelected()){
                if (a12RadioButton.isSelected()){
                    TextField.setFont(new Font("宋体",0,12));
                    System.out.println("设置为宋体12号");
                }
                else{
                    TextField.setFont(new Font("宋体",0,18));
                    System.out.println("设置为宋体18号");
                }
            }
        }
    });
    ButtonClose.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            System.exit(0);
        }
    });
    SongTiRadioButton.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            if (SongTiRadioButton.isSelected()){
                HeiTiRadioButton.setSelected(false);//单选框互斥
                System.out.println("选中宋体");
            }
        }
    });
    HeiTiRadioButton.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            if (HeiTiRadioButton.isSelected()){
                SongTiRadioButton.setSelected(false);//单选框互斥
                System.out.println("选中黑体");
            }
        }
    });
    a12RadioButton.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            if (a12RadioButton.isSelected()){
                a18RadioButton.setSelected(false);//单选框互斥
                System.out.println("选中12号");
            }
        }
    });
    a18RadioButton.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            if (a18RadioButton.isSelected()){
                a12RadioButton.setSelected(false);//单选框互斥
                System.out.println("选中18号");
            }
        }
    });
}
```

这里补充一波，**设置字体和字号：**

```java
TextField.setFont(new Font("宋体",0,18));
```

最后到这里，程序没法运行。因为系统不会为我们生成 main 方法，手动生成很简单，直接右键即可：

[![hxfgui5.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui5.jpg)](https://up.media.everdo.cn/image/I0Ra)

最后，运行效果：

[![guidemo01.gif](https://media.everdo.cn/tank/pic-bed/2020/04/22/guidemo01.gif)](https://up.media.everdo.cn/image/I16s)

查看编译生成的文件和打包成的 jar 后都可以看到，除了我们些的类，还要自动打包进去的 intelij/uiDesigner/core 的代码。推测，系统很可能把我们定义的布局文件生成到这些 class 里。

[![hxfgui6.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui6.jpg)](https://up.media.everdo.cn/image/IMp3)

**补充二**

这个案例，我是写程序判断 RadioButton 选中情况来实现两个按钮互斥功能，其实 intelij 也有 RadioButtonGroup，只不过没有像 NetBeans 那样显示到右侧组件栏

> （PS，intelij自带的组件真的少的可怜

[![hxfgui7.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui7.jpg)](https://up.media.everdo.cn/image/IyPG)

ButtonGroup 的开启方式被隐藏到了属性栏

### 组合框和列表

```
JTextField：文本字段
JComboBox：组合框
JList：列表
```

JComboBox组合框，设置静态选项的方法是设置 model 属性，一行一个：

[![hxfgui8.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui8.jpg)](https://up.media.everdo.cn/image/ITi9)

动态修改则使用 addIthem 方法

```java
comboBox.addItem("字符串");
```

设置默认选中项，同理可以 get

```java
comboBox.setSelectedIndex(0);
```

JList列表要增加内容比较复杂，需要使用 setModel 方法，传入一个类，父类是抽象类，需要完成 getSize 和 getElementAt 方法

```java
list.setModel(new AbstractListModel() {
    String[] strings = {"aaa","bbb","ccc"};
    @Override
    public int getSize() {
        return strings.length;
    }

    @Override
    public Object getElementAt(int index) {
        return strings[index];
    }
});
```

### 对话框和菜单

新建方式和新建窗体类似

[![hxf-gui9.png](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxf-gui9.png)](https://up.media.everdo.cn/image/IXvj)

打开对话框方式

```java
new testDialog().setVisible(true);
```

菜单：

```java
JMenuBar：菜单条
JMenu：菜单
JMenuItem：菜单项
```

通用对话框:

```java
JFileChooser：文件选择对话框
JOptionPane：消息对话框
JColorChooser：颜色选择对话框
```

文件选则的详细调用方法：

```java
JFileChooser fc = new JFileChooser();
int i = fc.showOpenDialog(ButtonChose);
if(i==0){
    s = fc.getSelectedFile().toString();
    System.out.println(s);
}
else
    System.out.println("被取消");
```

JOptionPane：

```java
JOptionPane.showConfirmDialog(null,"yes or no","标题",JOptionPane.YES_NO_OPTION);
```

#### DEMO2

编写如图所示应用程序，单击选择图片文件按钮后，显示下面的打开文件对话框，选择要显示的图片，点击显示图片，显示刚刚选中的图片，按关闭按钮结束程序。

[![tp2.th.png](https://media.everdo.cn/tank/pic-bed/2020/04/22/tp2.th.png)](https://up.media.everdo.cn/image/ICgO)

先设计窗体：

[![hxfgui10.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui10.jpg)](https://up.media.everdo.cn/image/IpD6)

接下来添加按钮点击事件,

文件选则按钮代码:

```java
ButtonChose.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        JFileChooser fc = new JFileChooser();
        int i = fc.showOpenDialog(ButtonChose);
        if(i==0){
            s = fc.getSelectedFile().toString();
            System.out.println(s);
        }
        else
            System.out.println("被取消");
    }
});
```

显示图片按钮代码：

```java
ButtonShow.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        ImageIcon i = new ImageIcon(s);
        Image pic = i.getImage().getScaledInstance(200,200,Image.SCALE_DEFAULT);
        ImageIcon ico = new ImageIcon(pic);
        PicLable.setIcon(ico);
    }
});
```

退出程序按钮代码：

```java
ButtonClose.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.exit(0);
    }
});
```

运行效果：

[![hxfgui12.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui12.jpg)](https://up.media.everdo.cn/image/Iw5S)

[![hxfgui13.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui13.jpg)](https://up.media.everdo.cn/image/Itfn)

## JFormDesigner

这是一款 idea 的增强 GUI 设计插件，设计的界面可以生成标准的 java 代码，而不是像 idea 自带的 Swing GUI Designer 一样没有代码生成。

同时这个插件还有更多的组件可以供选择！！！

[![hxfgui14.jpg](https://media.everdo.cn/tank/pic-bed/2020/04/22/hxfgui14.jpg)](https://up.media.everdo.cn/image/IZNJ)

### 踩坑

使用这个插件一定要手动编写 main 方法，系统生成的不管用。手动编写其实只要一句话：(新建时继承选择Jframe)

```java
public static void main(String[] args) {
    new form1().setVisible(true);
}
```

~~~时间关系，JFormDesigner 我还没有深入使用，下次折腾了再补充！~~~

---

后来做了两个MOOC的练习，因为有些控件 IEDA 自带的设计器找不到，故使用了 JFD。

见链接： [JFD使用的两个案例](https://coding.emptinessboy.com/2020/05/%E4%B8%A4%E4%B8%AA%E7%AE%80%E5%8D%95%E7%9A%84JAVA-GUI%E7%BB%83%E4%B9%A0/)
