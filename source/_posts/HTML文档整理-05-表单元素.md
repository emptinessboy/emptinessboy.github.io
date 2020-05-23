---
title: HTML文档整理 05-表单元素
date: 2020-03-14 17:13:01
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

在网页中，表单主要是用于负责采集浏览者的相关数据，如常见的注册表、调查表和留言表等。在HTML5中，表单拥有多个新的表单输入类型，这些新特性提供了更好的输入控制和验证。

## 表单概述

表单主要用于收集网页上浏览者的相关信息，其标记为<form></form>。表单的基本语法格式如下：
<!--more-->

```html
<form action="url" mothod="get|post" enctype="mime"></form>
```

其中，action 指定处理提交表单的格式，它可以是一个 URL 地址或一个电子邮件地址；method 指明提交表单的 HTTP 方法。enctype 指明用来把表单提交给服务器时的互联网媒体形式。表单是一个能够包含表单元素的区域，通过添加不同的表单元素，将显示不同的效果

下面是一个基本表单的实例：

```html
<form>
    用户名称
    <input type="text" name="user" /><br />
    用户密码
    <input type="password" name="user" /><br />
    <input type="submit" value="登录">
</form>
```

<p>
<form>
    用户名称
    <input type="text" name="user" /><br />
    用户密码
    <input type="password" name="user" /><br />
    <input type="submit" value="登录">
</form>
</p>

### required 必填项

required 属性规定必须在提交之前填写输入域（不能为空）。required 属性适用于以下类型的输入属性：text、search、url、email、password、date、pickers、number、checkbox、radio 等。

```html
required="required"
```

### ```<input>``` 相关属性

由于 ```<input />``` 在 HTML 表单操作中是一个非常基本的操作，这里先将该标签的属性做成列表来方便下面查找

属性值|描述
---|---
button|定义可点击按钮（多数情况下，用于通过 JavaScript 启动脚本）。
checkbox|定义复选框。
file|定义输入字段和 "浏览"按钮，供文件上传。
hidden|定义隐藏的输入字段。
image|定义图像形式的提交按钮。
password|定义密码字段。该字段中的字符被掩码。
radio|定义单选按钮。
reset|定义重置按钮。重置按钮会清除表单中的所有数据。
submit|定义提交按钮。提交按钮会把表单数据发送到服务器。
text|定义单行的输入字段，用户可在其中输入文本。默认宽度为 20 个字符。

## 使用表单基本元素

表单元素是能够让用户在表单中输入信息的元素，常见的有文本框、密码框、下拉菜单、单选按钮、复选框等。

### 单行文本输入框 ```text```

文本框是一种让访问者自行输入内容的表单对象，通常被用来填写单个字或简短的回答，如用户姓名和地址。代码格式如下：

```html
<form>
    自定义文字：
    <input type="text" name="user" size="30" maxlength="25" value="i@my.huxiaofan.com"/>
    <!--textarea 标签内的内容可以直接用于编辑，和 placeholder 属性不同-->
</form>
```
<form>
    自定义文字：
    <input type="text" name="user" size="30" maxlength="25" value="i@my.huxiaofan.com"/>
</form>

> 其中，type="text" 定义单行文本输入框；name 属性定义文本框的名称，要保证数据的准确采集，必须定义一个独一无二的名称；size 属性定义文本框的宽度，单位是单个字符宽度；maxlength 属性定义最多输入的字符数；value 属性定义文本框的初始值。

### 密码域 password

密码输入框是一种特殊的文本域，主要用于输入一些保密信息。当网页浏览者输入文本时，显示的是黑点或其他符号，这样就增加了输入文本的安全性。

```html
<form>
    请输入密码：
    <input type="password" name="user" size="30" maxlength="25" />
</form>
```

<p>
<form>
    请输入密码：
    <input type="password" name="user" size="30" maxlength="25" />
</form>
</p>

### 多行文本框标记 ```<textarea>```

其中，name 属性定义多行文本框的名称，要保证数据的准确采集，必须定义一个独一无二的名称；cols 属性定义多行文本框的宽度，单位是单个字符宽度；rows 属性定义多行文本框的高度，单位是单个字符高度；wrap 属性定义输入内容大于文本域时显示的方式。

```html
<textarea name="cantent" cols="50" row="5" warp="true" placeholder="请输入..."></textarea>
```

<textarea name="cantent" cols="50" row="5" warp="true" placeholder="请输入..."></textarea>

```html
<form action="/404.php" id="usrform">
    用户名: 
    <input type="text" name="usrname" value="Emptinessboy">
    <input type="submit">
</form>

<textarea name="comment" form="usrform">本宝宝最帅！</textarea>
<!--textarea 标签内的内容可以直接用于编辑，和 placeholder 属性不同-->
```

<form action="/404.php" id="usrform">
    用户名: 
    <input type="text" name="usrname" value="Emptinessboy">
    <input type="submit">
</form>

<textarea name="comment" form="usrform">本宝宝最帅！</textarea>

一般情况下，textarea 是嵌套在 form 标签里的。当 textarea 在表单外时，基于 id 的绑定就为 HTML 布局提供了更多的可能和灵活性。这里演示代码的 textarea 绑定了 formid 为 usrform 的表单，因此点击表单的提交窗口会同时把 textarea 的值提交上去！

[![html-textarea.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html-textarea.jpg)](https://up.media.everdo.cn/image/HVei)

下面整理了一些 textarea 常用的属性和方法：

属性|值|描述
---|---|---
name|name_of_textarea|规定文本区的名称。
cols|number|规定文本区内的可见宽度。
rows|number|规定文本区内的可见行数。
autofocus|autofocus|规定在页面加载后文本区域自动获得焦点。
disabled|disabled|规定禁用该文本区的编辑功能。且显示灰色
form|form_id|规定文本区域所属的一个或多个表单。可以用于关联提交按钮。
maxlength|number|规定文本区域的最大字符数，超出后不能输入。
placeholder|text|规定描述文本区域预期值的简短提示。
readonly|readonly|规定文本区为只读。
required|required|规定文本区域是必填的。
wrap|hard / soft|当提交表单时，wrap="hard" 的文本区域中的文本会包含换行符

### 单选按钮 radio

单选按钮主要是让网页浏览者在一组选项里只能选其一。

```html
<form>
    请选择选项：
    <input type="radio" name="answer" value="A" />选项A 
    <input type="radio" name="answer" value="B" />选项B 
    <input type="radio" name="answer" value="C" />选项C 
    <input type="radio" name="answer" value="D" />选项D 
</form>
```

<p>
<form>
    请选择选项：
    <input type="radio" name="answer" value="A" />选项A 
    <input type="radio" name="answer" value="B" />选项B 
    <input type="radio" name="answer" value="C" />选项C 
    <input type="radio" name="answer" value="D" />选项D 
</form>
</p>

### 复选框 checkbox

复选框主要是让网页浏览者在一组选项里可以同时选择多个选项。每个复选框都是一个独立的元素，必须有一个唯一的名称。

其中，type="checkbox" 定义复选框；name 属性定义复选框的名称，**在同一组中的复选框都必须用同一个名称**；value 属性定义复选框的值。

```html
<form>
    多项选择：
    <input type="radio" name="answer" value="A" checked />选项A 
    <input type="radio" name="answer" value="B" />选项B 
    <input type="radio" name="answer" value="C" />选项C 
    <input type="radio" name="answer" value="D" />选项D 
</form>
```
<form>
    多项选择：
    <input type="checkbox" name="answer" value="A" checked />选项A 
    <input type="checkbox" name="answer" value="B" />选项B 
    <input type="checkbox" name="answer" value="C" />选项C 
    <input type="checkbox" name="answer" value="D" />选项D 
</form>

> 技巧提示：checked属性主要用来设置默认选中项,本案例中选项 A 默认被选中

### 选择列表标记 ```<select>```

下拉列表主要用于在有限的空间里设置多个选项，它既可以用作单选，也可以用作多选。

其中，name 属性定义选择列表的名称；size 属性定义选择列表的行数；multiple 属性表示可以多选，如果不设置该属性，则只能单选；value 属性定义选择项的值；selected 属性表示默认已经选择本选项。

单项选择列表

```html
<form>
<select name="answer">
    <option value="A" selected>选项A</option>
    <option value="B">选项B</option>
    <option value="D">选项C</option>
    <option value="D">选项D</option>
</select>
<form>
```

<form>
<select name="answer">
    <option value="A" selected>选项A</option>
    <option value="B">选项B</option>
    <option value="D">选项C</option>
    <option value="D">选项D</option>
</select>
<form>

多项选择列表

```html
<form>
<select name="answer" size="2" multiple>
    <option value="A" selected>选项A</option>
    <option value="B">选项B</option>
    <option value="D">选项C</option>
    <option value="D">选项D</option>
</select>
<form>
```

<form>
<select name="answer" size="2" multiple>
    <option value="A" selected>选项A</option>
    <option value="B">选项B</option>
    <option value="D">选项C</option>
    <option value="D">选项D</option>
</select>
<form>

列表内显示了4个选项，用户可以按住 Ctrl 键选择多个选项。

### 普通按钮 button

```<input type="button" />``` 定义可点击的按钮，但没有任何行为。button 类型常用于在用户点击按钮时启动 JavaScript 程序。代码格式如下：

```html
<form>
    <input type="button" name="try" value="尝试" onclick="" />
</form>
```

<form>
    <input type="button" name="try" value="尝试" onclick="" />
</form>

下面是一个进阶示例，使用 javascript 将文本框1的内容复制到文本框2中：(由于是文本中嵌入 js 代码，可能会被浏览器或 IDE 安全策略拦截)

```html
<form>
    <p>
        <input type="text" id="field_1" value="吼吼吼吼">
        <br>
        <input type="text" id="filed_2" value="嘎嘎嘎嘎">
        <br>
    </p>
    <input type="button" name="copy" value="点我试试" onclick="document.getElementById('filed_2').value=document.getElementById('field_1').value" >
</form>
```

<p>
<form>
    <p>
        <input type="text" id="field_1" value="吼吼吼吼">
        <br>
        <input type="text" id="filed_2" value="嘎嘎嘎嘎">
        <br>
    </p>
    <input type="button" name="copy" value="点我试试" onclick="document.getElementById('filed_2').value=document.getElementById('field_1').value" >
</form>
</p>

### 提交按钮 submit

```<input type="submit" />``` 定义提交按钮。提交按钮用于向服务器发送表单数据。数据会发送到表单的 action 属性中指定的页面。

```html
GET 方式发送请求，若需要 POST 则修改 form.method
<form action="/404.php" method="get">
  <p>邮箱: <input type="text" name="email" placeholder="请输入邮箱地址..."/></p>
  <p>昵称: <input type="text" name="nickname" maxlength="18" placeholder="想一个昵称吧"/></p>
  <input type="submit" value="提交" />
</form>
```

<form action="/404.php" method="get">
  <p>邮箱: <input type="text" name="email" placeholder="请输入邮箱地址..."/></p>
  <p>昵称: <input type="text" name="nickname" maxlength="18" placeholder="想一个昵称吧"/></p>
  <input type="submit" value="提交" />
</form>

单击确认按钮，输入会发送到服务器上名为 "404.php" 的页面。:-D 当然本服务器上这个 php 是不存在的

这里，我们研究下 GET 方式和 POST 方式在浏览器执行过程中的区别。

[![html-submitget.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html-submitget.jpg)](https://up.media.everdo.cn/image/HYM4)

> 可以很明显看到，上图中 GET 方式为从服务器拉取数据，但是通过改变 URL 使得通过 URL 进行参数传递。而下图 POST 方式，则是与之不同。

[![html-submitpost.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/14/html-submitpost.jpg)](https://up.media.everdo.cn/image/HbaM)

###  重置按钮 reset

```<input type="reset" />``` 定义重置按钮。重置按钮会清除表单中的所有数据。代码格式如下：

```html
<form>
  <p>随便瞎写: <input type="text" name="text" value=""/></p>
  <input type="reset" name="" value="一键清除"/>
</form>
```

<form>
  <p>随便瞎写: <input type="text" name="text" value=""/></p>
  <input type="reset" name="" value="一键清除"/>
</form>

## 表单高级元素的使用

除了上述基本属性外，HTML5中还有一些高级属性，包括url、eamil、time、range、search等。对于部分高级属性。其中有些效果IE 浏览器暂时还不支持

### url 属性

url属性用于说明网站网址，显示为在一个文本框中输入URL地址，在提交表单时会自动验证url的值。

用户可以使用 max 属性设置其最大值、min 属性设置其最小值、step 属性设置合法的数字间隔、value 属性规定其默认值。

可以在文本框中输入相应的网址。如果输入的 url 格式不准确，按Enter键后就会弹出报错信息。

```html
<form>
  <p>请输入网址: <input type="url" name="wangzhi" value=""/></p>
  <input type="submit" name="" value="GO"/>
</form>
```

<p>
<form>
  <p>请输入网址: <input type="url" name="wangzhi" value=""/></p>
  <input type="submit" name="" value="GO"/>
</form>
</p>

> 增强用户体验：iPhone 的 Safari 浏览器会识别 url 输入类型，然后改变触摸屏的键盘来适应它（添加 .com 选项）。

### Email 属性

与url属性类似，email 属性用于让浏览者输入 E-mail 地址，在提交表单时会自动验证 email 域的值

```html
<form>
  <p>请输入邮箱: <input type="email" name="email" value=""/></p>
  <input type="submit" name="" value="GO"/>
</form>
```

<p>
<form>
  <p>请输入邮箱: <input type="email" name="email" value=""/></p>
  <input type="submit" name="" value="GO"/>
</form>
</p>

### Tel 和 Search 属性

tel 输入类型用于应该包含电话号码的输入字段。但现阶段浏览器并不支持对 Tel 属性进行校验，使用这个属性视同于使用普通文本提交属性。

search 输入类型用于搜索字段，比如站内搜索或谷歌搜索等。搜索字段的外观与常规的文本字段无异。

>也就是说这两个属性实际使用简单根据需要应用就行，可能在某些客户端可以触发增强的交互，反正也没太大用 （dog

### number 属性

number 输入类型用于包含数字值的输入字段。可以对 number 设置可接受数字的限制。

- max 规定允许的最大值。
- min 规定允许的最小值。
- step 规定合法数字间隔（如果 step="3"，则合法的数字是 -3,0,3,6, 以此类推）
- value 规定默认值。

```html
<form>
    <input type="number" name="points" min="1" max="10" value="5" />
</form>
```
<p>
<form>
    <input type="number" name="points" min="1" max="10" value="5" />
</form>
</p>

### Range 属性

range属性可以显示一个滚动的控件，用户可以使用max、min和step属性设置控件的范围。代码格式如下：（其中高级属性和上面的 number 相同）

```html
<form>
    拖动滑块: 
    <input type="range" name="points" min="1" max="10" />
</form>
```

<p>
<form>
    拖动滑块: 
    <input type="range" name="points" min="1" max="10" />
</form>
</p>

> 默认情况下，滑块位于滚珠的中间位置。如果用户指定的最大值小于最小值，则允许使用反向滚动轴，目前浏览器对这一属性还不能很好地支持。

### Date 和 Times

HTML5 拥有多个供选择日期和时间的新的输入类型：(IE 不支持)

- date - 选择日、月、年
- month - 选择月、年
- week - 选择周、年
- time - 选择时间（时、分）
- datetime - 选择时间、日期、月、年（UTC 时间）貌似 Chrome 不行
- datetime-local - 选择时间、日期、月、年（本地时间）

下面的例子允许您从日历选取一个日期：

```html
<form>
    <input type="date" name="user_date" />
    <input type="month" name="user_date" />
    <input type="week" name="user_date" />
    <input type="time" name="user_date" />
    <input type="datetime" name="user_date" />
    <input type="datetime-local" name="user_date" />
</form>
```

<p>
<form>
<input type="date" name="user_date" />&ensp;
<input type="month" name="user_date" />&ensp;
<input type="week" name="user_date" />&ensp;
<input type="time" name="user_date" />&ensp;
<input type="datetime" name="user_date" />&ensp;
<input type="datetime-local" name="user_date" />
</form>
</p>

### color 属性

color 输入类型用于规定颜色。该输入类型允许你从拾色器中选取颜色：

```html
<form action="/example/html5/demo_form.asp" method="get">
    选择颜色: 
    <input type="color" name="user_color" /><br />
    <input type="submit" />
</form>
```
<p>
<form action="/example/html5/demo_form.asp" method="get">
    选择颜色: 
    <input type="color" name="user_color" /><br />
    <input type="submit" />
</form>
</p>

### file 属性

file 输入类型用于文件上传。

```html
<form action="404.php" method="get">
    请选择图片：
    <input type="file" name="img" />
    <input type="submit" />
</form>
```

<p>
<form action="404.php" method="get">
    请选择图片：
    <input type="file" name="img" />
    <input type="submit" />
</form>
</p>

### 图形化按钮 image

image 输入类型将提交按钮显示为一个自定义图像。

对于 ```<input type="image">```，src 和 alt 属性是必需的。

```html
<form>
    姓名: 
    <input type="text" name="name" placeholder="输入名字" /><br />
    <input type="image" src="https://media.everdo.cn/tank/pic-bed/2020/03/15/eg_submit.th.jpg" alt="Submit" width="28" height="28"/>
</form>
```

<p>
<form>
    姓名: 
    <input type="text" name="name" placeholder="输入名字" /><br />
    <input type="image" src="https://media.everdo.cn/tank/pic-bed/2020/03/15/eg_submit.th.jpg" alt="Submit" width="28" height="28"/>
</form>
</p>

## Tips：关于表单默认值

hidden 输入类型定义隐藏字段。隐藏字段对于用户是不可见的。隐藏字段常常存储默认值，或者由 JavaScript 改变它们的值。

```html
<form action="/404.php" method="get">
  <input type="text" name="text" /><br />
  <input type="hidden" name="shuaige" value="Emptinessboy" />
  <input type="submit" value="提交" />
</form>
```
<form action="/404.php" method="get">
  <input type="text" name="text" /><br />
  <input type="hidden" name="shuaige" value="Emptinessboy" />
  <input type="submit" value="提交" />
</form>

在这个案例中，一旦点击提交按钮，就会把 shuaige 值 Emptinessboy 给上传到服务器！就像下图那样：

[![html-texthidden.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/15/html-texthidden.jpg)](https://up.media.everdo.cn/image/HeAY)

写文档好累啊！