---
title: HTML文档整理 07-定位，离线和WEB存储
date: 2020-03-16 19:01:26
category: HTML学习
tags: html
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/03/13/html5.png
---

在HTML5网页代码中，通过一些有用的API，可以查找访问者当前的位置。若要体验本文里所有的案例，请务必在浏览器授权本站使用你的地理信息位置，否则将无法定位。

## 地理定位的函数

通过地理定位可以确定用户的当前位置，并能获取用户地理位置的变化情况。其中，比较常用的就是 API 中的 getCurrentpositong() 函数。

> API 是应用程序的编程接口，是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件以访问一组例程的能力。

getCurrentpositong() 函数的语法格式如下：

```javascript
navigator.geolocation.getCurrentPosition( successCallback, errorCallback, options)
```

> Navigator 对象包含有关浏览器的信息。注释：没有应用于 navigator 对象的公开标准，不过所有浏览器都支持该对象。

其中 successCallback 参数是指在位置成功获取时用户想要调用的函数名称；errorCallback 参数是指在位置获取失败时用户想要调用的函数名称；options 参数指出地理定位时的属性设置。访问用户位置是耗时的操作，同时出于隐私问题，还要取得用户的同意。

### successCallback: 

该对象包含两个属性：coords 和 timestamp。

若成功，则 getCurrentPosition() 方法返回对象。始终会返回 latitude、longitude 以及 accuracy 属性。如果可用，则会返回其他下面的属性。

属性|描述
--|--
coords.latitude|（始终）十进制数的纬度
coords.longitude|（始终）十进制数的经度
coords.accuracy|（始终）位置精度
coords.altitude|海拔，海平面以上以米计
coords.altitudeAccuracy|位置的海拔精度
coords.heading|方向，从正北开始以度计
coords.speed|速度，以米/每秒计
timestamp|响应的日期/时间

### errorCallback: 

返回的错误代码包含两个属性：message：错误信息；code：错误代码

错误代码包含四个值：unknow_error: 表示不包括在其他错误代码中的错误，可以在 message 中查找信息。permission_denied: 表示用户拒绝浏览器获取位置信息的请求。position unavalablf: 表示网络不可用或者连接不到卫星。timeout: 表示获取超时时。必须在 options 中指定了 timeout 值时才有可能发生这种错误。


### PositionOptions: 

数据格式为 json，有3个属性：

enableHighAcuracy：布尔值，表示是否启用高精确度模式，如果启用这个模式，浏览器在获取位置信息时可能需要耗费更多的时间。Timeout: 整数，表示浏览器需要在指定的时间内获取位置信息，否则触发 errorCallback。maximumAge: 整数/常量，表示浏览器重新获取位置信息的时间间隔。

### 使用样例

通过上面的 API 说明，就可以用下面的 **displayOnMap函数** 来调用经纬度坐标：

```javascript
function displayOnMap(position){
    var latitude=position.coords.latitude;    //经度
    var longitude=position.coords.longitude;    //纬度
}
```

下面是定位 API 的一些具体使用案例：

#### 最基本使用

```html
01 直接输出样例：

<p id="demo">暂未获取地理位置</p>
<script>
var x=document.getElementById("demo");
navigator.geolocation.getCurrentPosition(
	function showPosition(position)
  	{
  		x.innerHTML="Latitude: " + position.coords.latitude + 
  		"<br />Longitude: " + position.coords.longitude;	
  	}
);
</script>
```

<p id="demo">暂未获取地理位置</p>
<script>
var x=document.getElementById("demo");
navigator.geolocation.getCurrentPosition(
	function showPosition(position)
  	{
  		x.innerHTML="Latitude: " + position.coords.latitude + 
  		"<br />Longitude: " + position.coords.longitude;	
  	}
);
</script>

> 上面展示的是一个最基本的案例，我对此解读如下：首先创建一个 id 为 demo 的段落，然后编写 JavaScript 脚本。脚本中声明变量 x 指向 id 为 demo 的段落。
> 
> 接下来调用 getCurrentPosition() 的 API，因为 API 需要配合回调的函数，因此这里新建了一个 showPosition 的函数，并新建一个名为 position 的变量。变量 position 的值会在 getCurrentPosition() 函数执行时，被传递参数，因此接下来只要输出 position 被传参后的的信息即可。

因此，现在 position.coords.latitude 和 position.coords.longitude 里的值，就是精度纬度了。使用 x.innerHTML 就改变了前面段落 ```<p id="demo"> </p>``` 里的值了！

#### 使用按钮并检查浏览器

```html
02 按钮输出并执行浏览器兼容检查：

<p id="demoA">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocationOne()">试一下</button>
<script>
var a=document.getElementById("demoA");
function getLocationOne()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.getCurrentPosition(showPositionOne);
    }
  else{a.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPositionOne(positionA)
  {
  a.innerHTML="Latitude: " + positionA.coords.latitude + 
  "<br />Longitude: " + positionA.coords.longitude;	
  }
</script>
```

<p id="demoA">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocationOne()">试一下</button>
<script>
var a=document.getElementById("demoA");
function getLocationOne()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.getCurrentPosition(showPositionOne);
    }
  else{a.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPositionOne(positionA)
  {
  a.innerHTML="Latitude: " + positionA.coords.latitude + 
  "<br />Longitude: " + positionA.coords.longitude;	
  }
</script>

> 在这段代码中，为了实现点击按钮显示经纬度，因此为按钮点击添加了 onclick="getLocationOne()" 事件。点击后触发 getLocationOne() 函数，该函数使用一个 if 语句对浏览器是否能对 navigator.geolocation 返回值进行了判断。如果有返回值，就执行后面的函数调用。
> 
> 此处为 getLocationOne() 指定了回调函数 showPositionOne() 并使用 positionA 变量来传递参数。

```
判断浏览器是否支持地理位置服务：

if ("geolocation" in navigator) {
  /* 地理位置服务可用 */
} else {
  /* 地理位置服务不可用 */
}
```

在 mozilla 官方文档中,如果 geolocation 对象存在，那么地理位置服务可用。

#### 输出报错

```html
03 异常时输出错误信息：

<p id="demoB">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocationTwo()">试一下</button>
<script>
var b=document.getElementById("demoB");
function getLocationTwo()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.getCurrentPosition(showPositionTwo,showError);
    }
  else{b.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPositionTwo(positionB)
  {
  b.innerHTML="Latitude: " + positionB.coords.latitude + 
  "<br />Longitude: " + positionB.coords.longitude;	
  }
function showError(error)
  {
  switch(error.code) 
    {
    case error.PERMISSION_DENIED:
      b.innerHTML="User denied the request for Geolocation."
      break;
    case error.POSITION_UNAVAILABLE:
      b.innerHTML="Location information is unavailable."
      break;
    case error.TIMEOUT:
      b.innerHTML="The request to get user location timed out."
      break;
    case error.UNKNOWN_ERROR:
      b.innerHTML="An unknown error occurred."
      break;
    }
  }
</script>
```

<p id="demoB">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocationTwo()">试一下</button>
<script>
var b=document.getElementById("demoB");
function getLocationTwo()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.getCurrentPosition(showPositionTwo,showError);
    }
  else{b.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPositionTwo(positionB)
  {
  b.innerHTML="Latitude: " + positionB.coords.latitude + 
  "<br />Longitude: " + positionB.coords.longitude;	
  }
function showError(error)
  {
  switch(error.code) 
    {
    case error.PERMISSION_DENIED:
      b.innerHTML="User denied the request for Geolocation."
      break;
    case error.POSITION_UNAVAILABLE:
      b.innerHTML="Location information is unavailable."
      break;
    case error.TIMEOUT:
      b.innerHTML="The request to get user location timed out."
      break;
    case error.UNKNOWN_ERROR:
      b.innerHTML="An unknown error occurred."
      break;
    }
  }
</script>

> 这里创建了一个 showError(error) 的函数作为 getCurrentPosition() 执行错误时的回调对象。 errorCallback 的参数传递到 error 变量中。

#### 其他有趣的方法

- watchPosition() - 返回用户的当前位置，并继续返回用户移动时的更新位置（就像汽车上的 GPS）。
- clearWatch() - 停止 watchPosition() 方法

下面的例子展示 watchPosition() 方法。您需要一台精确的 GPS 设备来测试该例（比如 iPhone）：

```html
<p id="demoC">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocationThree()">试一下</button>
<script>
var c=document.getElementById("demoC");
function getLocationThree()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.watchPosition(showPositionThree);
    }
  else{c.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPositionThree(positionC)
  {
  c.innerHTML="Latitude: " + positionC.coords.latitude + 
  "<br />Longitude: " + positionC.coords.longitude;	
  }
</script>
```

<p id="demoC">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocationThree()">试一下</button>
<script>
var c=document.getElementById("demoC");
function getLocationThree()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.watchPosition(showPositionThree);
    }
  else{c.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPositionThree(positionC)
  {
  c.innerHTML="Latitude: " + positionC.coords.latitude + 
  "<br />Longitude: " + positionC.coords.longitude;	
  }
</script>

> watchPosition() 和 上面提到的 getCurrentPosition() 方法完全一致，可以直接套用。但却能实时跟踪位置变化。

### 使用地图 API

为了在地图上显示用户的具体位置，可以利用地图网站的API。下面以使用百度地图为例，需要使用Baidu Maps Javascript API。

在使用此API前，需要在HTML5页面中添加一个引用，具体代码如下；

```html
标准引入（适用于多数情况）：

<script type="text/javascript" src="//api.map.baidu.com/api?type=webgl&v=1.0&ak=您的密钥"></script>
```

```html
异步调用（进阶优化选项）：

<script type="text/javascript"> 
//异步加载js返回callback函数
function loadScript() { 
    var script = document.createElement("script"); 
    script.src = "https://api.map.baidu.com/api?v=1.0&type=webgl&ak=这个要自己申请哦&callback=hxfmapint";
    document.body.appendChild(script); 
} 
window.onload = loadScript;
</script>
```

其中*号代码注册到 key。注册 key 的方法为：在 [百度地图开放平台](http://lbsyun.baidu.com/index.php?title=jspopular)  网页中注册百度地图API，然后输入需要内置百度地图页面的URL地址生成API密钥，最后将key文件复制保存。

其中百度地图的更细致的使用文档需要参考百度官方文档：[lbs.baidu.com](http://lbs.baidu.com/)

```html
完整的带定位的异步调用接口使用实例：

<style type="text/css">
	#hxfmap {width: 100%;height: 400px;overflow: hidden;margin:0;font-family:"微软雅黑";}
</style>

<script type="text/javascript"> 
//异步加载js返回callback函数
function loadScript() { 
    var script = document.createElement("script"); 
    script.src = "https://api.map.baidu.com/api?v=1.0&type=webgl&ak=这个要自己申请哦&callback=hxfmapint";
    document.body.appendChild(script); 
} 
window.onload = loadScript; 
</script>

<script type="text/javascript">
function hxfmapint() { 
    // 按住鼠标右键，修改倾斜角和角度
    // GL版命名空间为BMapGL
	var map = new BMapGL.Map("allmap");    // 创建Map实例
	var point = new BMapGL.Point(121.548899, 29.870192);
	map.centerAndZoom(point,19);
    map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
    map.addEventListener('click', function(e) {
        alert('点击的经纬度：' + e.latlng.lng + ', ' + e.latlng.lat);
        var mercator = map.lnglatToMercator(e.latlng.lng, e.latlng.lat);
        alert('点的墨卡托坐标：' + mercator[0] + ', ' + mercator[1]);
    });
    // 实现定位功能
    var geolocation = new BMapGL.Geolocation();
	geolocation.getCurrentPosition(function(r){
		if(this.getStatus() == BMAP_STATUS_SUCCESS){
			var mk = new BMapGL.Marker(r.point);
			map.addOverlay(mk);
			map.panTo(r.point);
			alert('您的位置：'+r.point.lng+','+r.point.lat);
		}
		else {
			alert('failed'+this.getStatus());
		}        
	},{enableHighAccuracy: true})
}
</script>

<div id="hxfmap">这里将显示地图</div>
```

<style type="text/css">
	#hxfmap {width: 100%;height: 400px;overflow: hidden;margin:0;font-family:"微软雅黑";}
</style>
<script type="text/javascript"> 
//异步加载js返回callback函数
function loadScript() { 
    var script = document.createElement("script"); 
    script.src = "https://api.map.baidu.com/api?v=1.0&type=webgl&ak=tegOOlMnipQTOgHLwFtzHukBKNjIHzUp&callback=hxfmapint";
    document.body.appendChild(script); 
} 
window.onload = loadScript; 
</script>
<script type="text/javascript">
function hxfmapint(dw) {
  var dw; 
    // 按住鼠标右键，修改倾斜角和角度
	var map = new BMapGL.Map("hxfmap");    // 创建Map实例，GL版命名空间为BMapGL
	var point = new BMapGL.Point(121.548899, 29.870192);
	map.centerAndZoom(point,19);
  map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
  map.addEventListener('click', function(e) {
      alert('点击的经纬度：' + e.latlng.lng + ', ' + e.latlng.lat);
      var mercator = map.lnglatToMercator(e.latlng.lng, e.latlng.lat);
      alert('点的墨卡托坐标：' + mercator[0] + ', ' + mercator[1]);
  });
  var scaleCtrl = new BMapGL.ScaleControl();  // 添加比例尺控件
  map.addControl(scaleCtrl);
  var zoomCtrl = new BMapGL.ZoomControl();  // 添加比例尺控件
  map.addControl(zoomCtrl);
  map.setHeading(64.5);
	map.setTilt(40);
  var opts = {
	  position: point,   // 指定文本标注所在的地理位置
	  offset: new BMapGL.Size(30, -30)    //设置文本偏移量
	}
	var label = new BMapGL.Label("喵喵喵，我是 Emptinessboy", opts);  // 创建文本标注对象
	label.setStyle({
		color : '#555',
		fontSize : '12px',
		height : '20px',
		lineHeight : '20px',
		fontFamily: '微软雅黑'
	});
	map.addOverlay(label);
  if(dw==true){
  var geolocation = new BMapGL.Geolocation();
	geolocation.getCurrentPosition(function(r){
		if(this.getStatus() == BMAP_STATUS_SUCCESS){
			var mk = new BMapGL.Marker(r.point);
			map.addOverlay(mk);
			map.panTo(r.point);
			alert('您的位置：'+r.point.lng+','+r.point.lat);
		}
		else {
			alert('failed'+this.getStatus());
		}        
	},{enableHighAccuracy: true})
  }
}
</script>
<button onclick="hxfmapint(true)">展示我的定位</button><!--传递是否定位参数-->
<div id="hxfmap"></div>

哈哈哈，上述案例中，可以给地图设一个初始经纬度坐标点，比如我设置的我高中的坐标 (121.548899, 29.870192)

### 为什么无法定位？

> Secure context：This feature is available only in secure contexts (HTTPS), in some or all supporting browsers.（只有网站升级到 HTTPS 才能使用地理位置 API）

> 注意: 出于安全考虑，当网页请求获取用户位置信息时，用户会被提示进行授权。注意不同浏览器在请求权限时有不同的策略和方式。Windows10在未开启定位的情况下无法获取位置

## H5 离线 Web 应用

为了能在离线的情况下访问网站，可以采用HTML5的离线Web功能。应用程序缓存为应用带来三个优势：

1. 离线浏览 - 用户可在应用离线时使用它们
2. 速度 - 已缓存资源加载得更快
3. 减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。

在 HTML5 中新增了本地缓存（也就是 HTML 离线 Web 应用），主要是通过应用程序缓存整个离线网站的 HTML、CSS、Javascript、网站图像和资源。当服务器没有和 Internet 建立连接的时候，也可以利用本地缓存中的资源文件来正常运行Web应用程序。另外，如果网站发生了变化，则应用程序缓存将重新加载变化的数据文件。

### 应用程序缓存 manifest

manifest 文件是一个简单文本文件，在该文件中以清单的形式列举了需要被缓存或不需要被缓存的资源文件的文件名称，以及这些资源文件的访问路径。

Manifest 文件把指定的资源文件类型分为三类，分别是 “CACHE” “NETWORK” 和 “FALLBACK”。这三类的含义分别如下：

（1）CACHE 类别：该类别指定需要被缓存在本地的资源文件。这里需要特别注意的是，在为某个页面指定需要本地缓存的资源文件时，不需要把这个页面本身指定在 CACHE 类型中，因为如果一个页面具有 manifest 文件，则浏览器会自动对这个页面进行本地缓存。

（2）NETWORK 类别：该类别为不进行本地缓存的资源文件，这些资源文件只有当客户端与服务器端建立连接的时候才能访问。

（3）FALLBACK 类别：该类别中指定两个资源文件，其中一个资源文件为能够在线访问时使用的资源文件，另一个资源文件为不能在线访问时使用的备用资源文件。

#### Manifest 基础

如需启用应用程序缓存，需要在文档的 ```<html>``` 标签中包含 manifest 属性：

```html
<!DOCTYPE HTML>
<html manifest="demo.appcache">
...
</html>
```
每个指定了 manifest 的页面在用户对其访问时都会被缓存。如果未指定 manifest 属性，则页面不会被缓存（除非在 manifest 文件中直接指定了该页面）。

manifest 文件的建议的文件扩展名是：".appcache"。

> 注意，manifest 文件需要配置正确的 MIME-type，即 "text/cache-manifest"。必须在 web 服务器上进行配置。

#### Manifest 语法

manifest 文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。

文章的前面部分已经提及，manifest 文件可分为三个部分：

- CACHE MANIFEST
- NETWORK
- FALLBACK

***CACHE MANIFEST***

第一行，CACHE MANIFEST，是必需的：

```
CACHE MANIFEST
/theme.css
/logo.gif
/main.js
```

上面的 manifest 文件列出了三个资源：一个 CSS 文件，一个 GIF 图像，以及一个 JavaScript 文件。当 manifest 文件加载后，浏览器会从网站的根目录下载这三个文件。然后，无论用户何时与因特网断开连接，这些资源依然是可用的。

***NETWORK***

下面的 NETWORK 小节规定文件 "login.asp" 永远不会被缓存，且离线时是不可用的：

```
NETWORK:
login.asp
```

可以使用星号来指示所有其他资源/文件都需要因特网连接：

```
NETWORK:
*
```

***FALLBACK***
下面的 FALLBACK 小节规定如果无法建立因特网连接，则用 "offline.html" 替代 /html5/ 目录中的所有文件：

```
FALLBACK:
/html5/ /404.html
```
其中第一个 URI 是资源，第二个是替补。

#### 完整的 Manifest 文件

```
CACHE MANIFEST
# 2012-02-21 v1.0.0
/theme.css
/logo.gif
/main.js

NETWORK:
login.asp

FALLBACK:
/html5/ /404.html
```

重要的提示：以 "#" 开头的是注释行，但也可满足其他用途。应用的缓存会在其 manifest 文件更改时被更新。如果您编辑了一幅图片，或者修改了一个 JavaScript 函数，这些改变都不会被重新缓存。更新注释行中的日期和版本号是一种使浏览器重新缓存文件的办法。

#### 缓存管理

用户可以为每一个页面单独指定一个mainifest文件，也可以对整个Web应用程序指定一个总的manifest文件。

一旦应用被缓存，它就会保持缓存直到发生下列情况：

- 用户清空浏览器缓存
- manifest 文件被修改（通过注释修改版本号）
- 由程序来更新应用缓存

一旦文件被缓存，则浏览器会继续展示已缓存的版本，即使已经修改了服务器上的文件。为了确保浏览器更新缓存，则需要更新 manifest 文件。

> 注释：浏览器对缓存数据的容量限制可能不太一样（某些浏览器设置的限制是每个站点 5MB）。

#### 演示

```html
这里是样例的 HTML

<!DOCTYPE html>
<html manifest="http-manifest.appcache">
<meta charset="utf-8"/>
<body>
<script src="demo_time.js"></script>
<p id="timePara"><button onclick="getDateTime()">获得日期和事件</button></p>
<p><img src="logo.png"/></p>
<p>首次访问后尝试切断网络，此页面可以被离线访问</p>
<hr>
<p><a href="https://coding.emptinessboy.com/">回文章</a></p>
</body>
</html>
```

```
这里是样例的 manifest

CACHE MANIFEST
demo_time.js
logo.png
```

[演示地址-点我打开](https://huxiaofan.com/doc/http-manicache/)

> 第一次访问演示地址后，脱机仍然可以访问

[![html-manifest.md.jpg](https://media.everdo.cn/tank/pic-bed/2020/03/17/html-manifest.md.jpg)](https://up.media.everdo.cn/image/HqR3)

## Web 存储

HTML5 提供了两种在客户端存储数据的新方法：

- localStorage - 没有时间限制的数据存储
- sessionStorage - 针对一个 session 的数据存储

在 HTML5 中，数据不是由 HTTP 请求传递的，而是只有在请求时使用数据。它使在不影响网站性能的情况下存储大量数据成为可能。

之前，这些都是由 cookie 完成的。但是 cookie 不适合大量数据的存储，因为它们由每个对服务器的请求来传递，这使得 cookie 速度很慢而且效率也不高。本地存储和 Cookies 扮演着类似的角色，但是它们有以下的区别。

（1）本地存储是仅存储在用户的硬盘上并等待用户读取，而 Cookies 是在服务器上读取。

（2）本地存储仅供客户端使用，如果需要服务器端根据存储数值作出反映，就应该使用 Cookies。

（3）读取本地存储不会影响到网络带宽，但是使用 Cookies 将会发送到服务器，这样会影响到网络带宽，无形中增加了成本。

（4）从存储容量上看，本地存储可存储多达 5MB 的数据，而 Cookies 最多只能存储 4KB 的数据信息。

对于不同的网站，数据存储于不同的区域，并且一个网站只能访问其自身的数据。HTML5 使用 JavaScript 来存储和访问数据。

### sessionStorage 函数

sessionStorage 函数针对一个 session 进行数据存储。如果用户关闭浏览器窗口，则数据会被自动删除。创建一个 sessionStorage 函数的基本语法格式如下：

```html
<script type="text/javascript">
sessionStorage.abc=" ";
</script>
```

一个最简单的使用 sessionStorage 存放并读取变量例子：

```html
<script type="text/javascript">
sessionStorage.name="HELLO，我是 Emptinessboy";
document.write(sessionStorage.name);
</script>
```
<p>
<script type="text/javascript">
sessionStorage.name="HELLO，我是 Emptinessboy";
document.write(sessionStorage.name);
</script>
</p>

下面一个计数器案例，刷新页面会看到计数器在增长，关闭浏览器或标签页，然后再试一次，计数器会清零。

```html
<script type="text/javascript">
if (sessionStorage.pagecount)
	{
	sessionStorage.pagecount=Number(sessionStorage.pagecount) +1;
	}
else
	{
	sessionStorage.pagecount=1;
	}
document.write("当前页面会话访问了 " + sessionStorage.pagecount + " 次！");
</script> 
```
<p>
<script type="text/javascript">
if (sessionStorage.pagecount)
	{
	sessionStorage.pagecount=Number(sessionStorage.pagecount) +1;
	}
else
	{
	sessionStorage.pagecount=1;
	}
document.write("当前页面会话访问了 " + sessionStorage.pagecount + " 次！");
</script> 
</p>

### localStorage 函数

与 seessionStorage 函数不同，localStorage 函数存储的数据没有时间限制。也就是说网页浏览者关闭网页很长一段时间后，再次打开此网页时，数据依然可用。

```html
<script type="text/javascript">
localStorage.abc=" ";
</script>
```
一个最简单的使用 localStorage 存放并读取变量例子：

```html
<script type="text/javascript">
sessionStorage.name="HELLO，我是 Emptinessboy";
document.write(localStorage.name);
</script>
```
<p>
<script type="text/javascript">
localStorage.name="HELLO，我是 Emptinessboy";
document.write(localStorage.name);
</script>
</p>

下面一个计数器案例，刷新页面会看到计数器在增长，关闭浏览器窗口，然后再试一次，计数器会继续计数。

```html
<script type="text/javascript">
if (localStorage.pagecount)
	{
	localStorage.pagecount=Number(localStorage.pagecount) +1;
	}
else
	{
	localStorage.pagecount=1;
	}
document.write("你一共访问这个页面 " + localStorage.pagecount + " 次了！");
</script>
```
<p>
<script type="text/javascript">
if (localStorage.pagecount)
	{
	localStorage.pagecount=Number(localStorage.pagecount) +1;
	}
else
	{
	localStorage.pagecount=1;
	}
document.write("你一共访问这个页面 " + localStorage.pagecount + " 次了！");
</script>
</p>

### TIPS

1. 不同的浏览器 Web 存储是独立的

2. 主流浏览器都支持 localStorage 和 sessionStorage