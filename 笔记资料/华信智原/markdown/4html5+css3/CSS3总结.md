### 1.CSS3新属性
- border-radius:30px/10%;
- box-shadow:5px 5px 5px #ccc;
- border-image;//支持性较差IE9都不支持
- background-size;//设置背景尺寸；拉伸背景图，填充满整个背景
- background-origin;//规定背景图片的定位区域：content-box、padding-box、border-box
- CSS3中可以插入多重背景图片：background-image：url(1),url(2)...;
- text-shadow:5px 5px 5px #ccc;
- word-wrap:文字强制换行
- text-justify
- text-overflow：文本溢出包含元素时发生的事
- elipsis：显示省略号来代表超出的文字
- 自定义字体
- 2d转换：移动、缩放、转动、拉伸等操作
- translate();//移动
- rotate();//旋转
- -ms-兼容IE
- -webkit-兼容Chrome、safri
- -moz-兼容火狐
- - o-兼容欧鹏
- transform：rotate(45deg);
- transform:translate(50px,100px);//百分比获取的是元素宽高的百分比偏移，可用来实现元素居中显示。
- transform:scaleX(3);//倍数拉伸，以中心为基准
- transform：scale(2,3);
- transform:skewX(30deg);//元素翻转
- transform:skew(20deg,20deg);
- 3d转换：IE10以上才支持
- rotateX、rotateY
- transform：转换、变形
- perspective：给父元素添加，子元素有透视效果；兼容较差，Chrome都必须加前缀兼容
- 过渡效果：transition;元素从一种样式逐渐变成另一种样式的效果。
- transition：all 3s;同时改变所有样式，多个样式也可以用逗号分隔。
- 动画效果：@keyframes、通过animation绑定到选定元素来调用动画
- infinite：无限循环
- forwards：动画停留在最后一帧

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			div{
				width:200px;
				height:200px;
				float: left;
				text-align: center;
				line-height: 200px;
				font-size:30px;
				opacity: .8;
				position: absolute;
			}
			
			#box{
				
				border: 1px solid #000;
				position: absolute;
				left:50%;
				top:50%;
				transform: translate(-50%,-50%);
				transform-style:preserve-3d ;
				transition: all;
			}
			#box:hover{
				transform: rotateX(45deg) rotateY(45deg);
			}
			#box1{
				background-color:red;
				transform: translateZ(100px);
			}
			#box2{
				background-color:yellow;
				transform: rotateY(90deg);
				transform: translateZ(100px);
			}
			#box3{
				background-color:skyblue;
				
				transform: translateZ(-100px);
			}
			#box4{
				background-color:lightgreen;
				transform: rotateY(90deg);
				transform: translateZ(-100px);
			}
			#box5{
				background-color: purple;
				transform: rotateX(90deg);
				transform: translateZ(100px);
			}
			#box6{
				background-color:brown;
				transform: rotateX(90deg);
				transform: translateZ(-100px);
			}
		</style>
	</head>
	<body>
		<div id="box">
			<div id="box1">前</div>
			<div id="box2">左</div>
			<div id="box3">后</div>
			<div id="box4">右</div>
			<div id="box5">上</div>
			<div id="box6">下</div>
		</div>		
	</body>
</html>

```

### 2.标准盒模型
- 存在问题：布局时border和padding会撑大盒模型
- 非标准盒模型
  - box-sizing:content-box;
  - box-sizing:border-box;
  - IE8以上才兼容

### 3.flex布局：弹性盒子布局
- IE10以上才支持，移动端可大胆使用
- display:flex/inline-flex;定义盒子为弹性容器。
- dispaly:-webkit-flex;兼容webkit内核浏览器兼容。
- 设置为flex后，子元素的float、clear、vertical-align就不生效了。
- 容器：父元素；项目：子元素；主轴：main axis；交叉轴：cross axis；主轴开始结束位置：main start/end；交叉轴开始结束位置：cross start/end；项目占据位置：main size/cross size;
- 容器属性（添加给父元素的属性）：
  - flex-direction：决定主轴的方向（即项目的排列方式）。
    - row：默认值，方向水平从左向右；float：left；
    - row-reverse：水平从右往左；float：right；
    - column：列方式排列从上往下；
    - column-reverse：从下往上；
  - flex-wrap：决定项目排不下时如何换行。
    - nowrap：默认值，不换行；
    - wrap：正常换行，多出的排在下面；
    - wrap-reverse：多出的排在上面；
  - flex-flow：就是flex-direction和flex-wrap的简写合并；
  - justify-content：定义项目在主轴上的对齐方式。
    - center：项目居中；
    - flex-start：默认值，左对齐；
    - flex-end：右对齐；
    - space-between：两端对齐，项目之间距离等分；
    - space-around：每个项目之间间隔相等，项目与父元素之间距离是项目之间距离的一半；
  - align-items：定义项目在交叉轴上的对齐方式。
    - center：居中；
    - flex-start：顶部对齐；
    - flex-end：底部对齐；
    - baseline：项目第一行文字基线对齐；
    - stretch：默认值；
  - align-content：定义多根轴线的对齐方式。（用的不多）
- 项目属性（添加给子元素的属性）：
  - flex-grow：弹性分组，默认值0，1占满剩余空间。==加了该属性，width属性就失效了。==
  - flex-shrink：项目缩小比例。
  - align-self：允许项目有不同于其他项目的属性。可覆盖父元素的align-items属性。
  

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding: 0;
			}
			.father{
				width: 200px;
				height: 200px;
				margin: 200px auto;
				position: relative;
				transform-style:preserve-3d ;
				animation: go 5s infinite alternate;
			}
			.box{
				width:200px;
				height:200px;
				border: 1px solid #000;
				box-shadow: 5px 5px 5px #ccc;
				border-radius: 10px;
				float: left;
				display: flex;
				position: absolute;
				background-color:skyblue;
			}
			.dian{
				width: 50px;
				height: 50px;
				border-radius: 50%;
				background-color: red;
			}			
			.box1{
				
				justify-content: center;
				align-items: center;
				transform: translateZ(100px);
			}
			.box2{
				justify-content:space-around;
				align-items: center;
				transform: rotateY(90deg) translateZ(-100px);
			}
			.box3{
				justify-content: space-around;	
				transform: rotateX(90deg) translateZ(100px);			
			}
			.box3 .dian{
				margin: 10px 0;
			}
			.box3 .dian:nth-child(2){
				align-self: center;
			}
			.box3 .dian:nth-child(3){
				align-self: flex-end;
			}
			.box4{
				flex-wrap:wrap;
				justify-content: center;
				align-items: center;
				transform: rotateX(90deg) translateZ(-100px);
			}
			.box4 .dian{
				margin: 10px;
			}
			.box5{				
				flex-wrap:wrap;
				justify-content: center;
				align-items: center;
				transform:rotateY(90deg) translateZ(100px);			
			}
			.box5 .dian{
				margin:5px 20px;
			}
			.box5 .dian:nth-child(3){
				margin:5px 75px;
			}
			.box6{
				flex-wrap:wrap;
				justify-content: center;
				align-items: center;
				transform: translateZ(-100px);
			}
			.box6 .dian{
				margin:5px 20px;
			}
			@keyframes go{
				from{transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);}
				to{transform: rotateX(360deg) rotateY(360deg) rotateZ(360deg);}
			}
		</style>
	</head>
	<body>
		<div class="father">
			<div class="box box1">
				<div class="dian"></div>			
			</div>
			<div class="box box2">
				<div class="dian"></div>
				<div class="dian"></div>
			</div>
			<div class="box box3">
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>
			</div>
			<div class="box box4">
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>
			</div>
			<div class="box box5">
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>			
				<div class="dian"></div>
			</div>
			<div class="box box6">
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>
				<div class="dian"></div>			
				<div class="dian"></div>
				<div class="dian"></div>
			</div>
		</div>		
	</body>
</html>

```

[阮一峰日志](http://www.ruanyifeng.com/blog/archives.html)

### 4.视口：meta标签
- meta_viewport
- name=viewport；
- content="width=device-width（设置宽度为视口宽度）,initial-scale=1（设置初始缩放为1）,minimum-scale=1（设置最小缩放比例为1）,maxmum-scale=1（设置最大缩放比例为1）,user-scalable=no（禁止用户缩放）";//为移动端设计的标签,用于移动端页面尺寸根据屏幕自适应

### 5.CSS3媒体查询
- @media only screen and(max-width:600px){div{...}};
- @media only screen and(min-width:601px) and (max-width:800px){div{...}};
- @media only screen and(min-width:801px) and (max-width:960px){div{...}};
- @media only screen and(min-width:961px){div{...}};


```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			.box{
				width:100%;
				height:100px;
				text-align: center;				
				line-height: 100px;
			}
			@media only screen and (max-width: 600px){
				.box{
					font-size: 20px;
					background-color: red;
				}
			}
			@media only screen and (min-width:601px) and (max-width: 800px){
				.box{
					font-size: 30px;
					background-color: blue;
				}
			}
			@media only screen and (min-width:801px) and (max-width: 960px){
				.box{
					font-size: 40px;
					background-color: green;
				}
			}
			@media only screen and (min-width:961px) and (max-width: 1200px){
				.box{
					font-size: 50px;
					background-color: yellow;
				}
			}
			@media only screen and (min-width:1201px){
				.box{
					font-size: 60px;
					background-color: purple;
				}
			}
		</style>
	</head>
	<body>
		<div class="box">
			媒体查询			
		</div>
	</body>
</html>

```

### 6.页面尺寸分区
- 超小屏幕768px以下
- 小屏幕768px到992px
- 中等屏幕992px以上
- 大屏幕1200px以上

### 7.尺寸单位（面试题）
- rem：root相对于根元素值大小的倍数
- html{font-size：16px;//Chrome默认大小是16px，最小是12px}
  - 在媒体查询中改变根元素font-size大小，可实现动态页面布局；
- 1rem=16px；
- em：相对其父元素字体值大小的倍数
- px：固定值
- rem配合媒体查询代码


[电子书查询网站](https://www.jiumodiary.com/)  
[资源搜索网站](https://www.chongbuluo.com/)  
[网站设计欣赏](https://www.xuansite.com/)