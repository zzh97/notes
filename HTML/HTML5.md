###3.HTML5
####1.视频
```
<!--controls自带控件，loop循环播放，autoplay自动播放，preload自动加载（包含于autoplay）-->
<video src="/i/movie.ogg" width="320" height="240" controls="controls" loop="loop" autoplay="autoplay" preload="auto">
	Your browser does not support the video tag.
</video>
```
注： video有play()、pause()、load()三个方法
####2.音频
```
<audio src="/i/song.ogg" controls="controls">
	Your browser does not support the audio element.
</audio>
```
注：方法和属性同上，只是没有宽高
####3.拖拽
####4.画布
```
// 获取canvas节点
var canvas = document.getElementById('canvas');
// 设置绘图环境为2D
var ctx = canvas.getContext('2d');
// 设置填充为红色
ctx.fillStyle="#f00";
// 绘制一个小竖条
ctx.fillRect(0,0,10,50); 
// 设置字号与字体
ctx.font="20px Georgia";
// 绘制文本
ctx.fillText("Hello World!",50,100);
// 创建锚点
ctx.beginPath();
// 移动锚点
ctx.moveTo(0,0);
// 创建并移动锚点
ctx.lineTo(300,150);
// 设置描边为蓝色
ctx.strokeStyle="#00f";
// 绘制锚点路径
ctx.stroke();
// 创建新的锚点
ctx.beginPath();
// 创建弧形锚点路径
ctx.arc(100,150,30,0,2*Math.PI);
// 填充锚点路径
ctx.fill();
```
####5.地理地位
####6.Web存储
```
// 检查是否支持Storege
if (typeof(Storage) !== 'undefined') {
	// 存储，等价于localStorage.user = 'zzh';
	localStorage.setItem('user', 'zzh');
	// 使用，等价于log(localStorage.user);
	log(localStorage.getItem('user'));
}
```
sessionStorage与localStorage用法相同，唯一的区别就是sessionStorage在关闭页面后就会清空
####7.应用缓存
####8.Web Worker
```
var div = document.getElementById('box');
// 检查浏览器是否支持Worker
if(typeof(Worker) !== 'undefined'){
	// 创建Worker对象
	var w = new Worker('xxx.js');
	// 添加一个 "onmessage" 事件监听器
	w.onmessage = function (event){
		// 把返回的数据i写入div中
		div.innerHTML=event.data;
	};
}
// 停止Worker 
w.terminate();
```
在xxx.js中
```
var i=0;
setInterval(function(){
	i++;
	// 向调用者访问数据i，至event.data中
	postMessage(i);
}, 1000);
```
####9.服务器发送事件
```
//检查是否支持EventSource
if(typeof(EventSource) !== 'undefined')
{
	// 创建EventSource对象
	var source = new EventSource('xxx.php');
	// 监听服务器更新
	source.onmessage=function(event)
	{
		// 输出数据
		log(event.data);
	};
}
```
在xxx.php中
```
<?php
	header('Content-Type: text/event-stream');
	header('Cache-Control: no-cache');
	$time = date('r');
	echo "data: The server time is: {$time}\n\n";
	flush();
?>
```