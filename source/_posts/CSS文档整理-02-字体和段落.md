---
title: CSS文档整理 02-字体和段落
date: 2020-04-14 17:36:10
category: CSS学习
tags: CSS3
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/04/03/css3_bg.jpg
---

注：字体和段落几乎都支持 inherit 继承属性，下文可能部分省略。

## 文字属性

### 字体 font-family

font-family 属性用于指定文字字体类型，如宋体、黑体、等，即在网页中展示字体不同的形状。<!--more-->

#### 字体名称

具体的语法格式如下：

```css
body {font-family: 微软雅黑,宋体;}
```

使用name字体名称，按优先顺序排列，以逗号隔开，如果字体名称包含空格，则应使用引号括起

#### 字体系列

具体的语法格式如下：

```css
body {font-family: sans-serif;}
```

在 CSS 中，有两种不同类型的字体系列名称：

- 通用字体系列 - 拥有相似外观的字体系统组合（比如 "Serif" 或 "Monospace"）
- 特定字体系列 - 具体的字体系列（比如 "Times" 或 "Courier"）

下面是 5 种通用字体系列：

**Serif 字体：** 这些字体成比例，而且有上下短线。如果字体中的所有字符根据其不同大小有不同的宽度，则成该字符是成比例的。

**Sans-serif 字体：** 这些字体是成比例的，而且没有上下短线。

**Monospace 字体：** Monospace 字体并不是成比例的。它们通常用于模拟打字机打出的文本、老式点阵打印机的输出，甚至更老式的视频显示终端。采用这些字体，每个字符的宽度都必须完全相同，所以小写的 i 和小写的 m 有相同的宽度。这些字体可能有上下短线，也可能没有。如果一个字体的字符宽度完全相同，则归类为 Monospace 字体，而不论是否有上下短线。

**Cursive 字体：** 这些字体试图模仿人的手写体。通常，它们主要由曲线和 Serif 字体中没有的笔划装饰组成。

**Fantasy 字体：** 这些字体无法用任何特征来定义，只有一点是确定的，那就是我们无法很容易地将其规划到任何一种其他的字体系列当中。

下面是一个具体案例：

```html
<p style="font-family: serif;">I am Emptinessboy !</p>
<p style="font-family: sans-serif;">I am Emptinessboy !</p>
```

<p style="font-family: serif;">I am Emptinessboy !</p>
<p style="font-family: sans-serif;">I am Emptinessboy !</p>

#### 混搭

可以通过混合特定字体名和通用字体系列来解决兼容性问题：

```html
<p style="font-family: 黑体,serif;">I am Emptinessboy !</p>
```

<p style="font-family: 黑体,serif;">I am Emptinessboy !</p>


### 字号 font-size

在 CSS3 新规定中，通常使用 font-size 设置文字大小，其属性值如下。

```
xx-small | x-small | small | medium | large | x-large| xx-large

把字体的尺寸设置为不同的尺寸，从 xx-small 到 xx-large。默认值：medium。
```
|||
---|---
smaller|把 font-size 设置为比父元素更小的尺寸。
larger|把 font-size 设置为比父元素更大的尺寸。
length|把 font-size 设置为一个固定的值。
%|把 font-size 设置为基于父元素的一个百分比值。
inherit|规定应该从父元素继承字体尺寸。

font-size 值可以是绝对或相对值。绝对值大小在确定了输出的物理尺寸时很有用，但不允许用户在所有浏览器中改变文本大小（不利于可用性）。相对大小：相对于周围的元素来设置大小，允许用户在浏览器改变文本大小。

```html
<div style="font-size:13pt">
    上级标记大小
    <p style="font-size:inherit">inherit 继承</p>
    <p style="font-size:x-small">x-small</p>
    <p style="font-size:x-large">x-large</p>
    <p style="font-size:smaller">smaller</p>
    <p style="font-size:larger">larger</p>
    <p style="font-size:50%">50%</p>
    <p style="font-size:16pt">16pt</p>
</div>
```

<p></p>
<div style="font-size:13pt">
    上级标记大小
    <p style="font-size:inherit">inherit 继承</p>
    <p style="font-size:x-small">x-small</p>
    <p style="font-size:x-large">x-large</p>
    <p style="font-size:smaller">smaller</p>
    <p style="font-size:larger">larger</p>
    <p style="font-size:50%">50%</p>
    <p style="font-size:16pt">16pt</p>
</div>

在上面例子中，font-size 字体大小为 50% 时，其比较对象是上一级标签中的13pt。同样还可以使用 inherit 值，直接继承上级标记的字体大小。

#### 使用 em 来设置字体大小

许多开发者使用 em 单位代替 pixels。W3C 推荐使用 em 尺寸单位。

1em 等于当前的字体尺寸。如果一个元素的 font-size 为 16 像素，那么对于该元素，1em 就等于 16 像素。在设置字体大小时，**em 的值会相对于父元素的字体大小改变。**

浏览器中默认的文本大小是 16 像素。因此 1em 的默认尺寸是 16 像素。

> 可以使用下面这个公式将像素转换为 em：pixels/16=em（注：16 等于父元素的默认字体大小，假设父元素的 font-size 为 20px，那么公式需改为：pixels/20=em）。

所以最推荐的做法是：结合使用百分比和 EM

在所有浏览器中均有效的方案是为 body 元素（父元素）以百分比设置默认的 font-size 值，例如：

```css
body {font-size:100%;}
h1 {font-size:3.75em;}
h2 {font-size:2.5em;}
p {font-size:0.875em;}
```

### 字重 font-weight

格式：

```css
body {font-weight:normal;}
```

属性|定义
---|---
100-900|定义由粗到细的字符。400 等同于 normal，而 700 等同于 bold。
normal|默认值。定义标准的字符。
bold|定义粗体字符。
bolder|定义更粗的字符。
lighter|定义更细的字符。

inherit	规定应该从父元素继承字体的粗细。

下面是具体使用案例：

```html
<p style="font-weight:normal">正常</p>
<p style="font-weight:lighter">细体</p>
<p style="font-weight:bolder">细体</p>
```

<p style="font-weight:normal">正常</p>
<p style="font-weight:lighter">细体</p>
<p style="font-weight:bolder">细体</p>

### 字体风格 font-style

font-style通常用来定义字体风格，即字体的显示样式。在CSS3新规定中，语法格式如下：

```css
body {font-style:normal}
```

该属性有三个值：

- normal - 文本正常显示
- italic - 文本斜体显示
- oblique - 文本倾斜显示

斜体（italic）是一种简单的字体风格，对每个字母的结构有一些小改动，来反映变化的外观。与此不同，倾斜（oblique）文本则是正常竖直文本的一个倾斜版本。

```html
案例：

<p style="font-style:normal">正常</p>
<p style="font-style:italic">italic 斜体</p>
<p style="font-style:oblique">oblique 倾斜</p>
```

<p style="font-style:normal">正常</p>
<p style="font-style:italic">italic 斜体</p>
<p style="font-style:oblique">oblique 倾斜</p>


### 大小写 font-variant

> font-variant 不同于 [text-transform 点击查看](https://coding.emptinessboy.com/2020/04/CSS%E6%96%87%E6%A1%A3%E6%95%B4%E7%90%86-02-%E5%AD%97%E4%BD%93%E5%92%8C%E6%AE%B5%E8%90%BD/#%E6%96%87%E6%9C%AC%E8%BD%AC%E6%8D%A2-text-transform)

属性|含义
---|---
normal|默认值。浏览器会显示一个标准的字体。
small-caps|浏览器会显示小型大写字母的字体。
inherit|规定应该从父元素继承 font-variant 属性的值。

```html
案例：

<p style="font-variant: normal">SETTING normal</p>
<p style="font-variant: small-caps">SETTING small-caps</p>
```

<p style="font-variant: normal">SETTING normal</p>
<p style="font-variant: small-caps">SETTING  small-caps</p>

使用了 small-caps 属性值的段落文本全部变成了大写，只是大写字母的尺寸不同。

### 字体复合属性 font

font 属性可以一次性地使用多个属性的属性值定义文本字体（一句话设置上面一堆属性），其语法格式如下：

```css
body {font:font-style font-variant font-weight font-size font-family}
```

> 注意：font-size 和 font-family 则必须按照固定的顺序出现，如果这两个的顺序不对或缺少一个，那么整条样式规则可能因此会被忽略。

### 字体颜色 color

直接使用 color 属性设置 16 进制值改变颜色。此外 CSS3 中新增加的表现形式，分别是HSL()、HSLA() 和 RGBA()：

```html
<style type="text/css">
    p.normal{color:#00ff00}
    p.ex{color:rgb(0,0,255)}
    p.hs{color:hsl(0,75%,50%)}
    p.ha{color:hsla(120,50%,50%,1)}
    p.ra{color:rgba(125,10,45,0.5)}
</style>
<p class="normal">这是一段普通的段落。</p>
<p class="ex">该段落定义了 class="ex"。该段落中的文本是蓝色的。</p>
<p class="hs">此处使用了CSS3中的新增加的HSL函数，构建颜色。</p>
<p class="ha">此处使用了CSS3中的新增加的HSLA函数，构建颜色。</p>
<p class="ra">此处使用了CSS3中的新增加的RGBA函数，构建颜色。</p>
```

<style type="text/css">
    p.normal{color:#00ff00}
    p.ex{color:rgb(0,0,255)}
    p.hs{color:hsl(0,75%,50%)}
    p.ha{color:hsla(120,50%,50%,1)}
    p.ra{color:rgba(125,10,45,0.5)}
</style>
<p class="normal">这是一段普通的段落。</p>
<p class="ex">该段落定义了 class="ex"。该段落中的文本是蓝色的。</p>
<p class="hs">此处使用了CSS3中的新增加的HSL函数，构建颜色。</p>
<p class="ha">此处使用了CSS3中的新增加的HSLA函数，构建颜色。</p>
<p class="ra">此处使用了CSS3中的新增加的RGBA函数，构建颜色。</p>

## 文本高级样式

### 阴影文本 text-shadow

text-shadow 属性有4个属性值，最后两个是可选的，第一个属性值表示阴影的水平位移，可取正负值；第二个属性值表示阴影垂直位移，可取正负值；第三个属性值表示阴影模糊半径，不可为负值，该值可选；第4个个属性值表示阴影颜色值，该值可选。语法格式如下：

```css
text-shadow: length length opacity color;
```

下面是示例代码：

```html
<p style="text-shadow: .05em .05em .1em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
<p style="text-shadow: .3em .05em .1em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
<p style="text-shadow: .3em .3em .1em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
<p style="text-shadow: .3em .3em .6em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
```

<p style="text-shadow: .05em .05em .1em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
<p style="text-shadow: .3em .05em .1em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
<p style="text-shadow: .3em .3em .1em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>
<p style="text-shadow: .3em .3em .6em purple;font-size: 2em;">Hello, I am EmptinessBoy !</p>

模糊半径是一个长度值，它支持了模糊效果的范围，但如何计算效果的具体算法并没有指定。在阴影效果的长度值之前或之后，还可以指定一个颜色值。颜色值会被用作阴影效果的基础，如果没有指定颜色，那么将使用文本颜色来替代。

### 溢出文本 text-overflow

text-overflow 属性用来定义当文本溢出时是否显示省略标记，即定义省略文本的显示方式，并不具备其他的样式属性定义。

要实现溢出时产生省略号的效果还须定义强制文本在一行内显示（white-space:nowrap）及溢出内容为隐藏（overflow:hidden），只有这样才能实现溢出文本显示省略号的效果。

```css
基本语法：

text-overflow: clip|ellipse;
```

下面是使用的具体案例：

```html
<style type="text/css">
.test_demo_clip{text-overflow:clip; overflow:hidden; white-space:nowrap; width:200px; background:#333;}  
.test_demo_ellipsis{text-overflow:ellipsis;overflow:hidden;white-space:nowrap;width:200px;background:#333;} 
</style>
<p class="test_demo_clip">不显示省略标记，而是简单的裁切条</p>
<p class="test_demo_ellipsis">显示省略标记，不是简单的裁切条</p>
```

<style type="text/css">
.test_demo_clip{text-overflow:clip; overflow:hidden; white-space:nowrap; width:200px; background:#333;}  
.test_demo_ellipsis{text-overflow:ellipsis;overflow:hidden;white-space:nowrap;width:200px;background:#333;} 
</style>
<p class="test_demo_clip">不显示省略标记，而是简单的裁切条</p>
<p class="test_demo_ellipsis">显示省略标记，不是简单的裁切条</p>


### 控制换行 word-wrap

CSS3 中新增加的 word-wrap 文本样式来控制文本换行。其基本语法如下：

```css
word-warp: normal|break-world
```

- normal 只在允许的断字点换行（浏览器保持默认处理）。
- break-world 在长单词或 URL 地址内部进行换行。

下面是具体案例：

```html
<p style="width:11em; border:1px solid #000000;word-wrap:break-word;">This paragraph contains a very long word: thisisaveryveryveryveryveryverylongword. The long word will break and wrap to the next line.</p>

<p style="width:11em; border:1px solid #000000;word-wrap:normal;">This paragraph contains a very long word: thisisaveryveryveryveryveryverylongword. The long word will not break and wrap to the next line.</p>
```

<p style="width:11em; border:1px solid #000000;word-wrap:break-word;">This paragraph contains a very long word: thisisaveryveryveryveryveryverylongword. The long word will break and wrap to the next line.</p>

<p style="overflow:visible; width:11em; border:1px solid #000000;word-wrap:normal;">This paragraph contains a very long word: thisisaveryveryveryveryveryverylongword. The long word will not break and wrap to the next line.</p>

### 字体尺寸适配 font-size-adjust（兼容性差）

实际应用中，只需把 font-size-adjust 属性的值，设置为首选字体的 aspect 值，就可以保证使用备选字体后，文本的显示尺寸不发生变化。

```
公式：

aspect =（x-height）/（font-size）

首选字体的字体尺寸 * （font-size-adjust 值 / 可用字体的 aspect 值）= 可应用到可用字体的字体尺寸
```

举例：如果 14px 的 Verdana（aspect 值是 0.58）不可用，但是某个可用的字体的 aspect 值是 0.46，那么替代字体的尺寸将是 14 * (0.58/0.46) = 17.65px。

下面是一个具体案例：

```html
<style type="text/css">
    /*定义整体样式*/
    div{font-size:16px;}
    #div1{font-family:'Times New Roman';}
    #div2{font-family:Verdana}
</style>
<body>
    <div id="div1">Hello World !</div>
    <div id="div2">Hello World !</div>
</body>
```

<style type="text/css">
    /*定义整体样式*/
    div{font-size:16px;}
    #div1{font-family:'Times New Roman';}
    #div2{font-family:Verdana}
</style>
<body>
    <div id="div1">Hello World !</div>
    <div id="div2">Hello World !</div>
</body>

西方字体的 aspect 值：

字体类型|aspect值
---|---
Fjemish Script|0.28
Caflisch Script Web|0.37
Bernhard Modern|0.4
Gill Sans|0.46
Times New Roman|0.46
Minion Web|0.47
Myriad Web|0.48
Georgia|0.5
Trebuchet MS|0.53
Comic Sans MS|0.54
Verdana|0.58

## 段落属性

### 单词间隔 word-spacing

单词之间的间隔如果设置合理，一是会给整个网页布局节省空间，二是可以给人赏心悦目的感觉，提高用户的阅读效率。在 CSS3 中，可以使用 word-spacing 直接定义指定区域或段落中字符之间的间隔。

属性|值
---|---
normal|默认。定义单词间的标准空间。
length|定义单词间的固定空间。
inherit|规定应该从父元素继承 word-spacing 属性的值。

下面是一个具体案例：

```html
<p style="word-spacing:normal">I am EmptinessBoy</p>
<p style="word-spacing:25px">I am EmptinessBoy</p>
<p style="word-spacing:25px">吼吼吼 吼吼吼</p>
```

<p style="word-spacing:normal">I am EmptinessBoy</p>
<p style="word-spacing:25px">I am EmptinessBoy</p>
<p style="word-spacing:25px">吼吼吼 吼吼吼</p>

>注意：word-spacing 属性不能用于设置文字之间的间隔。

### 字符间隔 letter-spacing

在CSS3中，可以通过 letter-spacing 来设置字符文本之间的距离，这里允许使用负值，这可让字符之间更加紧凑。其语法格式如下：

属性|值
---|---
normal|默认。规定字符间没有额外的空间。
length|定义字符间的固定空间（允许使用负值）。
inherit|规定应该从父元素继承 letter-spacing 属性的值。

下面是一个具体案例：

```html
<p style="letter-spacing: -0.3em">I am EmptinessBoy</p>
<p style="letter-spacing: 1.3em">I am EmptinessBoy</p>
```

<p style="letter-spacing: -0.3em">I am EmptinessBoy</p>
<p style="letter-spacing: 1.3em">I am EmptinessBoy</p>

### 文字修饰 text-decoration

在CSS3中，text-decoration属性是文本修饰属性，该属性可以为页面提供多种文本的修饰效果，如下画线、删除线、闪烁等。text-decoration属性语法格式如下：

值|描述
---|---
none|默认。定义标准的文本。
underline|定义文本下的一条线。
overline|定义文本上的一条线。
line-through|定义穿过文本下的一条线。
blink|定义闪烁的文本。(难兼容)
inherit|规定应该从父元素继承 text-decoration 属性的值。

下面是案例代码：

```html
<p style="text-decoration:none">Hello World!</p>
<p style="text-decoration:underline">Hello World!</p>
<p style="text-decoration:overline">Hello World!</p>
<p style="text-decoration:line-through">Hello World!</p>
<p style="text-decoration:blink">Hello World!</p>
```

<p style="text-decoration:none">Hello World!</p>
<p style="text-decoration:underline">Hello World!</p>
<p style="text-decoration:overline">Hello World!</p>
<p style="text-decoration:line-through">Hello World!</p>
<p style="text-decoration:blink">Hello World!</p>

### 垂直对齐方式 vertial-align

该属性用来设置垂直对齐方式。该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值，这会使元素降低而不是升高。在表格中，这个属性可以用来设置单元格内容的对齐方式。

值|描述
---|---
baseline|默认。元素放置在父元素的基线上。
sub|垂直对齐文本的下标。
super|垂直对齐文本的上标
top|把元素的顶端与行中最高元素的顶端对齐
text-top|把元素的顶端与父元素字体的顶端对齐
middle|把此元素放置在父元素的中部。
bottom|把元素的顶端与行中最低的元素的顶端对齐。
text-bottom|把元素的底端与父元素字体的底端对齐。
length| 
%|使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。
inherit|规定应该从父元素继承 vertical-align 属性的值。

下面是一个具体案例：

```html
这是一幅 <img class="top" border="0" src="/i/eg_cute.gif" /> 位于段落中的图像。

这是一幅 <img class="bottom" border="0" src="/i/eg_cute.gif" /> 位于段落中的图像。
```

<p>
这是一幅 <img style="vertical-align:text-top" border="0" src="https://media.everdo.cn/tank/pic-bed/2020/04/15/eg_cute.gif" /> 位于段落中的图像。

这是一幅 <img style="vertical-align:text-bottom" src="https://media.everdo.cn/tank/pic-bed/2020/04/15/eg_cute.gif" /> 位于段落中的图像。
</p>

> vertical-align属性值还能使用百分比来设置垂直高度

### 文本转换 text-transform

在 CSS 样式中，text-transform 属性可用于设置文本字体的大小写转换。

值|描述
---|---
none|默认。定义带有小写字母和大写字母的标准的文本。
capitalize|文本中的每个单词以大写字母开头。
uppercase|定义仅有大写字母。
lowercase|定义无大写字母，仅有小写字母。
inherit|规定应该从父元素继承 text-transform 属性的值。

> 如果值为 capitalize，则要对某些字母大写，但是并没有明确定义如何确定哪些字母要大写，这取决于用户代理如何识别出各个“词”。

下面是具体使用案例：

```html
<p style="text-transform: uppercase">I am EmptinessBoy !</p>
<p style="text-transform: lowercase">I am EmptinessBoy !</p>
<p style="text-transform: capitalize">I am EmptinessBoy !</p>
<p style="text-transform: normal">I am EmptinessBoy !</p>
```

<p style="text-transform: uppercase">I am EmptinessBoy !</p>
<p style="text-transform: lowercase">I am EmptinessBoy !</p>
<p style="text-transform: capitalize">I am EmptinessBoy !</p>
<p style="text-transform: normal">I am EmptinessBoy !</p>

### 水平对齐方式 text-align


text-align 属性用于定义对象文本的对齐方式。与 CSS2 相比，CSS3 增加了 start、end 和 string 属性值。

属性|说明
--|--
left，right，center|把文本排列到左边，右边，中间。
justify|实现两端对齐文本效果。
inherit|规定应该从父元素继承 text-align 属性的值。

在新增加的属性值中，start 和 end 属性值主要是针对行内元素的（即在包含元素的头部或尾部显示），而 ```<string>``` 属性值主要用于表格单元格中，将根据某个指定的字符对齐。

```html
代码示例：

<p style="text-align: justify">I am EmptinessBoy !</p>
<p style="text-align: left">I am EmptinessBoy !</p>
<p style="text-align: center">I am EmptinessBoy !</p>
<p style="text-align: right">I am EmptinessBoy !</p>
```

<p style="text-align: justify">I am EmptinessBoy !</p>
<p style="text-align: left">I am EmptinessBoy !</p>
<p style="text-align: center">I am EmptinessBoy !</p>
<p style="text-align: right">I am EmptinessBoy !</p>

### 文本缩进 text-indent

在普通段落中，通常首行缩进两个字符，用来表示这是一个段落的开始。同样在网页的文本编辑中可以通过指定属性来控制文本缩进。CSS 的 text-indent 属性可用来设置文本块中首行的缩进。

值|描述
---|---
length|定义固定的缩进。默认值：0。
%|定义基于父元素宽度的百分比的缩进。
inherit|规定应该从父元素继承 text-indent 属性的值。

具体案例：

```html
<p style="text-align: justify;text-indent: 2em">I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !</p>

<p style="text-align: justify;text-indent: 10%">I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !</p>
```

<p style="text-align: justify;text-indent: 2em">I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !</p>

<p style="text-align: justify;text-indent: 10%">I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !</p>

### 文本行高 line-height

在 CSS 中，line-height 属性用来设置行间距，即行高。

值|描述
---|---
normal|默认。设置合理的行间距。
number|设置数字，此数字会与当前的字体尺寸相乘来设置行间距。
length|设置固定的行间距。
%|基于当前字体尺寸的百分比行间距。
inherit|规定应该从父元素继承 line-height 属性的值。

```html
<p style="line-height:15px">
I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !
</p>
<p style="line-height:200%">
I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !
 </p>
```

<p style="line-height:15px">
I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !
</p>
<p style="line-height:200%">
I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy ! I am EmptinessBoy !
 </p>

### 处理空白 white-sapce

> **空白字符：** 在网页文本编辑中，有时需要包含一些不必要的制表符、换行符或额外的空白符（多于单词之间的一个标准的空格），这些符号统称为空白字符。通常情况下，浏览器可以自动忽略这些额外的空白字符并按照一种适合窗口的方式布置文本。它会丢弃段落开头和结尾处任何额外的空白，并将单词之间的所有制表符、换行和额外的空白压缩（合并）成单一的空白字符。此外，当用户调整窗口大小，时浏览器会根据需要重新格式化文本以便匹配新的窗口尺寸。对于某些元素，可能会以某种方式特意格式化文本以便包含额外的空白字符，而不抛弃或压缩这些字符。

white-space 属性用于设置对象内空格字符的处理方式，该属性对文本的显示有着重要的影响。在标记上应用 white-space 属性可以影响浏览器对字符串或文本间空白的处理方式。


值|描述
---|---
normal|默认。空白会被浏览器忽略。
pre|空白会被浏览器保留。其行为方式类似 HTML 中的 ```<pre>``` 标签。
nowrap|文本不会换行，文本会在在同一行上继续，直到遇到 ```<br>``` 标签为止。
pre-wrap|保留空白符序列，但是正常地进行换行。
pre-line|合并空白符序列，但是保留换行符。
inherit|规定应该从父元素继承 white-space 属性的值。

示例代码：

```html
<p style="white-space: pre-wrap;">
    I am EmptinessBoy  !
I am EmptinessBoy  !
I am EmptinessBoy  !
</p>

<p style="white-space: nowrap;">
    I am EmptinessBoy  !
I am EmptinessBoy  !
I am EmptinessBoy  !
</p>
```

<p style="white-space: pre-wrap;">
    I am EmptinessBoy  !
I am EmptinessBoy  !
I am EmptinessBoy  !
</p>

<p style="white-space: nowrap;">
    I am EmptinessBoy  !
I am EmptinessBoy  !
I am EmptinessBoy  !
</p>

### 文本反排

在网页文本编辑中，通常英语文档的基本方向是从左至右。如果文档中某一段的多个部分包含从右至左阅读的语言，此时可以通过 CSS 提供的 unicode-bidi 和 direction 两个属性解决文本反排的问题。

#### unicode-bidi

（这里我也没咋搞明白）

- normal 元素不会对双向算法打开附加的一层嵌套。对于行内元素，顺序的隐式重排会跨元素边界进行。

- embed 如果是一个行内元素，这个值对于双向算法会打开附件的一层嵌套。这个嵌套层的方向由 direction 属性指定。会在元素内部隐式地完成顺序重排。这对应于在元素开始处增加一个 LRE（对于 direction:ltr ：U+202A）或 RLE（对于 direction:rtl ：U+202B），并在元素的最后增加一个 PDF（U+202C）。

- bidi-override 这会为行内元素创建一个覆盖。对于块级元素，将为不在另一块中的行内后代创建一个覆盖。这说明，顺序重排在元素内部严格按照 direction 属性进行；忽略了双向算法的隐式部分。这对应于在元素开始处增加一个 LRO（对于 direction:ltr ：U+202D）或 RLO（对于 direction:rtl ：U+202E），并在元素最后增加一个 PDF（U+202C）。

#### direction

direction属性用于设置文本流的方向：

值|描述
---|---
ltr|默认。文本方向从左到右。
rtl|文本方向从右到左。
inherit|规定应该从父元素继承 direction 属性的值。

下面是具体样例：

```html
默认右对齐反转：

<p style="direction:rtl; unicode-bidi:bidi-override">1234567890</p>
```

<p style="direction:rtl; unicode-bidi:bidi-override">1234567890</p>
