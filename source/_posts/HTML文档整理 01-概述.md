---
title: HTML文档整理 01-概述
date: 2020-03-13 13:42:33
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

## 概述部分

HTML 是2014年10月发布的W3C推荐标准，是一种标记性语言

### 文档说明

HTML5对文档类型进行了简化，简单到15个字符就可以了，代码如下：

```html
<!DOCTYPE html>
```

技巧提示：Doctype申明需要出现在HTML文件的第一行。

<!--more-->

### HTML标记

HTML标记代表文档的开始，由于HTML语言语法的松散特性，该标记可以省略，但是为了使之符合Web标准和文档的完整性，用户要养成良好的编写习惯，建议不要省略该标记。

```html
<html> ... </html>
```

### 头标记

头标记head用于说明文档头部相关信息，一般包括标题信息、元信息、定义CSS样式和脚本代码等。HTML的头部信息是以<head>开始，以</head>结束，语法格式如下：

```html
<head> … </head>
```
#### 标题

标题一般是用来说明页面的用途的，它显示在浏览器的标题栏中

```html
<title> … </title>
```
#### Meta

<meta> 标记可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词

[![html-meta.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/13/html-meta.jpg)](https://up.media.everdo.cn/image/t7G)

##### （1）字符集charset属性

```html
<meta charset="UTF-8">
```

##### （2）搜索引擎的关键字优化
```html
<meta name="keywords" content="关键字,keywords" />
```
		
不同的关键字之间应用 **半角逗号隔开（英文输入状态下）**，不要使用 “空格” 或 “|” 间隔；是 **keywords，不是keyword**；关键字标签中的内容应该是一个个的短语，而不是一段话。
			
关键字标记中的内容要与网页核心内容相关，确信使用的关键词出现在网页文本中。使用用户易于通过搜索引擎检索的关键字，过于生僻的词汇不太适合做meta标记中的关键字。不要重复使用关键字，否则可能会被搜索引擎惩罚。一个网页的关键字标记里最多包含3~5个最重要的关键字，不要超过5个。每个网页的关键字应该不一样。

*目前它在搜索引擎排名中的作用很小。*

##### （3）页面描述meta description

描述元标记是一种HTML元标记，用来简略描述网页的主要内容，通常被搜索引擎用于搜索结果页上展示给最终用户看的一段文字片段。

```html	
<meta name="description" content="网页的介绍" />
```

##### （4）页面定时跳转

使用 ```<meta>``` 标记可以使网页在经过一定时间后自动刷新，可以通过将http-equiv属性值设置为refresh来实现。content属性值可以设置为更新时间。

```html
<meta http-equiv="refresh" content="秒;[url=网址]" />
```

例如，实现每5秒刷新一次页面，将下述代码放入head标记部分即可。

```html			
<meta http-equiv="refresh" content="5" />
```

## 网页的主体标记 body

网页所要显示的内容都放在网页的主体标记内，它是HTML文件的重点所在，后面章节所要介绍的HTML标记都将放在这个标记内。然而它并不仅仅是一个形式上的标记，它本身也可以控制网页的背景颜色或背景图像，这会在后面进行介绍。主体标记是以 ```<body>``` 开始，以 ```</body>``` 结束，

> 注意，在构建HTML结构时，标记不允许交错出现，否则会造成错误。

## 页面注释标记

```html
<!-- 被注释内容 -->
```

## 一些变化
	
- 标签不再区分大小写
- 在HTML5中，属性值不放在引号中也是正确的
  
	- ```<input checked="a" type="checkbox"/>``` 与 ```<input checked=a type=checkbox/>``` 相同
	- 仍然建议读者加上引号
  
- 允许部分属性值的属性省略
  
	- ```<input checked type="checkbox"/> <input readonly type="text"/>```
	- 其中``checked="checked"``省略为checked，而``readonly="readonly"``省略为readonly。

<br>
HTML5中的标记分为单标记和双标记。所谓单标记是指没有结束标记的标记，双标记是指既有开始标记又包含结束标记。  例如```<br />```

HTML5中不允许写结束标记的 **单标记** 元素有

```html
<area/>  <base/>  <br/>  <col/>  <command/>  <embed/>  <hr/>  <img/>  <input/>  <keygen/>  <link/>  <meta/>  <param/>  <source/>  <track/>  <wbr/>
```

HTML5中允许省略结束标记的 **双标记** 元素有

```html
<li>  <dt>  <dd>  <p>  <rt>  <rp>  <optgroup>  <option>  <colgroup>  <thead>  <tbody>  <tfoot>  <tr>  <td>  <th>
```

## Html快速构建新的模板

```html
<!-- author: @emptinessboy huxiaofan.com -->
<!DOCTYPE html>
<html>
	<head>
	
		<meta name="keywords" content="关键字,keywords" />
		<meta name="description" content="网页的介绍" />
	
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		
	</body>
</html>
```
## 在线代码校验

HTML5语法的新变化为了兼容各个不统一的页面代码，HTML5的设计在语法方面做了以下变化

在线校验 [http://validator.w3.org/](http://validator.w3.org/)