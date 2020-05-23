---
title: HTML文档整理 03-超链接和iFrame
date: 2020-03-13 17:00:29
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

## URL概念

例如：[https://coding.emptinessboy.com/feed.xml](https://coding.emptinessboy.com/feed.xml)

（协议https）:// (主机名/域名) / (路径)

### 相对 URL 和 绝对 URL

（1）绝对URL一般用于访问非同一台服务器上的资源。

<!--more-->

（2）相对URL是指访问同一台服务器上相同文件夹或不同文件夹中的资源。如果访问相同文件夹中的文件，只需要写文件名；如果访问不同文件夹中资源，URL以服务器的根目录为起点，指明文件的相对关系，由文件夹名和文件名两部分构成。

```html
URL绝对路径： <a href="https://coding.emptinessboy.com/feed.xml">robots.txt</a>
URL相对路径： <a href="/feed.xml">robots.txt</a>
URL相对路径： <a href="../../../feed.xml">robots.txt</a>
```

URL绝对路径： <a href="https://coding.emptinessboy.com/feed.xml">robots.txt</a>
URL相对路径： <a href="/feed.xml">robots.txt</a>
URL相对路径： <a href="../../../feed.xml">robots.txt</a>

## 超链接标记

建立超链接所使用的HTML标记为 ```<a></a>```。超链接最重要的两个要素是超链接指向的目标地址和设置为超链接的网页元素。基本的超链接结构如下：

```html
<a href="URL">网页元素</a>
```

## 文本和图片的超链接

文本超链接和图片超链接通过 ```<a></a>``` 标记实现，将文本或图片放在 ```<a>``` 开始标记和 ```</a>``` 结束标记之间即可建立超链接。

```html
<a href="https://coding.emptinessboy.com/">Emptinessboy</a>
<a href="https://coding.emptinessboy.com/"><img src="https://coding.emptinessboy.com/img/logo.png" /></a>
```
<a href="https://coding.emptinessboy.com/">Emptinessboy</a><br>
<a href="https://coding.emptinessboy.com/"><img src="https://coding.emptinessboy.com/img/logo.png" width="80px;" /></a>

## 超链接对象类型

超链接不但可以链接到各种类型（如图片文件、声音文件、视频文件、word等）的文件，还可以链接到其他网站、ftp服务器、电子邮件等。

如果超链接对象是浏览器能够识别的类型，就会直接在浏览器中显示；如果是浏览器不能识别的类型，则会触发下载对话框。

### 对象之电子邮件

电子邮件链接可以实现，当访问者单击某个链接以后，会自动打开电子邮件客户端软件（如Outlook或Foxmail等）

```html
<a href="mailto:i@my.huxiaofan.com">发邮件给 i@my.huxiaofan.com</a>
```
<a href="mailto:i@my.huxiaofan.com">发邮件给 i@my.huxiaofan.com</a>

### 对象之电话号码

电话号码链接可以实现，当访问者单击某个链接以后，会自动打开手机里的拨号器。

```html
<a href="tel:123456789">我怎么可能把电话告诉你呢/dog</a>
```
<a href="tel:123456789">我怎么可能把电话告诉你呢/dog</a>

点击后大概就是下面这样的效果啦！！

[![html_tel.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/html_tel.jpg)](https://up.media.everdo.cn/image/5d6)

（^_^ 一加五还能战！！！

## 新窗口打开超链接

默认情况下，当单击超链接时，目标页面会在当前窗口中显示并替换掉当前页面的内容。

如果要实现在单击某个超链接后在新的浏览器窗口中显示目标页面，就需要使用 ```<a>``` 标记的 target 属性。target 属性取值有4个：```_blank、_self、_top、_parent```。由于HTML5不再支持框，所以 ```_top、_parent```这两个取值不常用。

其中，```_blank``` 表示在新窗口中显示超链接页面；```_self``` 表示在当前窗口中显示超链接页面。当省略 ```target``` 属性时，默认取值为 ```_self```。

```html
<a href="https://coding.emptinessboy.com/">默认_self属性</a>
<a href="https://coding.emptinessboy.com/" target="_self">指定_self属性</a>
<a href="https://coding.emptinessboy.com/" target="_blank">使用_blank属性</a>
```

<a href="https://coding.emptinessboy.com/">默认_self属性</a>
<a href="https://coding.emptinessboy.com/" target="_self">指定_self属性</a>
<a href="https://coding.emptinessboy.com/" target="_blank">使用_blank属性</a>

## 热点区域（进阶）

热点区域或称超链接的触发区域。

当单击一张图片的不同区域时会显示不同的链接内容，这就是图片的热点区域。所谓图片的热点区域就是将一个图片划分成若干个链接区域。访问者单击不同的区域会链接到不同的目标页面。

在HTML中，可以为图片创建3种类型的热点区域：矩形、圆形和多边形。创建热点区域使用标记 ```<map> </map>``` 和 ```<area>```，语法格式如下：

### 案例（例子来自 w3school.com.cn）

```html
<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/eg_planets.jpg" width="215px" height="260px" usemap="#pic" />
<map name="pic" id="#pic">
    <area shape="rect" coords="0,0,110,260" href="https://up.media.everdo.cn/image/83Q" target="_blank" /> 
    图片左半边太阳部分热区域（0，0），（110，260）
    <area shape="circle" coords="129,161,10" href="https://up.media.everdo.cn/image/aEJ" target="_blank" /> 
    水星的热区域（120，161），r=10
    <area shape="poly" coords="165,150,190,150,180,120" href="https://up.media.everdo.cn/image/gUy" target="_blank" /> 
    金星热区域使用三角形演示 （160，150），（190，150），（180，120）
</map>
```
<p>
<img src="https://media.everdo.cn/tank/pic-bed/2020/03/13/eg_planets.jpg" width="215px" height="260px" usemap="#pic" />
<map name="pic" id="#pic">
    <area shape="rect" coords="0,0,110,260" href="https://up.media.everdo.cn/image/83Q" target="_blank" />
    <area shape="circle" coords="129,161,10" href="https://up.media.everdo.cn/image/aEJ" target="_blank" />
    <area shape="poly" coords="165,150,190,150,180,120" href="https://up.media.everdo.cn/image/gUy" target="_blank" />
</map>
</p>

### 代码解读

> img 元素中的 "usemap" 属性引用 map 元素中的 "id" 或 "name" 属性（根据浏览器），所以我们同时向 map 元素添加了 "id" 和 "name" 属性。

（1）要想建立图片热点区域，必须先插入图片。注意，图片必须增加 usemap 属性，说明该图像是热区映射图像，属性值必须以 ```“#”``` 开头，如 ```#pic```。

（2）```img``` 元素中的 ```"usemap"``` 属性引用 ```map``` 元素中的 ```"id"``` 或 ```"name"``` 属性（根据浏览器），所以我们同时向 ```map``` 元素添加了 ```"id"``` 和 ```"name"``` 属性。(已知 Chrome 是使用 name 属性的！！！)

（3）```<area>``` 总是嵌套在 ```<map>``` 标签中。它定义图像映射中的区域，主要是定义热点区域的形状及超链接。它有3个相应的属性：

- shape属性，控件划分区域的形状，其取值有3个，分别是 rect（矩形）、circle（圆形）和 poly（多边形）。
  
  - 如果 shape 属性取值为 rect，那么 coords 的设置值分别为矩形的左上角 x、y 坐标点和右下角x、y坐标点，单位为像素。
  - 如果 shape 属性取值为 circle，那么 coords 的设置值分别为圆形圆心 x、y 坐标点和半径值，单位为像素。
  - 如果 shape 属性取值为 poly，那么 coords 的设置值分别为多边形在各个点 x、y 坐标，单位为像素。

- coords 属性，控制区域的划分坐标。

- href 属性是为区域设置超链接的目标，设置值为 ```“#”``` 时，表示为空链接。

>上面示例运行结果截图如下：<br><br>[![html_maparea.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/html_maparea.jpg)](https://up.media.everdo.cn/image/K8S)

### DreamWeaver 实现

使用Dreamweaver CC可以很方便地快速且能精确定位热点区域。

01 创建一个HTML文档，插入一个图片文件。（这里以我之前搭建的公众号的网站 [Everdo博客](https://blog.everdo.cn) 的 banner 为例）

[![map-area.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/map-area.jpg)](https://up.media.everdo.cn/image/H4xl)

02 选中图片，在Dreamweaver CC中打开【属性】面板，面板左下角有3个蓝色图标按钮，依次代表矩形、圆形和多边形热点区域。单击左边的【矩形热点】工具图标

[![map-area-1.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/map-area-1.jpg)](https://up.media.everdo.cn/image/HHC0)

03 在设计视图，将鼠标指针移动到图片上，从左上方向右下方拖曳，得到矩形区域

[![map-area-2.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/map-area-2.jpg)](https://up.media.everdo.cn/image/HPJD)

04 如果绘制出来的矩形热区有误差，可以通过【属性】面板中的【指针热点】工具进行编辑

05 完成上述操作之后，保持矩形热区被选中状态，然后在【属性】面板中的【链接】文本框中输入该热点区域链接对应的跳转目标页面。

[![map-area-3.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/map-area-3.jpg)](https://up.media.everdo.cn/image/HIdL)

06 到此为止，使用热点区域制作网站的导航就完成了。此时页面相应的HTML源代码如下：

[![map-area-4.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/map-area-4.jpg)](https://up.media.everdo.cn/image/Hh1c)

>Tips：不推荐使用 HTML 的 热点map 属性来创建 banner，这个工具更适合用来创建地图里的超链接。

## 浮动框架 iFrame

HTML5中已经不支持frameset框架，但是它仍然支持iframe浮动框架的使用。浮动框架可以自由控制窗口大小，可以配合表格随意地在网页的任何位置插入窗口。

### 基本格式

使用iframe创建浮动框架的格式如下：

```html
<iframe src="链接对象"> </iframe>
```

其中，src表示浮动框架中显示对象的路径，可以是绝对路径，也可以是相对路径。

### 高级属性

属性|值|描述
---|---|---
src|URL|规定在 iframe 中显示的文档的 URL。
srcdoc|HTML_code|规定在 ```<iframe>``` 中显示的页面的 HTML 内容。
align|left，right，top，middle，bottom|不赞成使用。请使用样式代替。规定如何根据周围的元素来对齐此框架。
frameborder|1，0|规定是否显示框架周围的边框。
width|pixels %|定义 iframe 的宽度。
height|pixels %|规定 iframe 的高度。
longdesc|URL|规定一个页面，该页面包含了有关 iframe 的较长描述。
marginheight|pixels|定义 iframe 的顶部和底部的空白边距。
marginwidth|pixels|定义 iframe 的左侧和右侧的空白边距。
name|frame_name|规定 iframe 的名称。name 属性用于在 JavaScript 中引用元素，或者作为链接的目标。
sandbox|""，allow-forms，allow-same-origin，allow-scripts，allow-top-navigation|启用一系列对 ```<iframe>``` 中内容的额外限制。
scrolling|yes,no,auto|规定是否在 iframe 中显示滚动条。

### 进阶样例

这里的例子使用 jquery 方式使得 iframe 高度自适应文档内容(由于js载入框架不能跨域 **[见补充内容](#%E8%A1%A5%E5%85%85%EF%BC%9AiFrame-%E8%B7%A8%E5%9F%9F%E9%97%AE%E9%A2%98)**，代码运行结果暂时使用纯的 html 进行 iFrame)。完整JS载入的 iFrame 效果看我博客页面 [https://huxiaofan.com/diary/everdo-shengdanjie/](https://huxiaofan.com/diary/everdo-shengdanjie/)

```html
ps：这个例子是我做的一期公众号交互推文，是不是很好看呀！！喵喵喵

<iframe name="hxf" onload="this.height=hxf.document.body.scrollHeight" src="https://huxiaofan.com/doc/2019-12-25/everdo-hxf-blog.html" frameborder="0" scrolling="no" width="100%" height="0px">加载中……</iframe>
```

<a href="https://huxiaofan.com/diary/everdo-shengdanjie/" target="_blank">
<iframe name="hxf" src="https://huxiaofan.com/doc/2019-12-25/everdo-hxf-blog.html" frameborder="0" scrolling="yes" width="100%" height="800px">加载中……</iframe>
</a>

<br>

### 补充：iFrame 跨域问题

我们可以通过在服务端设置HTTP头部中的 X-Frame-Options（旧式浏览器） 和 Content-Security-Policy（新式浏览器） 信息来控制允许哪些站点对我们进行 iFrame。

这里我们为了让本站域名 coding.emptinessboy.com 可以引用我博客 huxiaofan.com 的 html,因此需要在 nginx.conf 添加.在服务端设置的方式如下：

```nginx
Nginx 配置:
add_header X-Frame-Options "ALLOW-FROM coding.emptinessboy.com huxiaofan.com";
add_header Content-Security-Policy "frame-ancestors coding.emptinessboy.com huxiaofan.com";
```

目前出于安全考虑，无法 ```<iframe>``` 使用JavaScript 访问其他来源的内容，如果可以的话，这将是一个巨大的安全漏洞。对于同源策略， 浏览器会阻止脚本尝试访问来源不同的框架。

如果未保留地址的以下至少之一，则认为起源是不同的：

```html
<protocol>://<hostname>:<port>/...
```

如果要访问框架，协议，主机名和端口必须与原始域相同