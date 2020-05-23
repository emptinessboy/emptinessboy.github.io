---
title: CSS文档整理 01-快速入门
date: 2020-04-03 00:31:23
category: CSS学习
tags: CSS3
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/03/css3_bg.jpg
---

## 概述

CSS（Cascading Style Sheet）称为层叠样式表，也可以称为CSS样式表或样式表，其文件扩展名为.css。CSS是用于增强或控制网页样式，并允许将样式信息与网页内容分离的一种标记性语言。

样式表定义如何显示 HTML 元素。样式通常保存在外部的 .css 文件中。通过仅仅编辑一个简单的 CSS 文档，外部样式表使你有能力同时改变站点中所有页面的布局和外观。

CSS 3 最大的优势是在后期维护中，如果一些外观样式需要修改，就只修改相应的代码即可。


## CSS 基础语法

在前面介绍过，CSS样式表由若干条样式规则组成，这些样式规则可以应用到不同的元素或文档中来定义它们的显示效果。每一条样式规则由三部分构成：选择符（selector）、属性（property）和属性值（value）。其基本格式如下：

```css
selector{
    property:value;
}
```

selector 可以采用多种形式，可以为文档中的 HTML 标记（如 ```<body>、<table>、<p>``` 等），也可以是XML文档中的标记。

value 指定了属性的值。如果定义选择符的多个属性，则属性和属性值为一组，组与组之间用 “;” 隔开。

```css
selector{
    property1:value1;
    property2:value2;
    ……
}
```
## 在 HTML5 中使用 CSS3

CSS 样式表能很好地控制页面显示，分离网页内容和样式代码，它控制 HTML5 页面效果的方式通常包括行内样式、内嵌样式、链接样式和导入样式。

### 行内样式（内联样式）

行内样式是所有样式中比较简单、直观的方法，它可以直接把 CSS 代码添加到HTML文件中，是作为 HTML 的标记属性存在的。通过这种方法，可以很简单地对某个元素单独定义样式。

使用行内样式方法直接在 HTML 标记中使用 style 属性，该属性的内容就是 CSS 的属性和值。例如：

> 提示：如果值为若干单词，则要给值加引号：

```html
<p style="color:red">段落样式</p>
```

下面是两个具体的行内样式案例：

```html
<p style="color:red;font-size:20px;text-decoration:underline;text-align:center">此段落使用行内样式修饰</p>
<p style="color:blue;font-style:italic">正文内容</p>
```

<p style="color:red;font-size:20px;text-decoration:underline;text-align:center">此段落使用行内样式修饰</p>
<p style="color:blue;font-style:italic">正文内容</p>

可以看到两个p标记中都使用了style属性，并且设置了CSS样式，各个样式之间互不影响，分别显示自己的样式效果。第一个段落为红色字体，居中显示且带有下画线；第二个段落为蓝色字体，并以斜体显示。

尽管行内样式简单，但这种方法并不常用，因为这样添加无法完全发挥样式表 “内容结构和样式控制代码分离” 的优势，而且这种方式也不利于样式的重用。如果为每一个标记都设置 style 属性，那么后期维护成本会过高，网页也容易过胖，故不推荐使用。

### 内嵌样式（内部样式表）

内嵌样式就是将CSS样式代码添加到 ```<head>与</head>``` 之间，并且用 ```<style>和</style>``` 标记进行声明。这种写法虽然没有实现页面内容和样式控制代码完全分离，但可以用于设置一些比较简单且需要样式统一的页面。

格式如下：

```html
<head>
    <style>
        p{
            color:red;
            font-size:12px;
        }
    </style>
</head>
```

>TIPS: 有些较低版本的浏览器不识别 ```<style>``` 标记，不能将样式正确地应用到页面显示上，而是直接将标记中的内容以文本的形式显示。为了解决此类问题，可以使用 HMTL 注释将标记中的内容隐藏。如果浏览器能够识别 ```<style>``` 标记，则标记内被注释的 CSS 样式定义代码依旧能够发挥作用。

### 链接样式（外部样式表）

链接样式是 CSS 中使用频率最高，也是最实用的方法。它可以很好地将 “页面内容” 和 “样式风格代码” 分离成两个文件或多个文件，实现了页面框架 HTML 代码和 CSS 代码的完成分离。

基本语法如下：

```html
<head>
    <link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

（1）rel 表示链接到样式表，其值为 stylesheet。（2）type 表示样式表类型为 CSS 样式表。（3）href 指定了CSS样式表文件的路径。

> 在设计整个网站时，为了实现相同的样式风格，可以将同一个 CSS 文件链接到所有的页面中。如果整个网站需要修改样式，则只修改 CSS 文件即可。

### 导入样式（@import方法）

导入样式和链接样式基本相同，都需要创建一个单独的 CSS 文件，然后将其引入到 HTML 文件中，只不过语法和运作方式有所差别。采用导入样式是在 HTML 文件初始化时，会被导入到 HTML 文件内作为文件的一部分，类似于内嵌效果。而链接样式则是在 HTML 标记需要样式风格时才以链接方式引入。

基本代码如下：

```html
<style>
  <!--
    @import "1.css"
    @import "2.css"
  -->
</style>
```

导入外部样式表相当于将样式表导入到内嵌样式表中，其中 @import 必须在样式表的开始部分（即位于其他样式表代码的上面）。

### 样式优先级

当同一个 HTML 元素被不止一个样式定义时，会使用哪个样式呢？

一般而言，所有的样式会根据下面的规则层叠于一个新的虚拟样式表中，其中数字 5 拥有最高的优先权。

1. 浏览器缺省设置
2. 导入样式（@import）
3. 外部样式表
4. 内部样式表（位于 ```<head>``` 标签内部）
5. 内联样式（在 HTML 元素内部）

因此，内联样式（在 HTML 元素内部）拥有最高的优先权，这意味着它将优先于以下的样式声明：```<head>``` 标签中的样式声明，外部样式表中的样式声明，或者浏览器中的样式声明（缺省值）。


## CSS3 选择器

根据 CSS 选择器用途可以把选择器分为标记选择器、类选择器、全局选择器、ID选择器和伪类选择器等。

### 标记选择器

基本语法如下：

```css
tagName{
    property:value;
}
```

其中 tagName 表示标记名称，如 p、h1 等HTML标记；property 表示CSS3属性；value 表示 CSS3 属性值。

通过声明一个具体标记，可以对文档里这个标记出现的每一个地方应用样式定义，**这种做法通常用在设置整个网站都会出现的基本样式。**

下面是一个设置全局默认字体的例子：

```css
body,p,td,th,div,blockquote,dl,ul,ol{
    font-family: Tahome, Verdana, Arial, Helvetica, sans-serif;
    font-size: 1em;
    color: #000000;
}
```

### 类选择器

使用标记选择器可以控制该页面中所有相关标记的显示样式，如果需要对其中一系列标记重新设置，此时仅使用标记选择器是远远不够的，还需要使用类选择器。

常用的语法格式如下：

```css
.classValue{
    property:value;
}
```

classValue 是选择器的名称，具体名称由 CSS 制定者自己命名。如果一个标记具有 class 属性且 class 属性值为 classValue，那么该标记的呈现样式由该选择器指定。在定义类选择符时，需要在 classValue 前面加一个句点 “.”。

下面是一个具体案例：

```html
<style>
.aa{
   color:blue;
   font-size:20px;
}
</style>
<p class="aa">此处使用类选择器aa控制段落样式</p>
```

### ID 选择器

ID 选择器和类选择器类似，都是针对特定属性的属性值进行匹配的。ID 选择器定义的是某一个特定的 HTML 标记，一个网页文件中只能有一个标记使用某一 ID 的属性值。

定义ID选择器的基本语法格式如下：

```css
#idValue{
    property:value;
}
```

在正常情况下，id 属性值在文档中具有唯一性。在定义 ID 选择器时，需要在 idValue 前面加一个 “#” 符号。

> 1）类选择器可以给任意数量的标记定义样式，但ID选择器在页面的标记中只能使用一次。
> 
> 2）ID选择器比类选择器具有更高的优先级，即当ID选择器与类选择器发生冲突时，优先使用ID选择器定义的样式。

由于 JavaScript 等脚本语言也能调用 HTML 中设置的 id，因此 ID 选择器一直被广泛使用。网页设计者在编写 HTML 代码时应该养成一个习惯，一个 id 只赋予一个 HTML 标记。

### 全局选择器

如果想要一个页面中所有 HTML 标记使用同一种样式，就可以使用全局选择器。全局选择器，顾名思义就是对所有 HTML 标记起作用。其语法格式如下：

```css
*{
    property:value;
}
```

其中，“ * ” 表示对所有标记起作用。

### 组合选择器

将多种选择器进行搭配，可以构成一种复合选择器，也称为组合选择器，即将标记选择器、类选择器和 ID 选择器组合起来使用。

一般的组合方式是标记选择器和类选择器组合或标记选择器和ID选择器组合：

```css
tagNme.classValue{property:value;}
```

使用案例：

```html
<style>
p.firstPar{
  color:blue
}
.firstPar{
  color:green
}
</style>
<p class="firstPar">此处使用组合选择器</p>
<h1 class="firstPar">我是一个标题</h1>
```
<style>
p.firstPar{
  color:blue
}
.firstPar{
  color:green
}
</style>
<p class="firstPar">此处使用组合选择器</p>
<span class="firstPar">我是一个标题</span>

### 继承选择器

继承选择器的规则是：子标记在没有定义的情况下所有的样式是继承父标记的；当子标记重新定义父标记已经定义过的声明时，子标记会执行后面的声明，其中与父标记不冲突的地方仍然沿用父标记的声明。

具体格式：

```css
外层 内层 最内层{
    property:value;
} 
```

例如：

```html
<style>
#red p{
    color:red;
}
</style>
<div id="red">
    <p>hello</p>
    <span>hello<hello>
</div>
```

<style>
#red p{
    color:red;
}
</style>
<div id="red">
    <p>hello</p>
    <span>hello<hello>
</div>

### 伪类

伪类也是选择器的一种，但是用伪类定义的 CSS 样式并不是作用在标记上的，而是作用在标记的状态上。

其中有一组伪类是主流浏览器都支持的，就是超链接的伪类，包括 :link、:vistited、:hover和:active。

伪类选择器定义的样式经常应用在标记<a>上，它表示超链接4种不同的状态，即未访问超链接（link）、已访问超链接（visited）、鼠标停留在超链接上（hover）和激活超链接（active）。

示例代码：

```html
<style>
a:link {color: red}		/* 未访问的链接 */
a:visited {color: green}	/* 已访问的链接 */
a:hover {color:blue}	/* 鼠标移动到链接上 */
a:active {color: orange}	/* 选定的链接 */
</style>
<a href="">空的</a>
<a href="#">锚点链接</a>
<a href="https://coding.emptinessboy.com">搜狐</a>
```

<style>
.a a:link {color: red}		/* 未访问的链接 */
.a a:visited {color: green}	/* 已访问的链接 */
.a a:hover {color:blue}	/* 鼠标移动到链接上 */
.a a:active {color: orange}	/* 选定的链接 */
</style>
<div class="a">
    <a href="">空的</a>
    <a href="#">锚点链接</a>
    <a href="https://coding.emptinessboy.com">URL</a>
</div>

### 属性选择器

属性选择器根据某个属性是否存在属性值来寻找元素，因此能够实现某些非常有意思和强大的效果。

现在的CSS3标准共有7个属性选择器，它们共同构成了CSS功能强大的标记属性过滤体系。

选择器|描述
---|---
[attribute]|用于选取带有指定属性的元素。
[attribute=value]|用于选取带有指定属性和值的元素。
[attribute~=value]|用于选取属性值中包含指定词汇的元素。
[attribute\|=value]|用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。
[attribute^=value]|匹配属性值以指定值开头的每个元素。
[attribute$=value]|匹配属性值以指定值结尾的每个元素。
[attribute*=value]|匹配属性值中包含指定值的每个元素。

下面是一个实际案例：

```css
[align]{color:red}
[align="left"]{font-size:20px;font-weight:bolder;}
[lang^="en"]{color:blue;text-decoration:underline;}
[src$="gif"]{border-width:5px;boder-color:#ff9900}
```

### 结构伪类选择器

结构伪类选择器（Structural pseudo-classes）是 CSS3 新增的类型选择器。顾名思义，结构伪类就是利用文档结构树（DOM）实现元素过滤。也就是说，通过文档结构的相互关系来匹配特定的元素，从而减少文档内对class属性和id属性的定义，使得文档更加简洁。

#### 选择器第一类：

选择器|说明
---|---
E:first-child|选择父元素的第一个子元素
E:last-child|选择父元素的最后一个子元素
E:nth-child(n)|选择父元素下的第n个元素或奇偶元素，n的值为 “数字 \| odd \| even”
E:only-child|选择父元素中唯一的子元素（该父元素只有一个子元素）

下面是具体案例：

```html
<style type="text/css">
*{padding:0;margin:0;}
ul
{
    display:inline-block;
    width:200px;
    list-style-type:none;
}
ul li
{
    height:20px;
}
ul li:first-child{background-color:red;}
ul li:nth-child(2){background-color:orange;}
ul li:nth-child(3){background-color:yellow;}
ul li:nth-child(4){background-color:green;}
ul li:last-child{background-color:blue;}
</style>
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```
<style type="text/css">
.demo *{padding:0;margin:0;}
.demo ul
{
    display:inline-block;
    width:200px;
    list-style-type:none;
}
.demo ul li
{
    height:20px;
}
.demo ul li:first-child{background-color:red;}
.demo ul li:nth-child(2){background-color:orange;}
.demo ul li:nth-child(3){background-color:yellow;}
.demo ul li:nth-child(4){background-color:green;}
.demo ul li:last-child{background-color:blue;}
</style>
<div class="demo">
    <ul>
       <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</div>

#### 隔行换色（no-js）

```css
ul li{
    height:20px;
    background-color:green;
}
/*设置偶数列颜色*/
ul li:nth-child(even)
{
    background-color:red;
}
```
<style>
.demo2 *{padding:0;margin:0;}
.demo2 ul{
    display:inline-block;
    width:200px;
    list-style-type:none;
}
.demo2 ul li{
    height:20px;
    background-color:green;
}
.demo2 ul li:nth-child(even)
{
    background-color:red;
}
</style>
<div class="demo2">
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</div>


#### 选择器第二类：

选择器|说明
---|---
:first-of-type|选择同元素类型的第 1 个同级兄弟元素
:last-of-type|选择同元素类型的最后 1 个同级兄弟元素
:nth-of-type（n）|匹配同元素类型的第 n 个同级兄弟元素，n 的值为“数字 \| odd \| even”
:only-of-type|匹配父元素中特定类型的唯一子元素（该父元素可以有多个子元素）

案例：

```html
<div>
    <h1></h1>
    <p></p>
    <span></span>
    <span></span>
</div>

h1:first-child  选择的是 h1 元素，因为 h1 元素是 div 的第1个子元素。
p:first-child   选择不到任何元素，因为 p 并不是 div 的第1个子元素，而是 div 的第2个子元素。

h1: first-of-type   选择的是 h1 元素，因为 h1 元素是 div 中所有 h1 元素中的第1个 h1 元素，事实上也只有一个为 h1 的子元素；
p: first-of-type    选择的是 p 元素，因为 p 元素是 div 中所有 p 元素中的第1个 p 元素，事实上也只有一个为 p 的子元素；
```

#### 选择器第三类：
选择器|说明
---|---
:root|选择文档的根元素。在HTML中，根元素永远是HTML
:not()|选择某个元素之外的所有元素
:empty|选择一个不包含任何子元素或内容的元素
:target|选取页面中的某个target元素

### UI元素状态伪类选择器

UI 元素的状态一般包括 可用、不可用、选中、未选中、获取焦点、失去焦点、锁定、待机等。CSS3定义了3种常用的状态伪类选择器：

选择器|说明
---|---
E:enabled|选择E元素中所有“可用”元素
E:disabled|选择E元素中所有“不可用”元素
E:checked|选择E元素中所有被选中的元素
E:focus|指定元素获得光标焦点时使用的样式
E::selection|改变E元素中被选择的网页文本的显示效果
E:read-write|选择E元素中所有“可读写”元素
E:read-only|选择E元素中所有“只读”元素
E::before|在E元素之前插入内容
E::after|在E元素之后插入内容

#### :enabled 与 :disabled选择器

在 Web 表单中，有些表单元素（如输入框、密码框、复选框等）有 “可用” 和 “不可用” 这2种状态。默认情况下，这些表单元素都处在可用状态。

下面是一段示例代码：

```html
<style>
.demo5 input:enabled {
    border:1px dotted #666;
    background:#ff9900;
}
input:disabled {
    border:1px dotted #999;
    background:#F2F2F2;
}
</style>
<form class="demo5" method="post" action="">
用户名：
<input type=text name=name><br>
密&nbsp;&nbsp;&nbsp;&nbsp;码：
<input type=password name=pass disabled="disabled"><br>
</form>
```

<style>
.demo5 input:enabled {
    border:1px dotted #666;
    background:#ff9900;
}
input:disabled {
    border:1px dotted #999;
    background:#F2F2F2;
}
</style>
<form class="demo5" method="post" action="">
用户名：
<input type=text name=name><br>
密&nbsp;&nbsp;&nbsp;&nbsp;码：
<input type=password name=pass disabled="disabled"><br>
</form>

#### :focus 选择器

下面是一段示例代码：

```html
<style type="text/css">
input:focus
{
    outline:1px solid red;
}
</style>
<p><label for="name">姓名：</label><input type="text" name="name"/></p>
<p><label for="email">邮箱：</label><input type="text" name="email"/></p>

```

<style type="text/css">
.demo3 input:focus
{
    outline:3px solid red;
}
</style>
<div class="demo3">
    <p><label for="name">姓名：</label><input type="text" name="name"/></p>
    <p><label for="email">邮箱：</label><input type="text" name="email"/></p>
</div>

:focus 选择器被用来指定 “表单元素” 获得光标焦点时使用的样式，主要在单行文本框 text、多行文本框 textarea 等表单元素获得焦点并输入文本时使用。

一般情况下，获取焦点和失去焦点是针对单行文本框 text、多行文本框 textarea 这2个表单元素而言。

#### ::selection 选择器

::selection 选择器，默认情况下，浏览器中用鼠标选择的网页文本都是 “深蓝的背景，白色的字体” 显示的。但是有些时候我们并不想要 “深蓝的背景，白色的字体” 这种显示效果。

下面是一段示例代码：

```html
<style type="text/css">
div::selection
{
    background-color:orange;
    color:white;
}
</style>
<div>
    <div>Hello，I am EmptinessBoy</div>
</div>
```

<style type="text/css">
.demo4 div::selection
{
    background-color:orange;
    color:white;
}
.demo4 span::selection
{
    background-color:green;
    color:white;
}
</style>
<div class="demo4">
    <p>Hello，I am EmptinessBoy（正常）</p>
    <div>Hello，I am EmptinessBoy（橙）</div>
    <span>Hello，He is 隔壁老王（被绿了）</span>
</div>

#### ::before 和 ::after选择器

在 CSS3 中，我们可以使用 ::before 和 ::after 这两个选择器在元素前面或后面添加内容。这两个选择器常和 "content属性" 配合使用，使用的场景最多的就是清除浮动和创建小图标。

```html
<style type="text/css">
    p::before{content: "隔壁老王";}
    p::after{content: "被绿了";color: green;}
</style>
<p>有一天</p>
```

<style type="text/css">
.demo6 p::before{content: "隔壁老王";}
.demo6 p::after{content: "被绿了";color: green;}
</style>
<span class="demo6">
    <p>有一天</p>
</span>

### 选择器声明

使用 CSS 选择器可以控制 HTML 标记样式，其中每个选择器属性可以一次声明多个，即创建多个 CSS 属性修饰 HTML 标记。实际上也可以将选择器声明多个，并且任何形式的选择器（如标记选择器、class类别选择器、ID选择器等）都是合法的。

#### 集体声明

集体声明就是在声明各种CSS选择器时，如果某些选择器的风格是完全相同的或者部分相同，可以将风格相同的CSS选择器同时声明。

格式参考如下：

```css
h1,h2,p {
    color:red;              
}
```

#### 多重嵌套声明

参见：[继承选择器](http://localhost:40006/2020/04/CSS%E6%96%87%E6%A1%A3%E6%95%B4%E7%90%86-01-%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/#%E7%BB%A7%E6%89%BF%E9%80%89%E6%8B%A9%E5%99%A8)

## TIPS:

### 统一字体大小

使用 font-size:14px 定义的宋体文字，在IE下实际高是16像素，下空白是3像素，Firefox 浏览器下实际高是17像素、上空1像素、下空3像素。

> 其解决办法是在文字定义上设置 line-height，并确保所有文字都有默认的 line-height 值。
