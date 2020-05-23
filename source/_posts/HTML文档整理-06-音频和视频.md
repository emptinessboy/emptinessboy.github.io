---
title: HTML文档整理 06-音频和视频
date: 2020-03-15 02:00:17
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

目前，在网页上没有关于音频和视频的标准，多数音频和视频都是通过插件来播放的，为此，HTML5新增了音频和视频的标记。

## ```<audio>``` 标记

与 HTML4 相比，HTML5 新增了 ```<audio>``` 标记，规定了一种包含音频的标准方法。

### audio 概述

```<audio>``` 标记主要是定义播放声音文件或音频流的标准。支持3种音频格式，分别为ogg、mp3和wav。如果需要在HTML5网页中播放音频，则输入的基本格式如下：

> 翻车警告！！下方音频为本人蜜汁鬼畜录音，谨慎播放！！由于播放下方音频导致的，双耳失聪，精神失常等等后果与本站无关！！

```html
<audio src="https://media.everdo.cn/tank/xiaofan/audio/2019/ksong_moumou.mp3" controls="controls">您的浏览器不支持新型播放控件</audio>
```

<audio src="https://media.everdo.cn/tank/xiaofan/audio/2019/ksong_moumou.mp3" controls="controls">您的浏览器不支持新型播放控件</audio>

其中src属性是规定要播放的音频地址，controls属性是提供添加播放、暂停和音量的控件。在 ```<audio>``` 与 ```</audio>``` 之间插入的内容是供不支持 audio 元素的浏览器显示的。

### audio 标记的属性

```<audio>``` 标记的常见属性和含义如下表所示。

属性|值|描述
---|---|---
src|url|要播放的音频的 URL。
controls|controls|如果出现该属性，则向用户显示控件，比如播放按钮。
preload|preload	|如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。
autoplay|autoplay|如果出现该属性，则音频在就绪后马上播放。
loop|loop|如果出现该属性，则每当音频结束时重新开始播放。
muted|muted|规定视频输出应该被静音。

另外，```<audio>```标记可以通过source属性添加多个音频文件。具体格式如下：

```html
<audio controls="controls">
    <source src="song.ogg" type="audio/ogg" />
    <source src="song.mp3" type="audio/mpeg" />
    您的浏览器不支持新型播放控件
</audio>
```

### 音频解码器

现代浏览器对音频的兼容问题已经很少遇见

## ```<video>``` 标记

```<video>``` 是一种统一的包含视频的标准方法。与 HTML4 相比，HTML5 新增了 ```<video>``` 标记。

### video 概述

video 标记主要是定义播放视频文件或视频流的标准。支持3种视频格式，分别为 Ogg、WebM 和 MPEG4。

如果需要在 HTML5 网页中播放视频，输入的基本格式如下：

> 翻车警告！！下方视频为本人不知道咋剪出来的旅行短片，谨慎播放！！由于播放下方视频导致的，双耳失聪，精神失常等等后果与本站无关！！ 

视频博客链接： [Blog](https://huxiaofan.com/travel/vlog-zhoushan/) / 视频B站链接： [av57628004](https://huxiaofan.com/go/?url=https://www.bilibili.com/video/av57628004)

```html
<video src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" controls="controls">您的浏览器不支持新型播放控件</video>
```

<video src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" width="100%" controls="controls">您的浏览器不支持新型播放控件</video>

另外，在 ```<video>``` 与 ```</video>``` 之间插入的内容是供不支持video元素的浏览器显示的。

### video 标记的属性

```<video>``` 标记的常见属性和含义如下表所示：

属性|值|描述
---|---|---
src|url|要播放的视频的 URL。
poster|URL|规定视频下载时显示的图像，或者在用户点击播放按钮前显示的图像。
controls|controls|如果出现该属性，则向用户显示控件，比如播放按钮。
preload|preload|如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。
autoplay|autoplay|如果出现该属性，则视频在就绪后马上播放。
width|pixels|设置视频播放器的宽度。
height|pixels|设置视频播放器的高度。
loop|loop|如果出现该属性，则当媒介文件完成播放后再次开始播放。
muted|muted|规定视频的音频输出应该被静音。

由上表可知，用户可以自定义视频文件显示的大小。例如，如果想让视频以320×240像素大小显示，就可以加入width和height属性。具体格式如下：[插图]

```html
<video width="300" height="200" src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" controls="controls">您的浏览器不支持新型播放控件</video>
```

<video width="300" height="200" src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" controls="controls">您的浏览器不支持新型播放控件</video>

另外，```<video>``` 标记可以通过 source 属性添加多个视频文件，具体格式如下：

```html
<video controls="controls">
    <source src="h264.mp4" type="video/mpeg" />
    <source src="h264.ogg" type="video/ogg" />
    您的浏览器不支持新型播放控件
</video>
```

### 视频解码器

目前，在 HTML5 中，使用比较多的视频解码文件是 Theora、H.264 和 VP8。（截止文章截稿前 H.265 还不能被 chrome 浏览器支持，但已经可以被微软 Chromium 内核的新版 edge 浏览器所支持！！！ 老款 edge 并不支持）

> 这里提供一个 H.265 视频测试链接，可以看到如下图 chrome 是只有声音没有画面的
> https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h265.mp4

[![html-h265.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/15/html-h265.jpg)](https://up.media.everdo.cn/image/HrZs)

## 音频和视频中的属性

在HTML5网页中，关于音频和视频的属性非常多，本节收录几个常用的属性。

### autoplay 属性
 
autoplay 控制音频或视频是否在加载后立即开始播放。 其中，autoplay属性的取值包括true和false。设置 autoplay 属性的语法格式如下：

```
audio|video.autoplay=true|false
```
 
返回autoplay属性的语法格式如下：

```
audio|video.autoplay
```

下面是一个具体使用的例子,单击【启动自动播放】按钮，然后单击【检查自动播放状态】按钮，即可看到此时 autoplay 属性为 true。:

```html
<button onclick="enableAutoplay()" type="button">启动自动播放</button>
<button onclick="disableAutoplay()" type="button">禁用自动播放</button>
<button onclick="checkAutoplay()" type="button">检查自动播放状态</button>

<video id="video1" controls="controls">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video标签。
</video>

<script>
myVid=document.getElementById("video1");
function enableAutoplay()
{ 
  myVid.autoplay=true;
  myVid.load();
} 
function disableAutoplay()
{ 
  myVid.autoplay=false;
  myVid.load();
} 
function checkAutoplay()
{ 
  alert(myVid.autoplay);
} 
</script> 
```

<button onclick="enableAutoplay()" type="button">启动自动播放</button>
<button onclick="disableAutoplay()" type="button">禁用自动播放</button>
<button onclick="checkAutoplay()" type="button">检查自动播放状态</button>

<video id="video1" width="100%" controls="controls">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video标签。
</video>

<script>
myVidone=document.getElementById("video1");
function enableAutoplay()
{ 
  myVidone.autoplay=true;
  myVidone.load();
} 
function disableAutoplay()
{ 
  myVidone.autoplay=false;
  myVidone.load();
} 
function checkAutoplay()
{ 
  alert(myVidone.autoplay);
} 
</script> 

### controls 属性

controls 属性设置或返回浏览器应当显示标准的音频或视频控件。

标准的音频或视频控件包括播放、暂停、进度条、音量、全屏切换、字幕和轨道。

设置controls属性的语法格式如下：

```
audio|video.controls=true|false
```

返回controls属性的语法格式如下：

```
audio|video.controls
```

下面是一个具体使用的例子,单击【启动控件】按钮，然后单击【检查控件状态】按钮，即可看到此时 controls 属性为 true。:

```html
<button onclick="enableControls()" type="button">启动控件</button>
<button onclick="disableControls()" type="button">禁用控件</button>
<button onclick="checkControls()" type="button">检查控件状态</button>

<video id="video2">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video 标签。
</video>

<script>
myVid=document.getElementById("video2");
function enableControls()
{ 
  myVid.controls=true;
  myVid.load();
} 
function disableControls()
{ 
  myVid.controls=false;
  myVid.load();
} 
function checkControls()
{ 
  alert(myVid.controls);
} 
</script> 
```

<button onclick="enableControls()" type="button">启动控件</button>
<button onclick="disableControls()" type="button">禁用控件</button>
<button onclick="checkControls()" type="button">检查控件状态</button>

<video id="video2" width="100%">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video 标签。
</video>

<script>
myVidtwo=document.getElementById("video2");
function enableControls()
{ 
  myVidtwo.controls=true;
  myVidtwo.load();
} 
function disableControls()
{ 
  myVidtwo.controls=false;
  myVidtwo.load();
} 
function checkControls()
{ 
  alert(myVidtwo.controls);
} 
</script>

## (高级) 音频和视频中的方法

在 HTML5 网页中，操作音频或视频文件的常用方法包括 canPlayType()方法、load()方法、play()方法 和 pause()方法。

### canPlayType() 方法

canPlayType() 方法用于检测浏览器是否能播放指定的音频或视频类型。

canPlayType() 方法返回值包含如下：

- probably：浏览器全面支持指定的音频或视频类型。
- maybe：浏览器可能支持指定的音频或视频类型。
- " "（空字符串）：浏览器不支持指定的音频或视频类型。

注意，目前所有主流浏览器都支持 canPlayType() 方法。InternetExplorer 8 及之前的版本不支持该方法。

```html
<p>浏览器可以播放 MP4视频吗?<span>
    <button onclick="supportType(event,'video/mp4','avc1.42E01E, mp4a.40.2')" type="button">检查</button>
</span></p>
<p>浏览器可以播放 OGG 音频吗?<span>
    <button onclick="supportType(event,'audio/ogg','theora, vorbis')" type="button">检查</button>
</span></p>

<script>
function supportType(e,vidType,codType)
{
  myVid=document.createElement('video');
  isSupp=myVid.canPlayType(vidType+';codecs="'+codType+'"');
  if (isSupp=="")
  {
    isSupp="不支持";
  }
  e.target.parentNode.innerHTML="检查结果: " + isSupp;
}
</script>
```

<p>浏览器可以播放 MP4视频吗? <span>
    <button onclick="supportType(event,'video/mp4','avc1.42E01E, mp4a.40.2')" type="button">检查</button>
</span></p>
<p>浏览器可以播放 OGG 音频吗? <span>
    <button onclick="supportType(event,'audio/ogg','theora, vorbis')" type="button">检查</button>
</span></p>

<script>
function supportType(e,vidType,codType)
{
  myVid=document.createElement('video');
  isSupp=myVid.canPlayType(vidType+';codecs="'+codType+'"');
  if (isSupp=="")
  {
    isSupp="不支持";
  }
  e.target.parentNode.innerHTML="检查结果: " + isSupp;
}
</script>

### load() 方法

load() 方法用于重新加载音频或视频文件。load()方法的语法格式如下：

```javascript
audio|video.load()
```
下面是一个具体使用的例子,单击【更改加载视频】按钮，即可切换到下一个视频：

```html
<button onclick="changeSource()" type="button">更改加载视频</button>

<video id="video3" controls="controls">
  <source id="mp4_src" src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>

<script> 
function changeSource()
{ 
  document.getElementById("mp4_src").src="https://media.everdo.cn/tank/xiaofan/video/2018/nbez304-h264-hd_raw.mp4";
  document.getElementById("video3").load();
} 
</script>
```

<button onclick="changeSource()" type="button">更改加载视频</button>

<video id="video3" controls="controls" width="100%">
  <source id="mp4_src" src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>

<script> 
function changeSource()
{ 
  document.getElementById("mp4_src").src="https://media.everdo.cn/tank/xiaofan/video/2018/nbez304-h264-hd_raw.mp4";
  document.getElementById("video3").load();
} 
</script>

### play() 和 pause() 方法

play() 方法用于开始播放音频或视频文件。pause() 方法用于暂停当前播放的音频或视频文件。

下面是一个具体使用的例子,为了更好体现效果，这里禁用了浏览器自带的播放控件。在案例中单击【播放视频】按钮，则视频开始播放；单击【暂停视频】按钮，则视频暂停播放：

```html
<button onclick="playVid()" type="button">播放视频</button>
<button onclick="pauseVid()" type="button">暂停视频</button>

<video id="video4">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>

<script>
var myVideo=document.getElementById("video4"); 
function playVid()
{ 
  myVideo.play(); 
} 

function pauseVid()
{ 
  myVideo.pause(); 
} 
</script> 
```

<button onclick="playVid()" type="button">播放视频</button>
<button onclick="pauseVid()" type="button">暂停视频</button> 

<video id="video4" width="100%">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>
<script> 
var myVideo=document.getElementById("video4"); 
function playVid()
{ 
  myVideo.play(); 
} 
function pauseVid()
{ 
  myVideo.pause(); 
} 
</script> 

### buffered 属性 (JS)

buffered 属性返回 TimeRanges 对象。TimeRanges 对象表示用户的音频或视频缓冲范围。缓冲范围指的是已缓冲音频或视频的时间范围。如果用户在音频或视频中跳跃播放，就会得到多个缓冲范围。

返回buffered属性的语法格式如下：

```html
audio|video.buffered
```
下面是一个具体使用的例子,单击【获得视频的第一段缓冲范围】按钮，即可看到此时视频的缓冲范围:

```html
<button onclick="getFirstBuffRange()" type="button">获得视频的第一段缓冲范围</button>

<video id="video5" controls="controls">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>

<script>
myVid=document.getElementById("video5");
function getFirstBuffRange()
{ 
  alert("开始: " + myVid.buffered.start(0) + " 结束: "  + myVid.buffered.end(0));
} 
</script>
```

<button onclick="getFirstBuffRange()" type="button">获得视频的第一段缓冲范围</button>

<video id="video5" controls="controls" width="100%">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>
<script>
myVidtime=document.getElementById("video5");
function getFirstBuffRange()
{ 
  alert("开始: " + myVidtime.buffered.start(0) + " 结束: "  + myVidtime.buffered.end(0));
} 
</script>

### currentSrc 属性 (JS)

currentSrc 属性返回当前音频或视频的 URL。如果未设置音频或视频，则返回空字符串。返回currentSrc 属性的语法格式如下：

```html
audio|video.currentSrc
```

下面是一个具体使用的例子,单击【获得当前视频的URL】按钮，即可看到当前视频的 URL 路径:

```html
<button onclick="getVid()" type="button">获得当前视频的URL：</button>

<video id="video6" controls="controls">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>

<script>
myVid=document.getElementById("video6");
function getVid()
{
  alert(myVid.currentSrc);
}
</script>
```

<button onclick="getVid()" type="button">获得当前视频的URL：</button>

<video id="video6" controls="controls" width="100%">
  <source src="https://media.everdo.cn/tank/xiaofan/video/2019/vlog-19-07-zhoushan_h264.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 video  标签。
</video>
<script>
myVidurl=document.getElementById("video6");
function getVid()
{
  alert(myVidurl.currentSrc);
}
</script>
