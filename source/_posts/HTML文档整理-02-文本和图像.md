---
title: HTML文档整理 02-文本和图像
date: 2020-03-13 15:25:28
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

## 添加文本

### 直接在DreamWeaver粘贴

略

### 特殊文字符号

如何在网页上显示这些特殊字符(字符转义)  每个行业都有自己的行业特性，如数学、物理和化学都有特殊的符号

在HTML中，特殊字符以“&”开头，以“；”结尾，中间为相关字符编码

<!--more-->

[![specialword-html5.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/specialword-html5.jpg)](https://up.media.everdo.cn/image/OCj)
	
> 技巧提示：尽量不要使用多个 ```“&nbsp”``` 来表示多个空格，因为多数浏览器对空格的距离实现是不一样的。

### 文本特殊样式

文本特殊样式在文档中经常会出现重要文本（加粗显示）、倾斜文本、上标和下标文本等。

#### 重要文本

```html
<p><b>我是粗体文字</b> </p>
```
<p><b>我是粗体文字</b> </p>

```html
<p><strong>我是加强调文字</strong></p>
```
<p><strong>我是加强调文字</strong></p>

#### 倾斜文本

```html
<p><i>我是倾斜文字</i></p>
```
<p><i>我是倾斜文字</i></p>

```html
<p><em>我是强调文字</em></p>
```
<p><em>我是强调文字</em></p>

> 就表现而言 ```<em></em>,<i></i>``` 表现都一样，都是表示斜体。但是 ```<em>``` 标签是“含有语义”的标签，搜索引擎会了解这些语义。其在HTML中是特意被设定为表示“强调”的意思。当发现这些表示“强调”的标签时，一些屏幕阅读器可能使用不同的inflection，更利于SEO。
	
#### 上标下标文本

在HTML中用 ```<sup>``` 标记实现上标文字，用 ```<sub>``` 标记实现下标文字。```<sup>``` 和 ```<sub>``` 都是**双标记**，放在开始标记和结束标记之间的文本会分别以上标或下标形式出现。

EG:可以套娃！

在HTML中用```<sup>```标记<sup>实现上标文字，</sup>用```<sub>```标记<sub>实现下标文字。```<sup>```<sup>和```<sub>```<sub>都是双标记，放在开始标记和结束标记之间的文本会分别以上标或下标形式出现。	
	
## 文本排版
	
### 换行和标题

换行标记 ```<br/>``` 与段落标记 ```<p>```

标题标记 ```<h1>～<h6>``` 作为标题，它们的重要性是有区别的，其中 ```<h1>``` 标题的重要性最高，```<h6>``` 的最低。

### 水平分割线

使用 ```<hr />``` 可以创建一条水平线。

<hr />

### 列表 

#### 建立无序列表 ```<ul>```

- 无序列表使用一对标记 ```<ul></ul>```
- 其中每一个列表项使用 ```<li></li>```
- 无序列表项中可以嵌套一个列表
- ```<li></li>``` 标记间又增加了一对 ```<ul></ul>```

```html
<ul>
    <li>列表项第一行</li>
    <li>列表项第二行</li>
    <ul>
    <li>列表嵌套项第一行</li>
    <li>列表嵌套项第二行</li>
    </ul>
    <li>列表项第三行</li>
</ul>
```

<ul>
    <li>列表项第一行</li>
    <li>列表项第二行</li>
    <ul>
    <li>列表嵌套项第一行</li>
    <li>列表嵌套项第二行</li>
    </ul>
    <li>列表项第三行</li>
</ul>

#### 建立有序列表 ```<ol>```

它使用标记 ```<ol></ol>```，每一个列表项使用 ```<li></li>```

```html
<ol>
    <li>列表项第一行</li>
    <li>列表项第二行</li>
    <ol>
    <li>列表嵌套项第一行</li>
    <li>列表嵌套项第二行</li>
    </ol>
    <li>列表项第三行</li>
</ol>
```

<ol>
    <li>列表项第一行</li>
    <li>列表项第二行</li>
    <ol>
    <li>列表嵌套项第一行</li>
    <li>列表嵌套项第二行</li>
    </ol>
    <li>列表项第三行</li>
</ol>

## 插入图像

### 图像标记 ```<img>```
	
在相对路径中，```“..”``` 表示上一级目录，```“../..”``` 表示上级的上级目录，依此类推
路径分隔符使用了 ```“\”和“/”``` 两种，其中 ```“\”``` 表示本地分隔符，```“/”``` 表示网络分隔符。

图像可以美化网页，插入图像使用**单标记** ```<img />```。

> DW 中快速插入图片快捷键为 ctrl+alt+i

```html
<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" alt="img方法" title="img属性值和使用方法"/>
```

<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" alt="img方法" title="img属性值和使用方法"/>

<br>
### 文件路径

> 在相对路径中，```“..”``` 表示上一级目录，```“../..”``` 表示上级的上级目录，依此类推
路径分隔符使用了 ```“\”``` 和 ```“/”``` 两种，其中 ```“\”``` 表示本地分隔符，“/”表示网络分隔符。

绝对路径实例：

```
E:\Webs\images\tp.jpg
```

相对路径实例：

```
./images/tp.jpg
```

### 图片格式

原则上，照片，背景等大图用 jpg ；透明图片使用 png ；动图使用 gif

矢量图 svg ；压缩图 webp

### 图片宽高属性

图片显示的尺寸是由 width 和 height 控制的。当只有其中一个属性时，另一个就以图片原始长宽比例来显示。设定的宽高均为按比例缩放

```html
指定宽高时，图片被压扁
<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" width="250px" height="55px;"/>
```

<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" width="250px" height="55px;"/>

```html
指定宽时，图片按原始比例缩放
<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" width="250px"/>
```

<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" width="250px"/>

```html
指定高时，图片按原始比例缩放
<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" height="55px"/>
```

<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/html-img.jpg" height="55px"/>

## Tips: ```<br/>``` 和 ```<p></p>```

一般来说 ```<br/>``` 间距小于 ```<p></p>``` 不过可以用 CSS 调整他们