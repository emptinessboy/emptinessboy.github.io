---
title: 两个简单的JAVA GUI练习
date: 2020-05-19 22:58:59
category: JAVA学习
tags: java
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/21/intelij.png
---

最近在听 NEU 的 JAVA 慕课，然后有两个简单的 GUI 课后练习：

## 菜单栏相关练习

> 编写如图所示应用程序，单击选择菜单项退出后，显示下面的请选择对话框，选择是结束程序，选择否显示下面的消息对话框。

[![a.jpg](https://media.everdo.cn/tank/pic-bed/2020/05/19/a.jpg)](https://up.media.everdo.cn/image/Iufc)

题目要求使用菜单栏 JMenuBar 和 菜单项 JMenuItem， 很遗憾 IEDA 所提供的 SwingGUIdesigner 并没有默认提高 菜单栏 和 菜单项的选则。因此这里被迫使用了 JFormDesigner 来创建可视化界面：

[![jfd-homework1.png](https://media.everdo.cn/tank/pic-bed/2020/05/19/jfd-homework1.png)](https://up.media.everdo.cn/image/h4G2)

这里，题目要求的两个 optionPane 也是可以先在 jFromDesinger 中先画好的。这样就可以不用手动初始化了。

至此，系统自动生成的代码如下：

```java
private void initComponents() {
    // JFormDesigner - Component initialization - DO NOT MODIFY  //GEN-BEGIN:initComponents
    menuBar1 = new JMenuBar();
    menuFile = new JMenu();
    menuItemOpen = new JMenuItem();
    menuItemExit = new JMenuItem();
    menuEidt = new JMenu();
    menuForm = new JMenu();
    optionPaneChoose = new JOptionPane();
    optionPaneNo = new JOptionPane();

    //======== this ========
    setTitle("EmptinessBoy\u4f5c\u4e1a");
    Container contentPane = getContentPane();
    contentPane.setLayout(new GridLayout(3, 4));

    //======== menuBar1 ========
    {

        //======== menuFile ========
        {
            menuFile.setText("\u6587\u4ef6");

            //---- menuItemOpen ----
            menuItemOpen.setText("\u6253\u5f00");
            menuFile.add(menuItemOpen);

            //---- menuItemExit ----
            menuItemExit.setText("\u9000\u51fa");
            menuItemExit.addActionListener(e -> menuItemExitActionPerformed(e));
            menuFile.add(menuItemExit);
        }
        menuBar1.add(menuFile);

        //======== menuEidt ========
        {
            menuEidt.setText("\u7f16\u8f91");
        }
        menuBar1.add(menuEidt);

        //======== menuForm ========
        {
            menuForm.setText("\u7a97\u53e3");
        }
        menuBar1.add(menuForm);
    }
    setJMenuBar(menuBar1);
    setSize(445, 315);
    setLocationRelativeTo(getOwner());
    // JFormDesigner - End of component initialization  //GEN-END:initComponents
}

// JFormDesigner - Variables declaration - DO NOT MODIFY  //GEN-BEGIN:variables
private JMenuBar menuBar1;
private JMenu menuFile;
private JMenuItem menuItemOpen;
private JMenuItem menuItemExit;
private JMenu menuEidt;
private JMenu menuForm;
private JOptionPane optionPaneChoose;
private JOptionPane optionPaneNo;
// JFormDesigner - End of variables declaration  //GEN-END:variables
```

为了使程序完成题目要求的功能，我们需要给菜单项 JMenuItem【menuItemExit】设置监听器。

事件监听代码：

### optionPane 对话框写法

```java
private void menuItemExitActionPerformed(ActionEvent e) {
    // TODO add your code here
    int i = optionPaneChoose.showConfirmDialog(null,"是否退出系统？","请选择", JOptionPane.YES_NO_OPTION);
    if(i==0)
        System.exit(0);
    else{
        //ConfirmDialog(null,"您选择了否！","消息",JOptionPane.YES_OPTION);
        optionPaneNo.showMessageDialog(null,"您选择了否","消息", JOptionPane.YES_OPTION);
    }
}
```

对于多选对话框，int i 的返回值就是指代了用户选中的 “是” 或 “否” 的值。一般情况下，选中是为 0.

> optionPaneNo.showMessageDialog 显示一个消息提示
> optionPaneChoose.showConfirmDialog 显示可确认对话框

### 设置点击关闭窗体的默认事件

只要在实现 JFrame 类的构造函数中加入一条

```java
setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
```

即可轻松搞定。

最后，整体运行效果：

[![jfd-homework2.png](https://media.everdo.cn/tank/pic-bed/2020/05/19/jfd-homework2.png)](https://up.media.everdo.cn/image/hJjZ)


## 窗体相关练习

> 窗体中显示一个图片，用鼠标可以拖动图片到任意位置。

没错，作业只有这么简简单单一句话。然后我也天真的以为这是一道秒杀题。但是，往往是我太天真了（悲哀

头里的步骤并不难，这里使用 JFormDesigner 创建窗体。然后随便拖拽一个 JLable 用来存放图片。

[![jfd-homework3.png](https://media.everdo.cn/tank/pic-bed/2020/05/20/jfd-homework3.png)](https://up.media.everdo.cn/image/hPNk)

下面是系统自动生成的代码（含后面加的监听器）：

```java
……
    private void initComponents() {
        // JFormDesigner - Component initialization - DO NOT MODIFY  //GEN-BEGIN:initComponents
        label1 = new JLabel();
        textField1 = new JTextField();

        //======== this ========
        setMinimumSize(new Dimension(500, 500));
        setTitle("EmptinessBoyMooc\u4f5c\u4e1a");
        var contentPane = getContentPane();

        //---- label1 ----
        label1.setIcon(null);
        label1.addMouseMotionListener(new MouseMotionAdapter() {
            @Override
            public void mouseDragged(MouseEvent e) {
                label1MouseDragged(e);
            }
        });
        label1.addMouseListener(new MouseAdapter() {
            @Override
            public void mousePressed(MouseEvent e) {
                label1MousePressed(e);
            }
        });

        //---- textField1 ----
        textField1.setText("\u6b64\u5904\u663e\u793a\u5750\u6807");

        GroupLayout contentPaneLayout = new GroupLayout(contentPane);
        contentPane.setLayout(contentPaneLayout);
        contentPaneLayout.setHorizontalGroup(
            contentPaneLayout.createParallelGroup()
                .addGroup(contentPaneLayout.createSequentialGroup()
                    .addGroup(contentPaneLayout.createParallelGroup(GroupLayout.Alignment.LEADING, false)
                        .addComponent(label1, GroupLayout.PREFERRED_SIZE, 100, GroupLayout.PREFERRED_SIZE)
                        .addGroup(contentPaneLayout.createSequentialGroup()
                            .addContainerGap()
                            .addComponent(textField1)))
                    .addContainerGap())
        );
        contentPaneLayout.setVerticalGroup(
            contentPaneLayout.createParallelGroup()
                .addGroup(contentPaneLayout.createSequentialGroup()
                    .addComponent(label1, GroupLayout.PREFERRED_SIZE, 100, GroupLayout.PREFERRED_SIZE)
                    .addPreferredGap(LayoutStyle.ComponentPlacement.RELATED, 302, Short.MAX_VALUE)
                    .addComponent(textField1, GroupLayout.PREFERRED_SIZE, GroupLayout.DEFAULT_SIZE, GroupLayout.PREFERRED_SIZE)
                    .addContainerGap())
        );
        pack();
        setLocationRelativeTo(getOwner());
        // JFormDesigner - End of component initialization  //GEN-END:initComponents
    }

    // JFormDesigner - Variables declaration - DO NOT MODIFY  //GEN-BEGIN:variables
    private JLabel label1;
    private JTextField textField1;
    // JFormDesigner - End of variables declaration  //GEN-END:variables
}
```

到这里，我们需要给 jlable 设置 icon，这里将设置 icon 的代码放到构造函数中：

### Jlabel 设置 icon 方法

```java
public MovePic() {
    initComponents();
    setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    ImageIcon i = new ImageIcon("src/logo.png");
    Image pic = i.getImage().getScaledInstance(100,100,Image.SCALE_DEFAULT);
    ImageIcon ico = new ImageIcon(pic);
    label1.setIcon(ico);
}
```

现在是不是只要给 存放了图片的 jlable 设置 MouseDragged 鼠标拖拽监听函数呢？

最开始一脸小白的我确实是这么想的，然后写下了简单的

```java
错误代码：
x = e.getX();
y = e.getY();
textField1.setText(x+","+y);
label1.setLocation(x,y);
```

网上都说了 e.getX(); e.getY(); 不就是获取当前是鼠标位置嘛。（呵呵

然而在实际测试中发现，实际上，这两个获取到的都是以 jlable 为容器，鼠标在 jlable 中的相对位置。因此单纯这样的代码无法实现所需要的功能。

那么，一心想偷懒的我想，那么只要针对 Jlable 的父容器设置鼠标监听器来改变坐标不就完了？（理想很美好，现实确是：

因为子容器遮挡了父容器，当鼠标移动到 Jlable 上时，设置在父容器 JFrame 的监听器就失效了！！

只有鼠标移出图片的时候，才能正确获取针对窗体的坐标。

### 终极坐标解决方案

那么只能使出大杀器了，（用我小学的算数水平，通过绝对坐标加减来获取位置了

经过查找文档，可知：

> e.getXOnScreen() e.getYOnScreen() 可以用来获取鼠标在整个屏幕的绝对位置，而 this.getX() this.getY()可以获得当前窗体在屏幕中的左上角位置。

那么？！

只要使用 ```x = e.getXOnScreen()-this.getX()``` 就可以通过计算获得鼠标在窗体内部的相对位置啦！！！

但是这时候还是有些小小的瑕疵 ——鼠标拖拽后，显示的位置是以鼠标结束位置作为左上角定点的，拖拽感觉不够自然。

修复的方法很简单。既然  e.getX() 可以获取当前鼠标相对于图片（jlable）的相对位置，那么只要在我们刚才获取的 x 减去 这个内部的相对位置就完美啦！！注意这个坐标需要在刚开始按下鼠标时获取才有用，因此需要放在 MousePressed 监听器中。

最后附上代码：

```java
public class MovePic extends JFrame {
    int x,y,a,b;
    public static void main(String[] args) {
        new MovePic().setVisible(true);
    }
    public MovePic() {
        initComponents();
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        ImageIcon i = new ImageIcon("src/logo.png");
        Image pic = i.getImage().getScaledInstance(100,100,Image.SCALE_DEFAULT);
        ImageIcon ico = new ImageIcon(pic);
        label1.setIcon(ico);
    }

    private void label1MouseDragged(MouseEvent e) {
        // TODO add your code here
        x = e.getXOnScreen()-this.getX()-a;
        y = e.getYOnScreen()-this.getY()-b-20;
        textField1.setText(x+","+y);
        label1.setLocation(x,y);
    }


    private void label1MousePressed(MouseEvent e) {
        // TODO add your code here
        a = e.getX();
        b = e.getY();
    }
……
```

运行效果：

[![e18f47190defc5112b413d963c2e3a72.gif](https://media.everdo.cn/tank/pic-bed/2020/05/20/e18f47190defc5112b413d963c2e3a72.gif)](https://up.media.everdo.cn/image/hItB)

nice！又是洗洗睡的一天（PS，最近腰疼犯了，睡觉保命要紧【滑稽】
