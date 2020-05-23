---
title: JS简单入门 05BOM与DOM对象
date: 2020-03-30 02:48:22
category: JS学习
tags: javascript
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/27/JavaScript-Web-Frameworks-Software.jpg
---

BOM 对象包括 window (窗口）、navigator (浏览器程序）、screen (屏幕）、location (地址）、history (历史）和 document (文档）等对象，**主要用于操纵浏览器窗口的行为和特征。**

DOM 是处理 HTML 文档的标准技术，允许 JavaScript 程序动态访问、更新浏览页面的内容、结构和样式。

## BOM 对象

浏览器对象模型（Browser Object Model (BOM)）允许 JavaScript 与浏览器对话。

其中 window 对象是浏览器的窗口，它是整个BOM 的核心，位于BOM 对象的最顶层。

[![window.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/30/window.jpg)](https://up.media.everdo.cn/image/HNPj)

### window 对象

window 对象表示整个浏览器窗口，用千获取浏览器窗口的大小、位置，或设置定时器等。

#### 属性和方法

属性|说明
---|---
document 、history 、location 、navigator 、screen|返回相应对象的引用。例如 document 展性返回 document 对象的引用
parent 、self 、top|分别返回父窗口、当前窗口和最顶层窗口的对象引用
screen Left 、screenTop 、screenX 、screenY|返回窗口的左上角在屏幕上的 X 、Y 坐标。FireFox 不支持 screenLeft 、screenTop, IE8 及更早的IE 版本不支待 screenX 、screenY
innerWidth 、innerHeight|分别返回窗口的文档显示区域的宽度和高度
outerWidth 、outerHeight|分别返回窗口的外部宽度和高度
closed|返回窗口是否已被关闭
opener|返回对创建此窗口的面口引用

方法|说明
---|---
open()、close()|打开或关闭浏览器窗口
alert()、confirm() 、prompt()|分别表示弹出警告框、确认框、用户输入框
moveBy() 、moveTo()|以窗口左上角为基准移动窗口， moveBy() 是按偏移量移动， moveTo() 是移动到指定的屏幕坐标
scrollBy()、scrollTo()|scrollBy() 是按偏移量滚动内容，scrollTo() 是滚动到指定的坐标
setTimeout()、clearTimeout()|设置或清除普通定时器
setlnterval()、clearlnterval()|设嚣或清除周期定时器

#### 基本使用

> 因为 window 对象是最顶层的对象，所以调用它的属性或方法时可以省略 window 。

```html
<button onclick="getSize()">点我获取窗口尺寸</button>
<script type="text/javascript">
function getSize(){
    var width = window.innerWidth;     //获取文档显示区域宽度
    var height = innerHeight;          //获取文档显示区域高度（省略window）
    window.alert(width+"*"+height);	   //调用alert输出
}
</script>
```

<button onclick="getSize()">点我获取窗口尺寸</button>
<script type="text/javascript">
function getSize(){
    var width = window.innerWidth;     //获取文档显示区域宽度
    var height = innerHeight;          //获取文档显示区域高度（省略window）
    window.alert(width+"*"+height);	   //调用alert输出
}
</script>

#### 打开和关闭窗口

window.open() 方法用于打开新窗口， window.close() 方法用于关闭窗口。其中打开的子窗口可以单独设置如下的属性：

属性|说明
---|---
width|窗口的宽度
height|窗口的高度
scrollbars|是否显示滚动条，默认为yes
resizable|是否可洞节窗口大小，默认为yes
titlebar|是否显示标题栏，默认为yes
location|是否显示地址栏，默认为yes
menubar|是否显示菜单栏，默认为yes
toolbar|是否显示工具栏，默认为yes
status|是否显示状态栏，默认为yes

下面是一个具体案例：

```html
<script language="javascript">
var myWindow;
function openNewWin()
{
	//打开一个窗口
	myWindow=window.open("https://huxiaofan.com/about/","myWindow","width=800,height=450,top=200,left=100");
}
function closeNewWin()
{
	//关闭一个窗口
	myWindow.close();
}
</script>
</head>
<body>
<p><a href="javascript:openNewWin()">点我打开新窗口</a></p>
<p><a href="javascript:closeNewWin()">点我关闭新窗口</a></p>
```

<script language="javascript">
var myWindow;
function openNewWin()
{
	//打开一个窗口
	myWindow=window.open("https://huxiaofan.com/about/","myWindow","width=800,height=450,top=200,left=100");
}
function closeNewWin()
{
	//关闭一个窗口
	myWindow.close();
}
</script>
</head>
<body>
<p><a href="javascript:openNewWin()">点我打开新窗口</a></p>
<p><a href="javascript:closeNewWin()">点我关闭新窗口</a></p>

#### 两种定时器使用

##### setTimeout()

setTimeout() 定时器可以实现延时操作，即延时一段时间后执行指定的代码。其基本语法如下：

```javascript
setTimeout(被执行的函数名, 毫秒) ;
```

下面是一个具体案例：

```html
<button onclick="out()">点我后等待三秒</button>
<script>
function show(){
alert("2.5 秒已经过去了");
}
function out(){
    setTimeout(show, 2500);//2.5 秒后调用show 函数
}
</script>
```

<button onclick="out()">点我后等待三秒</button>
<script>
function show(){
alert("2.5 秒已经过去了");
}
function out(){
    setTimeout(show, 2500);//2.5 秒后调用show 函数
}
</script>

当需要清除定时器时，可以使用 clearTimeout() 方法：

```html
<button onclick="clearTimeOutDemo()">清除定时器示例代码</button>
<script>
function showA () {
alert( " 定时器A ");
}
function showB() {
alert( " 定时器B ");
}
function clearTimeOutDemo(){
    var t1 = setTimeout (showA, 2000 ); //设置定时器t1, 2 秒后调用showA 函数
    var t2 = setTimeout (showB, 2000) ; //设置定时器t2 , 2 秒后调用showB 函数
    clearTimeout(t1);
}
</script>
```

<button onclick="clearTimeOutDemo()">清除定时器示例代码</button>
<script>
function showA () {
alert( " 定时器A ");
}
function showB() {
alert( " 定时器B ");
}
function clearTimeOutDemo(){
    var t1 = setTimeout (showA, 2000 ); //设置定时器t1, 2 秒后调用showA 函数
    var t2 = setTimeout (showB, 2000) ; //设置定时器t2 , 2 秒后调用showB 函数
    clearTimeout(t1);
}
</script>

上述代码清除了 t1 定时器，所以只会执行 showB() 的代码。

##### setlnterval()

setlnterval() 定时器用于周期性执行脚本， 即每隔一段时间执行指定的代码，通常用于在网
页上显示时钟、实现网页动画、制作漂浮广告等。需要注意的是，如果不使用 clearInterval() 清
除定时器， 该方法会一直循环执行，直到页面关闭为止。

下面是一个具体案例：

```html
<script language="javascript">
function showTime(){
	var now=new Date();
	var dataTime=now.toLocaleTimeString();
	time=document.getElementById("time");
    time.innerHTML=dataTime;
}
var timer=window.setInterval("showTime()",1000);
function clear(){
	window.clearInterval(timer);
	window.status="已取消定时器";
}
</script>
</head>
<body>
<div id="time"></div>
<p><a href="javascript:clear()">取消定时器</a></p>
```

<script language="javascript">
function showTime(){
	var now=new Date();
	var dataTime=now.toLocaleTimeString();
	time=document.getElementById("time");
    time.innerHTML=dataTime;
}
var timer=window.setInterval("showTime()",1000);
function clear(){
	window.clearInterval(timer);
	window.status="已取消定时器";
}
</script>
</head>
<body>
<div id="time"></div>
<p><a href="javascript:clear()">取消定时器</a></p>

### screen 对象

screen 对象用于获取用户计算机的屏幕信息，例如屏幕分辨率、颜色位数等。screen 对象的常用属性如下：

属性|说明
---|---
width 、height|屏幕的宽度和高度
availWidth 、availHeight|屏幕的可用宽度和可用高度（不包括Windows 任务栏）
colorDepth|屏幕的颜色位数

```html
<button onclick="isHdScreen()">检测一下你的屏幕</button>
<script>
function isHdScreen(){
    //获取屏幕分辨率
    var width= screen.width;
    var height= screen.height;
    //判断屏幕分辨率
    if (width<1920 || height<1080)
        alert("您的屏幕分辨率不足1920*1080, 不是高清屏幕");
    else
        alert("恭喜你的屏幕是分辨率大于等于 1080P 的高清屏幕");
}
</script>
```

<script>
function isHdScreen(){
    //获取屏幕分辨率
    var width= screen.width;
    var height= screen.height;
    //判断屏幕分辨率
    if (width<1920 || height<1080)
        alert("您的屏幕分辨率不足1920*1080, 不是高清屏幕");
    else
        alert("恭喜你的屏幕是分辨率大于等于 1080P 的高清屏幕");
}
</script>
<button onclick="isHdScreen()">检测一下你的屏幕</button> 尝试调整系统分辨率，看看是否有弹窗（嘻嘻

### location 对象

location 对象用千获取和设置当前网页的URL 地址，其常用的属性和方法如下：

属性 / 方法|说明
---|---
hash|获取或设置 URL 中的描点， 例如 "#top"
host|获取或设置 URL 中的主机名，例如 "itcast.cn"
port|获取或设嚣 URL 中的端口号，例如 "80"
href|获取或设置整个 URL, 例如 "https://coding.emptinessboy.com/"
pathname|获取或设置 URL 的路径部分，例如 "/2020/03/JS简单入门-05BOM与DOM对象/"
protocol|获取或设置 URL 的协议，例如 "http:"
search|获取或设置 URL 地址中的GET 请求部分，例如 "?name=EmptinessBoy&age=19"
reload()|重新加载当前文档

#### · 跳转到新地址

```javascript
location.href = "https://coding.emptinessboy.com/";
```

#### · 进入到指定的描点

```javascript
location.hash= "#属性和方法";
```
<button onclick="location.hash= '#属性和方法'">点我跳转锚点</button>

#### · 检测协议并提示用户

```javascript
if (location.protocol == "http:") {
    if (confirm("您在使用不安全的 http 协议，是否切换到更安全的 https 协议?")) {
        location.href = "https://coding.emptinessboy.com/";
    }
}
```

<script>
if (location.protocol == "http:") {
    if (confirm("您在使用不安全的 http 协议，是否切换到更安全的 https 协议?")) {
        location.href = "https://coding.emptinessboy.com/";
    }
}
</script>

上述代码实现了当页面打开后自动判断当前的协议。当用户以 http 协议访问时，会弹出一
个提示框提醒用户是否切换到 https 协议。

#### · history 对象

history 对象最初的设计和浏览器的历史记录有关，但出于隐私方面的考虑，该对象不再被
允许获取用户访问过的 URL 历史。history 对象主要的作用是控制浏览器的前进和后退.

方法|说明
---|---
back()|加载历史记录中的前—个 URL （相当于后退）
forward()|加载历史记录中的后一个 URL （相当于前进）
go()|加载历史记录中的某个页面

下面是一段示例代码：

```html
<button onclick="history.back()">后退</button>
<button onclick="history.go(-1)">后退1页</button>
<button onclick="history.forward()">前进</button>
<button onclick="history.go(1)">前进1页</button>
<button onclick="history.go(0)">重新载入页面</button>
```
<p>
<button onclick="history.back()">后退</button>
<button onclick="history.go(-1)">后退1页</button>
<button onclick="history.forward()">前进</button>
<button onclick="history.go(1)">前进1页</button>
<button onclick="history.go(0)">重新载入页面</button>
</p>

> 上述代码实现了浏览器前进与后退的控制。其中， history.go(-1) 与 history.back() 的作用相
同， history.go(1) 与 history.forward() 的作用相同。

### document 对象

> document 对象和 下面要展开的 DOM 对象是一回事（小声

document 对象用于处理网页文档，通过该对象可以访问文档中所有的元素。document 对象的常用属性和方法。

属性／方法|说明
---|---
body|访问<body> 元素
lastModified|获得文档最后修改的日期和时间
referrer|获得该文档的来路 URL 地址，当文档通过超链接被访问时有效
title|获得当前文档的标题
write()|向文档写 HTML 或 JavaScript 代码

在使用时，通过“document" 或“window . document" 即可表示该对

## DOM 对象

### 概述

Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

DOM ( Document Object Model) 被称为文档对象模型，是一个表示和处理文档的应用程序接口(API ) ，可用千动态访问、更新文档的内容、结构和样式。DOM 将网页中文档的对象关系规划为节点层级，构成它们之间的等级关系，这种各对象间的层次结构被称为节点树：

[![dom.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/30/dom.jpg)](https://up.media.everdo.cn/image/HkeO)

- 每个节点树有—个根节点
- 除了根节点，每个节点都有一个父节点
- 每个节点都可以有许多的子节点
- 具有相同父节点的节点叫做 “兄弟节点”

### 节点的访问

在 DOM 中，每个节点都是—个对象，因此每个节点对象都具有一系列的属性、方法。JavaScript 通过使用节点的属性和方法可以访问指定元素和相关元素，从而得到文档中的各个元素对象。

#### · 访问指定元素

一个元素对象可以拥有元素节点、文本节点、子节点或其他类型的节点

方法|说明
--|--
open()|打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出。
close()|关闭用 document.open() 方法打开的输出流，并显示选定的数据。
write()|向文档写 HTML 表达式 或 JavaScript 代码。
writeln()|等同于 write() 方法，不同的是在每个表达式之后写一个换行符。
getElementById()|返回对拥有指定 id 的第一个对象的引用。
getElementsByName()|返回带有指定名称的对象集合。
getElementsByTagName()|返回带有指定标签名的对象集合。
getElementsByClassName()|获取指定 class 的元素对象集合

下面是一个访问元素的具体案例：

```html
<script type="text/javascript">
function init(){
    var one = document.getElementById("one");  //找到<li id="one">的元素
    one.style.fontWeight = "bold";   //将文本加粗
    var lis = document.getElementsByTagName("li");  //找到所有li元素
    lis[3].style.color = "#8a2be2";   //将第四个li元素的字体颜色设置为 #8a2be2
}
</script>
<body onload="init()"> <!-- nload事件在页面或图像加载完成之后立即执行 -->
 	<ul>
 		<li id="one">标题一</li>
 		<li id="two">标题二</li>
 		<li id="three">标题三</li>
 		<li id="four">标题四</li>
 	</ul>
</body>
```

<script type="text/javascript">
function init(){
    var one = document.getElementById("one");  //找到<li id="one">的元素
    one.style.fontWeight = "bold";   //将文本加粗
    var lis = document.getElementById("uu").getElementsByTagName("li");  //找到所有li元素
    lis[3].style.color = "#8a2be2";   //将第四个li元素的字体颜色设置为 #8a2be2
}
</script>
<body onload="init()">
 	<ul id="uu">
 		<li id="one">标题一</li>
 		<li id="two">标题二</li>
 		<li id="three">标题三</li>
 		<li id="four">标题四</li>
    </ul>
</body>

#### · 访问关联元素

引用完成—个页面元素对象后，可以使用DOM 节点对象的 parentNode 、child Nodes 、firstChild 、lastChild 、previousSibling 或 nextS灿ng 属性访问相对于该页面元素的父、子或兄弟元素。

属性|说明
---|---
parentNode|元素节点的父节点
childNodes|元素节点的子节点数组
firstChild|第一个子节点
lastChild|最后—个子节点
previousSibling|前一个兄弟节点
nextSibiling|后一个兄弟节点

```html
示例代码：

<script type="text/javascript">
function init2(){
 	var a = document.getElementById("bdy"); //找到<body>元素
 	a = a.firstChild; //找到<ul>元素
 	a = a.childNodes[0]; //找到第一个<li>元素
 	a.style.color = "red"; //将字体颜色设为红色
}
</script>
<div id="bdy"><ul><li id="one">标题一</li><li id="two">标题二</li><li id="three">标题三</li><li id="four">标题四</li></ul></div>
<button onClick="init2()">测试！</button>
```

<script type="text/javascript">
function init2(){
 	var a = document.getElementById("bdy"); //找到<body>元素
 	a = a.firstChild; //找到<ul>元素
 	a = a.childNodes[0]; //找到第一个<li>元素
 	a.style.color = "red"; //将字体颜色设为红色
}
</script>
<div id="bdy"><ul><li id="one">标题一</li><li id="two">标题二</li><li id="three">标题三</li><li id="four">标题四</li></ul></div>
<p><button onClick="init2()">测试！</button></p>

>需要注意的是，不同浏览器在对待元素标记之间的空白字符和换行符上有区别，一般浏览器会将它们当作文本节点，而 IE6 至 IE8 浏览器则会忽略。

### 元素对象常用操作

由于 HTML DOM 将 HTML 文档表示为一棵 DOM 对象树，每个节点对象表示文档的特定部分，因此通过修改这些对象，就可以动态改变页面元素的属性。

#### 创建节点

方法|说明
---|---
createElement()|创建元素节点
createTextNode()|创建文本节点

#### 节点操作

方法|说明
---|---
appendChild()|为当前节点增加一个子节点（作为最后一个子节点）
insertBefore()|为当前节点增加一个子节点（插入指定子节点之前）
removeChild()|删除当前节点的某个子节点

#### 案例

```html
<p id="jdcz">嘿嘿嘿</p>
<script type="text/javascript">
function init3(){
	var text = document.createTextNode("I am EmptinessBoy！"); //创建一个文本节点
 	var p = document.createElement("p"); //创建一个<p>元素节点
 	p.appendChild(text); //为<p>元素追加文本节点
 	document.getElementById("jdcz").appendChild(p); //为<p>追加<p>元素
}
</script>
<button onClick="init3()">测试！</button>
```

<p id="jdcz">嘿嘿嘿</p>
<script type="text/javascript">
function init3(){
	var text = document.createTextNode("I am EmptinessBoy！"); //创建一个文本节点
 	var p = document.createElement("p"); //创建一个<p>元素节点
 	p.appendChild(text); //为<p>元素追加文本节点
 	document.getElementById("jdcz").appendChild(p); //为<p>追加<p>元素
}
</script>
<button onClick="init3()">测试！</button>
<br><br>

### 元素属性与内容操作（高频）

**元素和样式：**

属性／方法|说明
---|---
innerHTML|获取或设置元素的 HTML 内容
className|获取或设置元素的 class 屈性
style|获取或设置元素的 style 样式属性

**关于位置：**

属性／方法|说明
---|---
offsetWidth 、offsetHeight|获取或设嚣元素的宽和高（不含滚动条）
scrollWidth 、scrollHeight|获取或设置元素完整的宽和高（含滚动条）
offsetTop 、offsetLeft|获取或设嚣包含滚动条，距离上或左边滚动过的距离
scrollTop 、scrollLeft|获取或设置元素在网页中的坐标

**内容操作：**

属性／方法|说明
---|---
getAttribute()|获得元素指定属性的值
setAttribute()|为元素设驾新的属性
removeAttnbute()|为元素删除指定的属性

下面是一个简单的 Demo：

```html
<script type="text/javascript">
function init4() {
 	var test = document.getElementById("test");  //获取test元素对象
 	test.innerHTML = "<p>I am EmptinessBoy</p>";  //元素内容操作
 	test.setAttribute("style","color:red;font-weight:bold;font-size:18px;");  //设置元素的属性
 	test.className="top";
}
</script>
</head>
<button onClick="init4()">测试</button>
<div id="test" style="color:blue;">嘿嘿嘿</div>
```

<script type="text/javascript">
function init4() {
 	var test = document.getElementById("test");  //获取test元素对象
 	test.innerHTML = "<p>I am EmptinessBoy</p>";  //元素内容操作
 	test.setAttribute("style","color:red;font-weight:bold;font-size:18px;");  //设置元素的属性
 	test.className="top";
}
</script>
</head>
<button onClick="init4()">测试</button>
<div id="test" style="color:blue;">嘿嘿嘿</div>
<br>

#### 元素样式操作

在操作元素属性时， style 属性可以修改元素的样式， className 属性可以修改元素的类名，
通过这两种方法即可完成元素的样式操作。

##### className 操作元素类名

```html
使用改变 class 属性改变样式

<style type="text/css">
.textA{color:green;}
.textB{color:blue;} /*定义两组样式用于切换*/
</style>
<script type="text/javascript">
function init5() {
 	var test = document.getElementById("test1");  //获取test1元素对象
 	test.className = "textB";  //切换类名
}
</script>
<button onClick="init5()">测试</button>
<div id="test1" class="textA">I am EmptinessBoy</div>
```
<style type="text/css">
.textA{color:green;}
.textB{color:blue;} /*定义两组样式用于切换*/
</style>
<script type="text/javascript">
function init5() {
 	var test = document.getElementById("test1");  //获取test1元素对象
 	test.className = "textB";  //切换类名
}
</script>
<button onClick="init5()">测试</button>
<div id="test1" class="textA">I am EmptinessBoy</div>
<br>

##### 直接修改 style 属性

```html
直接修改 style 属性

<script type="text/javascript">
function init6() {
 	var test = document.getElementById("test2");  //获取test1元素对象
 	test.style.color = "#FFF";  //切换类名
}
</script>
<button onClick="init6()">测试</button>
<div id="test2" style="color:blue">I am EmptinessBoy</div>
```

<script type="text/javascript">
function init6() {
 	var test = document.getElementById("test2");  //获取test1元素对象
 	test.style.color = "#FFF";  //切换类名
}
</script>
<button onClick="init6()">测试</button>
<div id="test2" style="color:blue">I am EmptinessBoy</div>
<br>

## 性能优化！！

减少 DOM 访问：

> 与其他 JavaScript 相比，访问 HTML DOM 非常缓慢。

假如您期望访问某个 DOM 元素若干次，那么只访问一次，并把它作为本地变量来使用：

```javascript
var obj;
obj = document.getElementById("demo");
obj.innerHTML = "Hello";
```

缩减 DOM 规模：

> 请尽量保持 HTML DOM 中较少的元素数量。

这么做总是会提高页面加载，并加快渲染（页面显示），尤其是在较小的设备上。

每一次试图搜索 DOM（比如 getElementsByTagName）都将受益于一个较小的 DOM。