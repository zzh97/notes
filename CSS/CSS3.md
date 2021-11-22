##CSS
###1.什么是CSS
CSS(Cascading Style Sheets)层叠样式表，是用于定义HTML中标签们的属性（它们长成什么样子）  
目前CSS已经发展至CSS3（算是CSS的一个版本）  
与CSS有关扩展知识如下：  
①Less/Sass: 针对CSS的预编译指令  
②Bootstrap: 目前最流行的CSS框架
###2.如何使用CSS
```
<!--三种方法-->
<!--1.标签内写style-->
<div style="color: red"></div>
<!--2.HTML里写style-->
<style>
	div{
		color: red;
	}
</style>
<!--3.引入外部CSS-->
<link rel="stylesheet" href="xxx.css">
```
###3.CSS选择器
```
<style>
/*1.标签选择器*/
div{color: red;}
/*2.id选择器*/
#div{color: red;}
/*3.class选择器*/
.div{color: red;}
/*4.伪类选择器*/
div:hover{color: red;}
/*5.孩子选择器*/
div:nth-child(0){color: red;}
</style>
```
###4.CSS的常见属性
```
div{
	display: block;
	visibility:visible;
	float: left;
	position: relative;
	left: 10px;
	margin-top: 10px;
	width: 100px;
	height: 100px;
	opacity:0.7;
	background: rgba(255,0,0,0.7);
	border: 1px #f00 solid;
	color: white;
	font-size: 20px;
	text-align: center;
	line-height: 100px;
	overflow: hidden;
	cursor: pointer;
	z-index: 99;
	-webkit-user-select:none;
	-moz-user-select:none;
	-ms-user-select:none;
	user-select:none;
}
```
###5.CSS3中的新特性
####阴影
```
div{
	width: 100px;
	height: 100px;
	background: #f55;
	color: white;
	font-size: 20px;
	text-align: center;
	line-height: 100px;
	border-radius: 10px;
	box-shadow: 0rem 0rem 1rem #555;
	text-shadow: 0rem 0rem 1rem #555;
}
```
####过渡
```
div{
	width: 100px;
	height: 100px;
	background: #f55;
	transition:width 1s,opacity 1s;
	-moz-transition: width 1s,opacity 1s;
	-webkit-transition:width 1s,opacity 1s;
	-o-transition:width 1s,opacity 1s;
}
div:hover{
	width: 300px;
}
```
####旋转
```
div{
	width: 100px;
	height: 100px;
	background: #f55;
	transition: transform 1s;
	-moz-transition: transform 1s;
	-webkit-transition:transform 1s;
	-o-transition:transform 1s;
	
}
div:hover{
	transform:rotate(360deg);
	-ms-transform:rotate(360deg);
	-webkit-transform:rotate(360deg);
	-o-transform:rotate(360deg);
	-moz-transform:rotate(360deg);
}
```
####动画
```
@keyframes myfirst
{
0%   {background: red;}
25%  {background: yellow;}
50%  {background: blue;}
100% {background: green;}
}
div{
	width: 100px;
	height: 100px;
	background: red;
	animation: myfirst 5s;
	-moz-animation: myfirst 5s;
	-webkit-animation: myfirst 5s;
	-o-animation: myfirst 5s;
	animation-iteration-count: infinite;
	-webkit-animation-iteration-count: infinite;
}
```
###6.Flex布局
```
<style>
	#main{
		width: 500px;
		height: 500px;
		border: 1px #000 solid;
		display: flex;
		/*row左，row-reverse右，column上， column-reverse下*/
		flex-direction: row;
		/*nowrap不换行 wrap换行 wrap-reverse换行并颠倒*/
		flex-wrap: nowrap; /*元素超过，会被压缩*/
		/*flex-start左对齐 flex-end右对齐 center居中
		space-between两端对齐(等间) space-around两侧等间*/
		justify-content: space-around; /*主轴的对齐方式*/
		align-items: center; /*交叉轴的对齐方式*/
		align-content: flex-end; /*多轴情况(多行)*/
	}
	#main div{
		width: 100px;
		height: 100px;
		background: #f55;
		text-align: center;
		line-height: 100px;
		color: #fff;
		font-size: 20px;
	}
</style>
<div id="main">
	<div>1</div>
	<div>2</div>
	<div>3</div>
</div>
```
###7.Less/Sass
```
<style type="text/less">
//1.值变量
@pink: #f5a;
.box:nth-child(1){
	width: 100px;
	height: 100px;
	background: @pink;
}
//2.变量运算（不能重赋值，如同常量）
@width: 100px;
@width_half: @width / 2;
.box:nth-child(2){
	width: @width;
	height: @width_half;
	background: red;
}
//3.动态选择器, 变量名用{}包起来
@index: 3;
@Selector: .box:nth-child(@index);
@{Selector}{
	width: 100px;
	height: 100px;
	background: @pink;
}
//4.属性变量, 变量名要{}，只有值变量不用
@back: background;
.box:nth-child(4){
	width: 100px;
	height: 100px;
	@{back}: red;
}
//5.声明属性(混合方法的子集)
@height_50px:{height: 50px;};
.box:nth-child(5){
	width: 100px;
	@height_50px();
	@{back}: @pink;
}
//6.变量的作用域，就近原则，无视闭包
@gary: #999;
@backColor: @gary;
.box:nth-child(6){
	width: 100px;
	height: 100px;
	background: @backColor;
	@gary: #555;
}
//7.&上层选择器，有点像this指针
.box:nth-child(7){
	width: 100px;
	height: 100px;
	background: @pink;
	&:hover{
		background: red;
	}
}
//8.混合方法，()可省略
.box_style(){
	width: 50px;
	height: 50px;
	background: red;
}
.box:nth-child(8){
	.box_style();
}
</style>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<!--less.js必须放在style之后，并且style要设置type-->
<script src="js/less.min.js"></script>
```
###8.Bootstrap