---
title: Mark Down 之简单入门
date: 2020-02-26 14:40:22
category: 学习笔记
tags: MarkDown
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/02/26/Markdown.jpg
---
Markdown 是一种轻量级的标记语言，它允许人们使用易读易写的纯文本格式编写文档，借助可实现快速排版且转换成格式丰富的HTML页面。目前被越来越多的写作爱好者及工作者使用。

Markdown 编写的文档后缀为 **.md** ，**.markdown**

<br>

## 标题

在 Markdown 中总共有6个标题，我们分别把它们称为：一级标题、二级标题、三级标题、四级标题、五级标题和六级标题。其中六级标题最小，一级标题最大。

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```
[![markdown-.md.png](https://media.everdo.cn/tank/pic-bed/2020/02/26/markdown-.md.png)](https://up.media.everdo.cn/image/nm3)

<br>

## 换行
在Markdown之中我们会发现文字无法换行，始终集中在一行之中。这时如果需要换行那么该怎么办呢？
在这里我们可以使用“换行标签”（```</br>```）。

Ps:在一些 Markdown 编辑器中，如：网易云笔记的 Markdown 编辑器中空格+换行键(Enter)，也可以实现换行功能。

```markdown
上段文字
</br>
下段文字
```

上段文字
</br>
下段文字

<br>

## 注释

注释代码如下：

```markdown
[任意字符]:对括号内容的注释，两者均不显示

如 [^_^]:哈哈哈哈哈哈
```
[任意字符]:对括号内容的注释，两者均不显示

[^_^]:哈哈哈哈哈哈

这里干干净净什么都没有

<br>

## 引用

在我们想要引用一句话的时候，我们在 Markdown 中使用如下代码：

```markdown
代码格式：

>引用的内容
```

>引用话语：人类的本质是复读机

<br>

## 分隔线

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

```markdown
---
```

---

<br>

## 文字样式

在 Markdown 中有：斜体、加粗、高亮、划线。这些文字样式供我们选择，代码如下：

```markdwon
*斜体*

**加粗**

***粗斜体文本***

==高亮==

<u>下划线</u>

~~删除线~~
```
*斜体*

**加粗**

***粗斜体文本***

==高亮==

<u>下划线</u>

~~删除线~~

但如果我们想修改文字 大小 / 颜色 / 字体，就要用 font 标签，( Ps：center和font都是html的标签，在markdown也能用 )

```html
<font color=#2196F3 size=2 face="微软雅黑">微软雅黑大小为2的字</font>
```

color代表字体颜色（要用16进制颜色值），size代表文字大小，face代表字体

<font color=#2196F3 size=2 face="微软雅黑">微软雅黑大小为2的字</font>


实现“文字居中”就要center标签，代码如下：

```html
<center>居中</center>
```
<center>居中</center>

## 链接以及图片
在 Markdown 中添加链接和图片有异曲同工之妙，所以我们放在一起来讲，代码如下：

```markdwon
代码格式链接：[显示名称](链接)

[这里是链接](https://coding.emptinessboy.com/)

代码格式图片：![名称](图片链接)

![这样是图片](https://coding.emptinessboy.com/img/logo.png)
```

[这里是链接](https://coding.emptinessboy.com/)
![这样是图片](https://coding.emptinessboy.com/img/logo.png)

## 代码高亮

在Markdown中如果我们想要高亮一段代码，可以使用如下代码：

```markdown
  ```key
    代码 (把key换成代码类型)
    ```
 ```

语言|对应的 key
---|---
1C|1c
ActionScript|actionscript
Apache|apache
AppleScript|applescript
AsciiDoc|asciidoc
AspectJ|asciidoc
AutoHotkey|autohotkey
AVR Assembler|avrasm
Axapta|axapta
Bash|bash
BrainFuck|brainfuck
Cap’n Proto|capnproto
Clojure REPL|clojure
Clojure|clojure
CMake|cmake
CoffeeScript|coffeescript
C++|cpp
C#|cs
CSS|css
D|d
Dart|d
Delphi|delphi
Diff|diff
Django|django
DOS.bat|dos
Dust|dust
Elixir|elixir
ERB(Embedded Ruby)|erb
Erlang REPL|erlang-repl
Erlang|erlang
FIX|fix
F#|fsharp
G-code(ISO 6983)|gcode
Gherkin|gherkin
GLSL|glsl
Go|go
Gradle|gradle
Groovy|groovy
Haml|haml
Handlebars|handlebars
Haskell|haskell
Haxe|haxe
HTML|html
HTTP|http
Ini file|ini
Java|java
JavaScript|javascript
JSON|json
Lasso|lasso
Less|less
Lisp|lisp
LiveCode|livecodeserver
LiveScript|livescript
Lua|lua
Makefile|makefile
Markdown|markdown
Mathematica|mathematica
Matlab|matlab
MEL (Maya Embedded Language)|mel
Mercury|mercury
Mizar|mizar
Monkey|monkey
Nginx|nginx
Nimrod|nimrod
Nix|nix
NSIS|nsis
Objective C|objectivec
OCaml|ocaml
Oxygene|oxygene
Parser 3|parser3
Perl|perl
PHP|php
PowerShell|powershell
Processing|processing
Python’s profiler output|profile
Protocol Buffers|protobuf
Puppet|puppet
Python|python
Q|q
R|r
RenderMan RIB|rib
Roboconf|roboconf
RenderMan RSL|rsl
Ruby|ruby
Oracle Rules Language|ruleslanguage
Rust|rust
Scala|scala
Scheme|scheme
Scilab|scilab
SCSS|scss
Smali|smali
SmallTalk|smalltalk
SML|sml
SQL|sql
Stata|stata
STEP Part21(ISO 10303-21)|step21
Stylus|stylus
Swift|swift
Tcl|tcl
Tex|tex
text|text/plain
Thrift|thrift
Twig|twig
TypeScript|typescript
Vala|vala
VB.NET|vbnet
VBScript in HTML|vbscript-html
VBScript|vbscript
Verilog|verilog
VHDL|vhdl
Vim Script|vim
Intel x86 Assembly|x86asm
XL|xl
XML|xml
YAML|yml

<br>

## 无序列表

在 Markdown 中我们可以绘制列表，代码格式如下：

```markdown
- 列表1
  - 列表1.1
  - 列表1.2
```

- 列表1
    - 列表1.1
    - 列表1.2

## 有序列表

在 Markdown 中我们可以绘制列表，代码格式如下：

```markdown
1. 列表1
  - 列表1.1
  - 列表1.2
```

1. 列表1
    - 列表1.1
    - 列表1.2
2. 列表2
    - 列表2.1
    - 列表2.2

<br>

## 代办事项

在 Markdown 中你可以输入你最近的代办事项，代码格式如下：

```markdown
- [ ] 未完成事项
- [x] 已完成事项
```

- [ ] 未完成事项
- [x] 已完成事项

Ps：带x的代表已经完成的事项，空格的为还没有完成的事项

<br>

## 表格
在 Markdown 中我们同样可以绘制表格，代码格式如下 (Ps：第二行中 ---|---|--- 是有几个大标题就写几个。如果是两个就是 ---|--- ，四个就是 ---|---|---|--- )：

```markdown
大标题1|大标题2|大标题3
---|---|---
内容1|内容2|内容3
内容1|内容2|内容3
```

大标题1|大标题2|大标题3
---|---|---
内容1|内容2|内容3
内容1|内容2|内容3

<br>

## 脚注

```markdown
在文章中引入[^1]内容

[^1]:脚注说明文字
```

文字内容 [^md]

[^md]: md是markdown文件的后缀名


<br>

## 其他补充

Markdown中的转义字符为\，若不想使符号变成文字的格式等，在符号前加\。

<br>

**至此以上列举的 Markdown 就已经足够我们在日常写作中使用了。还有更多高级操作，例如使用 Markdown 渲染流程图，甘特图等等因为需要引入插件，并不完美兼容所有平台，故暂时不做学习了。本文整理自网络**