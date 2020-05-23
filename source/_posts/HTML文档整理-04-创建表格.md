---
title: HTML文档整理 04-创建表格
date: 2020-03-14 00:49:03
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

## 表格基本结构

使用表格显示数据，可以更直观和清晰。在HTML文档中表格主要用于显示数据，虽然可以使用表格布局，但是不建议使用，它有很多弊端。

```<table>``` 标记用于标识一个表格对象的开始，```</table>``` 标记用于标识一个表格对象的结束。<!--more-->**一个表格中，只允许出现一对 ```<table>``` 标记**。


```<tr>``` 标记用于标识表格一行的开始，```</tr>``` 标记用于标识表格一行的结束。表格内有多少对 ```<tr></tr>``` 标记，就表示表格中有多少行。```<td>``` 标记用于标识表格某行中的一个单元格开始，```</td>``` 标记用于标识表格某行中的一个单元格结束。

```<td></td>``` 标记书写在 ```<tr></tr>``` 标记内，一对 ```<tr></tr>``` 标记内有多少对 ```<td></td>``` 标记，就表示该行有多少个单元格。在HTML5中仅有 colspan 和 rowspan 两个属性。

最基本的表格必须包含一对 ```<table></table>``` 标记、一对或几对 ```<tr></tr>``` 标记及一对或几对 ```<td></td>``` 标记。一对 ```<table></table>``` 标记定义一个表格，一对 ```<tr></tr>``` 标记定义一行，一对 ```<td></td>``` 标记定义一个单元格。

> 简而言之，```<tr>``` 表示有多少行，```<td>``` 表示有多少列

```html
这是一个三行四列的表格：
<table >
   <tr>
       <td>A1</td>
       <td>B1</td>
       <td>C1</td>
       <td>D1</td>
   </tr>
   <tr>
       <td>A2</td>
       <td>B2</td>
       <td>C2</td>
       <td>D2</td>
   </tr>
   <tr>
       <td>A3</td>
       <td>B3</td>
       <td>C3</td>
       <td>D3</td>
   </tr><!--表格基本结构-->
</table>
```

<table >
   <tr>
       <td>A1</td>
       <td>B1</td>
       <td>C1</td>
       <td>D1</td>
   </tr>
   <tr>
       <td>A2</td>
       <td>B2</td>
       <td>C2</td>
       <td>D2</td>
   </tr>
   <tr>
       <td>A3</td>
       <td>B3</td>
       <td>C3</td>
       <td>D3</td>
   </tr><!--表格基本结构-->
</table>

## 合并单元格

### 合并两个单元格

在 HTML 中合并的方向有两种：一种是上下合并；另一种是左右合并，这两种合并方式只需要使用 colspan 和 rowspan 属性即可。

单元格的合并格式如下：

```html
左右单元格
<td colspan="数值"> 单元格内容 </td>
上下单元格
<td rowspan="数值"> 单元格内容 </td>
```

```html
这是一个三行四列的表格（合并单元格）：
<table >
   <tr>
    <!--A1,B1上下合并-->
       <td colspan="2">A1 B1</td>
       <td>C1</td>
       <td>D1</td>
   </tr>
   <tr>
       <td>A2</td>
       <td>B2</td>
       <td rowspan="2">C2 C3</td><!--C1,C2上下合并-->
       <td>D2</td>
   </tr>
   <tr>
       <td>A3</td>
       <td>B3</td>
       <td>D3</td>
   </tr>
</table>
```

<table >
   <tr>
   <!--A1,B1上下合并-->
       <td colspan="2">A1 B1</td>
       <td>C1</td>
       <td>D1</td>
   </tr>
   <tr>
       <td>A2</td>
       <td>B2</td>
       <td rowspan="2">C2 C3</td><!--C1,C2上下合并-->
       <td>D2</td>
   </tr>
   <tr>
       <td>A3</td>
       <td>B3</td>
       <td>D3</td>
   </tr>
</table>

需要注意的是在合并单元格后，相应的单元格标记就应该删除，否则就会多出来一个，以及后面的单元格依次向右移动的错乱现象。

### 合并多个单元格

```html
这是一个三行四列的表格：
<table >
   <tr>
       <td>A1</td>
       <td>B1</td>
       <td>C1</td>
       <td>D1</td>
   </tr>
   <tr>
       <td>A2</td>
       <td>B2</td>
       <td>C2</td>
       <td>D2</td>
   </tr>
   <tr>
       <td>A3</td>
       <td>B3</td>
       <td>C3</td>
       <td>D3</td>
   </tr><!--表格基本结构-->
</table>
```

<table >
   <tr>
       <td colspan="2" rowspan="2">A1 B1 <br>A2 B2</td>
       <td>C1</td>
       <td>D1</td>
   </tr>
   <tr>
       <td>C2</td>
       <td>D2</td>
   </tr>
   <tr>
       <td>A3</td>
       <td>B3</td>
       <td>C3</td>
       <td>D3</td>
   </tr><!--表格基本结构-->
</table>

## DreamWeaver操作表格

### 创建表格

在 Dreamweaver CC 2020 中创建表格，只需要执行【插入】菜单中的【Table】命令，在弹出的对话框中指定表格的行数、列数、宽度和边框，即可在光标处创建一个空白表格。

[![html_dw_table.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_dw_table.jpg)](https://up.media.everdo.cn/image/Hna2)

在弹出的对话框中指定表格的行数、列数、宽度和边框，即可在光标处创建一个空白表格

[![html_dw_table1.md.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_dw_table1.md.jpg)](https://up.media.everdo.cn/image/HB3Z)

选择表格之后，【属性】面板提供了表格的常用操作

[![html_dw_table2.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_dw_table2.jpg)](https://up.media.everdo.cn/image/HREk)

### 拆分合并表格

在Dreamweaver CC可视化操作中，提供了合并与拆分单元格两种操作。

进行单元格合并和拆分时，请将光标置于单元格内，如果选择了一个单元格，则拆分命令有效；如果选择了两个或两个以上单元格，则合并命令有效。

以合并命令为例，在设计视图选中两个单元格：

[![html_dw_table3.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_dw_table3.jpg)](https://up.media.everdo.cn/image/H2Bt)

进入属性面板，点击合并按钮

[![html_dw_table6.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_dw_table6.jpg)](https://up.media.everdo.cn/image/H3SI)

看到合并效果如下

[![html_dw_table5.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_dw_table5.jpg)](https://up.media.everdo.cn/image/HjZB)

## 完整表格标记

为了让表格结构更清楚，以及配合后面的CSS样式，更方便地制造出各种各样的表格，表格中还会出现表头、主体、脚注等。三者对应的 HTML 标记为 ```<thead>```、```<tbody>```、```<tfoot>```。
另外表格还有两个标记。标记 ```<caption>``` 表示表格的标题，在一行中除了 ```<td>``` 标记表示一个单元格以外，还可以使用 ```<th>``` 定义表格内的表头单元格。

使用 ```<caption>``` 标记定义了表格标题，```<thead>```、```<tbody>``` 和 ```<tfoot>``` 标记对表格进行了分组。在 ```<thead>``` 部分使用 ```<th>``` 标记代替 ```<td>``` 标记定义单元格，```<th>``` 标记定义的单元格默认加粗。```<caption>``` 标记必须紧随 ```<table>``` 标记之后。

```html
<style>
    tfoot{background-color: #FF3;}  /*脚注颜色*/
</style>

<table width="200" border="1"> <!--边框粗细-->
    <tr>
      <td colspan="2">&nbsp;</td>
      <td>&nbsp;</td>
      <td>&nbsp;</td>
    </tr>
    <tr>
      <td>&nbsp;</td>
      <td>&nbsp;</td>
      <td rowspan="2">&nbsp;</td>
      <td>&nbsp;</td>
    </tr>
    <tr>
      <td>&nbsp;</td>
      <td>&nbsp;</td>
      <td>&nbsp;</td>
    </tr>
</table>

<table >
   <caption>学生成绩单</caption> <!--表格标题-->
    <thead> <!--表头-->
     <tr>
         <th>姓名</th><th>性别</th><th>成绩</th>
     </tr>
    </thead>
    <tfoot> <!--脚注-->
        <tr>
            <td>平均分</td><td colspan="2">540</td>
        </tr>
    </tfoot>
    <tbody> <!--主体-->
     <tr>
      <td>张三</td>
      <td>男</td>
      <td>560</td>
      </tr>
    </tbody>
    <tr>
      <td>李四</td>
      <td>男</td>
      <td>520</td>
    </tr>
</table>
```
运行结果如下：

[![html_table.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html_table.jpg)](https://up.media.everdo.cn/image/HDJX)

## 一些简单 CSS

```html
<style>
table{
    /*表格添加宽度为3的#505050色边框*/
    border:3px solid #505050;
}
caption{
    /*表格标题字号36号*/
    font-size:36px;
}
th,td{
    /*表格单元格增加描边*/
    border:1px solid #505050;
}
</style>
```

> 使用 ```<thead>、<tbody>和<tfoot>``` 标记对行进行分组的意义何在？
> 
> 在HTML文档中增加 ```<thead>、<tbody> 和 <tfoot>``` 标记虽然从外观上不能看出任何变化，但是它们却使文档的结构更加清晰。使用 ```<thead>、<tbody> 和 <tfoot>``` 标记除了使文档更加清晰之外，还有一个更重要的意义，那就是方便使用CSS样式对表格的各个部分进行修饰，从而制作出更炫的表格