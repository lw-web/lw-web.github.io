[TOC]

### 1.页面上有三个按钮，每个按钮点击后会出现一个对应的盒子。  
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			div{
				width:100px;
				height:100px;
				background-color:skyblue;
				text-align: center;
				vertical-align: middle;
				display: none;
				margin-top:30px;
			}
			button{
				width:50px;
				height:50px;
				background-color: yellow;
			}
		</style>
	</head>
	<body>
		<button id="btn1">1</button>
		<button id="btn2">2</button>
		<button id="btn3">3</button>
		<div id="one">1</div>
		<div id="two">2</div>
		<div id="three">3</div>			
		<script type="text/javascript">			
			function myFunction(boxId,btnId){
				var boxId=document.getElementById(boxId);
				var btnId=document.getElementById(btnId);
				btnId.onclick=function(){
					boxId.style.display="block";
				}
				
			}
			myFunction("one","btn1");
			myFunction("two","btn2");
			myFunction("three","btn3");
		</script>
	</body>
</html>
```
### 2.隔行变色案例，鼠标经过高亮显示
==注意：行内样式权重高于类名设置的样式。==
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			ul{
				list-style: none;
			}
			li{
				line-height:40px;
				margin-top:10px;
				border:1px solid #777;
				padding-left:20px;
				width:300px;
				height:40px;
			}
			.bgc{
				background-color:skyblue!important;				
			}
		</style>
	</head>
	<body>
		<ul>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
			<li>我是段落内容，请仔细阅读。</li>
		</ul>
		<script type="text/javascript">
			var lis=document.getElementsByTagName("li");
			for(var i=0;i<lis.length;i++){
				if(i%2==0){
					lis[i].style.backgroundColor="yellow";					
				}
				lis[i].onmouseover=function(){
					this.className="bgc";
				}
				lis[i].onmouseout=function(){
					this.className="";
				}
			}
		</script>
	</body>
</html>
```
### 3.精灵图实现九宫格布局
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			ul{
				list-style: none;
				width:410px;
				height:310px;
				margin:100px auto;				
				border:1px solid #666;
				padding-left:20px;
			}
			li{
				display: block;
				width:100px;
				height:100px;
				float:left;
				text-align: center;
				margin-bottom: 10px;
			}
			i{
				display:block;
				width:44px;
				height:44px;
				background:url(img/QQ图片20190326144407.png) no-repeat;
				margin-top:10px;
				margin-left:40px;
			}
			a{
				text-decoration: none;
				color:#999;
				font-size:18px;
			}
		</style>
	</head>
	<body>
		<ul>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
			<li>
				<i></i>
				<a href="">充话费</a>
			</li>
		</ul>
		<script type="text/javascript">
			var is=document.getElementsByTagName("i");
			for(var i=0;i<is.length;i++){
				is[i].style.backgroundPosition="0px "+(-43*i)+"px";// 空格不能少
//				is[i].style.backgroundPositionY=(-43*i)+"px";// 只有Y方向变量改变
			}
		</script>
	</body>
</html>
```
### 4.京东搜索框

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
				position: relative;
			}
			#container{
				width: 500px;
				margin:100px auto;
			}
			#txt{
				height:30px;
				width:500px;
			}
			#label{
				position: absolute;
				top:5px;;
				left:10px;
				cursor: text;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<input type="text" id="txt"/>
			<label id="label" for="txt">默认商品</label>
		</div>
		<script type="text/javascript">
			var txt=document.getElementById("txt");
			var label=document.getElementById("label");
			txt.onfocus=function(){
				label.style.color="#666";
			}
			txt.onblur=function(){
				label.style.color="black";				
			}
			txt.oninput=function(){
				label.style.display="none";	
				if(txt.value==""){
					label.style.display="block";
				}
			}
		</script>		
	</body>
</html>
```
### 5.排它思想，让盒子点击单独高亮
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			div{
				width:100px;
				height:100px;
				float:left;
				border:1px solid red;
				margin:100px 20px;
			}
		</style>
	</head>
	<body>
		<div></div>
		<div></div>
		<div></div>
		<div></div>
		<div></div>
		<div></div>
		<div></div>		
		<script type="text/javascript">
			var divs=document.getElementsByTagName("div");
			for(var i=0;i<divs.length;i++){
				divs[i].onclick=function(){
					for(var j=0;j<divs.length;j++){
						divs[j].style.backgroundColor="";
					}
					this.style.backgroundColor="blue";
				}
			}			
		</script>		
	</body>
</html>
```
### 6.tab栏效果
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#container{
				width:382px;
				height:440px;
				border:1px solid #666;
				margin:100px auto;
			}
			#big{
				margin:auto;
				width:360px;
				height:360px;
			}
			#small li{
				display: inline-block;
				list-style: none;
				border:1px solid #666;
			}			
			#big img{
				display: none;
			}
			#small .light{
				border:2px red solid;
			}
			#big .show{
				display: block;
			}
		</style>
	</head>
	<body>
		<div id="container">			
			<div id="small">
				<ul>
					<li class="light"><img src="img/01.jpg"/></li>
					<li><img src="img/02.jpg"/></li>
					<li><img src="img/03.jpg"/></li>
					<li><img src="img/04.jpg"/></li>
					<li><img src="img/05.jpg"/></li>
				</ul>
			</div>
			<div id="big">
				<img src="img/01big.jpg" class="show"/>
				<img src="img/02big.jpg"/>
				<img src="img/03big.jpg"/>
				<img src="img/04big.jpg"/>
				<img src="img/05big.jpg"/>
			</div>
		</div>
		<script type="text/javascript">
			var lis=document.getElementsByTagName("li");
			var big=document.getElementById("big");
			var imgs=big.getElementsByTagName("img");
			for(var i=0;i<lis.length;i++){
				lis[i].index=i;
				lis[i].onmouseover=function(){
					for(var j=0;j<lis.length;j++){
						lis[j].className="";
						imgs[j].className="";
					}
					this.className="light";
					imgs[this.index].className="show";
				}
			}
		</script>
	</body>
</html>
```
### 7.用户输入一个英雄名字，得到对应的外号。
```
switch(val){
	case "宋江":
		alert("及时雨——"+val);
		break;
	case "林冲":
		alert("豹子头——"+val);
		break;
	case "杨志":
		alert("青面兽——"+val);
		break;
	case "花荣":
		alert("小李广——"+val);
		break;
	default:
		alert("查无此人，请自行百度");
		reak;					
}
```
### 8.下拉菜单

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			body {
				background-image: url(img/QQ图片20190327143644.jpg);
			}			
			select {
				width: 100px;
				height: 50px;
				font-size: 24px;
				padding-left: 20px;
			}
		</style>
	</head>
	<body>
		<select id="sec">
			<option value="1">春</option>
			<option value="2">夏</option>
			<option value="3">秋</option>
			<option value="4">冬</option>
		</select>
		<script type="text/javascript">
			var sec = document.getElementById("sec");
			sec.onchange = function() {
				var val = sec.value;
				switch(val) {
					case "1":
						document.body.style.backgroundImage = "url(img/QQ图片20190327143644.jpg)";
						break;
					case "2":
						document.body.style.backgroundImage = "url(img/QQ图片20190327143652.jpg)";
						break;
					case "3":
						document.body.style.backgroundImage = "url(img/QQ图片20190327143706.jpg)";
						break;
					case "4":
						document.body.style.backgroundImage = "url(img/QQ图片20190327143659.jpg)";
						break;
				}
			}
		</script>
	</body>
</html>
```
### 9.选择排序和冒泡排序
[选择排序和冒泡排序](https://www.cnblogs.com/banana201/p/4928733.html)
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			var arr=[1,3,3,2,5,4];
			var arr1=arr;
			maopao(arr);
			console.log(arr);
			xuanze(arr1);
			console.log(arr1);			
			function maopao(arr){
				var sum=0;
				for(var i=0;i<arr.length-1;i++){
					for(var j=0;j<arr.length-1-i;j++){
						var t;
						if(arr[j]<arr[j+1]){
							t=arr[j];
							arr[j]=arr[j+1];
							arr[j+1]=t
						}
						sum++
					}
				}
				console.log(sum);
			}
			function xuanze(arr){
				var sum=0;
				for(var i=0;i<arr.length-1;i++){
					var k=i
					for(var j=i+1;j<arr.length;j++){
						if(arr[k]<arr[j]){
							k=j;
						}
						sum++;
					}
					if(i!=k){
						var t;
						t=arr[i];
						arr[i]=arr[k];
						arr[k]=t
					}
				}
				console.log(sum);
			}
		</script>
	</body>
</html>
```
### 10.今日运势
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0px;
				padding:0px;
				font-size:18px;
			}
			#container{
				width:530px;
				height:440px;
				margin:50px auto;
				border:1px solid black;	
				padding:20px;	
			}
			h2{
				color:#666;
				font-size:24px;
				margin-bottom: 20px;
			}
			#centerLeft{
				width:50px;
				height:50px;
				background:url(img/星座精灵图.png) no-repeat;
				float:left;
				margin:0px 50px;
			}
			select{
				padding-left:10px;
				width:200px;
				height:30px;
				font-size:18px;
				display: block;
				margin-bottom: 10px;
			}
			#yunshi{
				display: block;
				float:left;
			}
			#star{
				width:80px;
				height:13px;
				float:left;
				position: relative;
			}
			#lightstar{
				display:block;
				width:80px;
				height:13px;
				float:left;
				background:url(img/星星图.png) left bottom no-repeat;
				position: absolute;
				top:5px;
				left:0;
			}
			#blackstar{
				display:block;
				width:80px;
				height:13px;
				float:left;
				background:url(img/星星图.png) left top no-repeat;
				margin-top:5px;
			}			
			#clear{
				clear:both;
			}
			p{
				margin-top:20px;
				text-indent:2em;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<div id="tops">
				<h2>星座运势</h2>
			</div>
			<div id="centers">
				<div id="centerLeft"></div>
				<div id="centerRight">
					<select id="sec">
						<option value="0">白羊座03.21-04.19</option>
						<option value="1">金牛座04.20-05.20</option>
						<option value="2">双子座05.21-06.21</option>
						<option value="3">巨蟹座06.22-07.22</option>
						<option value="4">狮子座07.23-08.22</option>
						<option value="5">处女座08.23-09.22</option>
						<option value="6">天秤座09.23-10.23</option>
						<option value="7">天蝎座10.24-11.22</option>
						<option value="8">射手座 11.23-12.21</option>
						<option value="9">摩羯座12.22-01.19</option>
						<option value="10">水瓶座01.20-02.18</option>
						<option value="11">双鱼座02.19-03.20</option>
					</select>
					<span id="yunshi">今日运势：</span>
					<div id="star">
						<span id="lightstar"></span>
						<span id="blackstar"></span>
					</div>
					<div id="clear">						
					</div>
				</div>
			</div>
			<div id="bottoms">
				<p id="content">今天的事业运势不错，虽然容易有一些竞争者或其他小人出现在事业中，但他们反而会成就自己的事业。今天仍然适合外出学习进修，提升自己。</p>
			</div>
		</div>
		<script type="text/javascript">
			function $id(id){
				return document.getElementById(id);
			}
			function change(val,num,str){
				centerLeft.style.backgroundPositionY=(-val*50)+"px";
				lightstar.style.width=(num*8)+"px";
				content.innerHTML=str;
			}
			var sec=$id("sec");
			var centerLeft=$id("centerLeft");
			var lightstar=$id("lightstar");
			var content=$id("content");
			var arr=[10,9,6,8,6,8,5,2,1,3,6,1];
			var str=["今天的事业运势不错，虽然容易有一些竞争者或其他小人出现在事业中，但他们反而会成就自己的事业。今天仍然适合外出学习进修，提升自己。","外出容易遇到一些小麻烦，但终能化解，转不利为有利。","会专注于事业方面，虽然在事业工作方面，会有些迷茫，这天感情方面运势也不错。","这天巨蟹会很忙碌，但会忙得非常愉快，即使平时不太爱运动的巨蟹，这天也可能很强活动一下自己。","快乐的一天，也有迁移运势，工作和健康方面的运势也都还不错。","这天适合多听取一些朋友，对自己家庭，或者房子装修布置的建议。","有利于学习考试，与上司的沟通也会比较良好，总体比较愉快。","财运很好的一天，讲话比较严谨大气，也适合多一些娱乐活动。","不错的一天，财运仍然较好，会因为平时不太熟悉的一些晚辈帮助，或者因为娱乐活动而获利。","有朋友来帮助自己，让自己信心满满，心理层面，也是比较愉悦。","暗中会得人帮助，也容易得到亲戚，邻居的一些帮助，这天财运上也还可以。","社交运仍然强旺，内心也变得强大起来，也会因为事业方面的事情，心情愉快。"];
			sec.onchange=function(){
				var val=this.value;
				change(val,arr[val],str[val]);
			}
		</script>
	</body>
</html>
```
### 11.商品展
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#container{
				width:360px;
				height:435px;
				border:1px solid #666;
				margin:100px auto;
			}
			#big{
				width:360px;
				height:360px;
				background:url(img/01big.jpg) no-repeat;
			}
			#small li{
				list-style: none;
				float:left;
				border:1px solid #666;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<div id="big"></div>
			<div id="small">
				<ul>
					<li><img src="img/01.jpg"/></li>
					<li><img src="img/02.jpg"/></li>
					<li><img src="img/03.jpg"/></li>
					<li><img src="img/04.jpg"/></li>
					<li><img src="img/05.jpg"/></li>
				</ul>
			</div>
		</div>
		<script type="text/javascript">
			var lis=document.getElementsByTagName("li");
			var big=document.getElementById("big");
			function show(index){
				lis[index].onmouseover=function(){
					console.log(11);
					big.style.backgroundImage="url(img/0"+(index+1)+"big.jpg)";
				}
			}
			for(var i=0;i<lis.length;i++){
				show(i);
			}
		</script>
	</body>
</html>
```
### 12.带id名的getClass函数封装
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			li{
				list-style: none;
				width:100px;
				height:40px;
				display: inline-block;
				float:left;
				margin:20px;
				background-color:hotpink;
			}
		</style>
	</head>
	<body>
		<div id="topbox">
			<ul>
				<li>上1</li>
				<li class="box">上2</li>
				<li>上3</li>
				<li class="box">上4</li>
				<li>上5</li>
				<li class="box">上6</li>
				<li>上7</li>
			</ul>
		</div>
		<div id="bottombox">
			<ul>
				<li>下1</li>
				<li>下2</li>
				<li>下3</li>
				<li>下4</li>
			</ul>
		</div>
		<script type="text/javascript">
			function getClass(classname,id){
				if(document.getElementsByClassName){
					if(id){
						var id=document.getElementById(id);
						return id.getElementsByClassName(classname);
					}else{
						return document.getElementsByClassName(classname);
					}
				}
				var arr=[];
				if(id){
					var id=document.getElementById(id);
					var dom=id.getElementsByTagName("*");
				}else{
					var dom=document.getElementsByTagName("*");
				}
				for(var i=0;i<dom.length;i++){
					var newArr=dom[i].className.split(" ");
					for(var j=0;j<newArr.length;j++){
						if(newArr[j]==classname){
							arr.push(dom[i]);
						}
					}
				}
				return arr;
			}
			var boxs=getClass("box","topbox");
			for(var i=0;i<boxs.length;i++){
				boxs[i].style.backgroundColor="skyblue";
			}
		</script>
	</body>
</html>
```
### 13.通过父节点关闭广告框  
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			body{
				width:100%;
				height:100px;
				background-color:yellow;
				position: relative;
			}
			span{
				display: block;
				width:50px;
				height:50px;
				background-color:red;
				border-radius: 10px;
				position: absolute;
				top:0;
				right:0;
				text-align: center;
				line-height: 50px;
				font-size:30px;
				cursor: pointer;
			}
		</style>
	</head>
	<body>
		<span>X</span>
	</body>
	<script type="text/javascript">
		var span=document.getElementsByTagName("span")[0];
		span.onclick=function(){
			this.parentNode.style.display="none";
		}
	</script>
</html>
```
### 14.简单的评论框 
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#container{
				width:500px;
				margin:50px auto;
				border:1px solid #333;
				padding-bottom:20px;
			}
			input{
				width:400px;
				height:30px;
				font-size:20px;				
			}
			button{
				width:90px;
				height:30px;
				font-size:20px;	
			}
			li{
				list-style:none;
				font-size:16px;
				height:30px;
				line-height: 30px;
				text-indent: 2em;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<input type="text" value="请输入你的评论内容" />
			<button>发表评论</button>
			<ul>
				<li>第一个评论第一个评论第一个评论第一个评论</li>
				<li>第二个评论第二个评论第二个评论第二个评论</li>
				<li>第三个评论第三个评论第三个评论第三个评论</li>
			</ul>
		</div>
		<script type="text/javascript">
			var input1=document.getElementsByTagName("input")[0];
			var txt;
			input1.onfocus=function(){
				if(input1.value=="请输入你的评论内容"){
					input1.value="";
				}				
			}
			input1.onblur=function(){
				if(input1.value==""){
					input1.value="请输入你的评论内容";
				}
				if(input1.value!=""&&input1.value!="请输入你的评论内容"){
					txt=input1.value;
				}
			}
			
			var ul=document.getElementsByTagName("ul")[0];			
			var btn=document.getElementsByTagName("button")[0];
			btn.onclick=function(){	
				var cLi=document.createElement("li");
				cLi.innerHTML=txt;
				ul.appendChild(cLi);
			}
		</script>
	</body>
</html>
```
### 15.轮播图基础版

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#container{
				width:590px;
				height:470px;
				margin:100px auto;
				position: relative;
			}
			#box{
				width:590px;
				height:470px;
				overflow: hidden;
			}
			ul{				
				height:50px;
				list-style: none;
				position: absolute;			
				bottom:20px;
				left:50%;
				margin-left:-25%;
			}
			ul li{
				float:left;
				width:50px;
				height:50px;
				border-radius: 25px;
				background-color:hotpink;
				margin-left:5px;
				margin-right:5px;
				line-height: 50px;
				text-align: center;
				font-size:28px;	
				font-weight: 700;				
			}
			ul li:nth-child(1){
				background-color:red;
			}
			button{
				font-size:16px;
				padding:5px;
				background-color:greenyellow;
				position: absolute;
				top:50%;
				margin-top:-5%;	
			}
			#right{
				right:0;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<div id="box">
				<img src="img/1.jpg"/>
				<img src="img/2.jpg"/>
				<img src="img/3.jpg"/>
				<img src="img/4.jpg"/>
				<img src="img/5.jpg"/>
			</div>
			<ul id="uu"></ul>
			<button id="left">上一张</button>
			<button id="right">下一张</button>
		</div>
		<script type="text/javascript">
			function $id(id){
				return document.getElementById(id);
			}
			var uu=$id("uu");
			var imgs=$id("box").getElementsByTagName("img");
			for(var i=0;i<imgs.length;i++){
				var cSpan=document.createElement("span");
				cSpan.innerHTML=i+1;
				var cLi=document.createElement("li");
				cLi.appendChild(cSpan);
				uu.appendChild(cLi);				
			}
			var lis=uu.getElementsByTagName("li");
			for(var i=0;i<lis.length;i++){
				lis[i].index=i;
				lis[i].onmouseover=function(){
					for(var j=0;j<lis.length;j++){
						imgs[j].style.display="none";
						lis[j].style.backgroundColor="hotpink";
					}
					this.style.backgroundColor="red";
					imgs[this.index].style.display="block";
				}
			}
			var left=$id("left");
			var right=$id("right");
			//未完待续		
		</script>
	</body>
</html>
```

### 16.简单日历
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:500px;
				height:500px;
				margin:100px auto;
				border:2px solid peru;
				border-radius: 20px;
				box-shadow: 5px 5px 5px #999;
				overflow: hidden;
			}
			p{
				height:100px;
				width:500px;
				text-align: center;
				font-size:50px;
				color:purple;
				line-height: 100px;
				text-shadow: 5px 5px 5px #999999;
			}
			#time{
				width:500px;
				height:50px;
				background-color: skyblue;
				text-align: center;
				line-height: 50px;
				font-size:20px;
				text-shadow: 5px 5px 5px #999;
			}
			#week{
				width:500px;
				height:100px;
				background-color: honeydew;
				text-align: center;
				line-height: 100px;
				font-size:40px;
				text-shadow: 5px 5px 5px #999;
			}
			#day{
				width:500px;
				height:250px;
				background-color: gainsboro;
				text-align: center;
				line-height:250px;
				font-size:60px;
				text-shadow: 5px 5px 5px #999;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<p>金牌日历</p>
			<div id="time">
				<span></span>
			</div>
			<div id="week">
				<span></span>
			</div>
			<div id="day">
				<span></span>
			</div>
		</div>
	</body>
	<script type="text/javascript">
		var date=new Date();
		var y=date.getFullYear();
		var m=date.getMonth()+1;
		var d=date.getDate();
		var w=date.getDay();
		var arr=["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
		var spans=document.getElementsByTagName("span");
		spans[0].innerHTML=y+"年"+m+"月"+d+"日";
		spans[1].innerHTML=arr[w];
		spans[2].innerHTML=d+"号";
	</script>
</html>
```
### 17.数字时钟
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			span{
				display: block;
				width:200px;
				height:80px;
				margin:100px auto;
				border: 2px solid skyblue;
				background-color:papayawhip;
				border-radius: 10px;
				text-align: center;
				font-size:30px;
				line-height: 80px;
				letter-spacing: 5px;
				color:red;
			}
		</style>
	</head>
	<body>
		<span id="time"></span>
		<script type="text/javascript">
			var time=document.getElementById("time");
			function timeShow(){				
				var date=new Date();
				var h=date.getHours();
				var m=date.getMinutes();
				var s=date.getSeconds();
				h<10?h="0"+h:h;
				m<10?m="0"+m:m;
				s<10?s="0"+s:s;				
				time.innerHTML=h+":"+m+":"+s;
			}
			setInterval(timeShow,1000);
		</script>
	</body>
</html>
```
### 18.倒计时
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			span{
				display: block;
				width:500px;
				height:50px;
				margin:20px auto;
				border: 2px solid skyblue;
				background-color:papayawhip;
				border-radius: 10px;
				text-align: center;
				font-size:24px;
				line-height:50px;
				letter-spacing: 5px;
				color:red;
				float:left;
			}
		</style>
	</head>
	<body>
		<span>距离十月一号阅兵还有：</span>
		<span id="time"></span>
		<script type="text/javascript">
			var time=document.getElementById("time");
			function djs(){				
				var date1=new Date("2019/10/1 8:00:00");
				var date2=new Date();
				var hs=date1.getTime()-date2.getTime();
				var df=hs/(1000*60*60*24);
				var d=parseInt(df);
				var hf=(df-d)*24;
				var h=parseInt(hf);
				var mf=(hf-h)*60;
				var m=parseInt(mf);
				var sf=(mf-m)*60;
				var s=parseInt(sf);
				time.innerHTML=d+"天"+h+"小时"+m+"分"+s+"秒";
			}
			setInterval(djs,1000);			
		</script>
	</body>
</html>
```
### 19.真实时钟
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box{
				height:332px;
				width:388px;
				background: url(img/z.png);
				margin: 100px auto;
				position: relative;
			}
			span{
				height:332px;
				width:388px;
				display: block;
				position: absolute;
				top:0;
				left:0;
			}
			span:nth-child(1){				
				background: url(img/h.png) no-repeat center;
			}
			span:nth-child(2){				
				background: url(img/m.png) no-repeat center;
			}
			span:nth-child(3){				
				background: url(img/s.png) no-repeat center;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<span id="h"></span>
			<span id="m"></span>
			<span id="s"></span>
		</div>	
		<script type="text/javascript">
			function $id(id){
				return document.getElementById(id);
			}
			var h=$id("h");
			var m=$id("m");
			var s=$id("s");
			clock();
			setInterval(clock,1000);			
			function clock(){
				var date=new Date();
				var ms=date.getMilliseconds();
				var ss=date.getSeconds()+ms/1000;
				var mm=date.getMinutes()+ss/60;
				var hh=date.getHours()+mm/60;
				s.style.transform="rotate("+(ss*6)+"deg)";
				m.style.transform="rotate("+(mm*6)+"deg)";
				h.style.transform="rotate("+(hh*30)+"deg)";
			}
		</script>
	</body>
</html>
```
### 20.短信验证
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		<input type="text" />
		<button>点击发送验证码</button>
		<script type="text/javascript">
			var btn=document.getElementsByTagName("button")[0];
			btn.onclick=function(){
				var that=this;//使用that变量来存储this
				var timer=null;//声明暂时未赋值的变量，一般让它等于null
				var count=5;//点击事件内部声明，可以不用重新赋值
				clearInterval(timer);//使用定时器，上来先清除定时器
				timer=setInterval(sendMsg,1000);//使用timer来指向定时器，方便清除操作
				function sendMsg(){
					count--;
					if(count<0){
						that.innerHTML="点击重新发送";//单标签内容一般用value，双标签一般用innerHTML
						clearInterval(timer);
						that.disabled=false;//恢复按钮点击
					}else{
						that.innerHTML="倒计时还有"+count+"秒";
						that.disabled=true;//禁用按钮点击功能
					}
				}
			}
		</script>
	</body>
</html>
```
### 21.5s后关闭广告
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#ad{
				width:100%;
				height:800px;
				background-color:skyblue;
			}
		</style>
	</head>
	<body>
		<div id="ad"></div>
		<script type="text/javascript">
			var ad=document.getElementById("ad");
			var count=5;
			setInterval(close,1000);
			function close(){
				count--;
				if(count==0){
					ad.style.display="none";
				}
			}
		</script>
	</body>
</html>
```
### 22.5s页面自动跳转
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<p id="pp">5秒自动跳转至百度首页</p>
		<script type="text/javascript">
			var pp=document.getElementById("pp");
			var count=5;
			setTimeout(tioazhuan,1000);//没秒循环操作一次，达到倒计时效果
			function tioazhuan(){
				count--;
				if(count<=0){
					window.location.href="http://www.baidu.com";
				}else{
					setTimeout(tioazhuan,1000);//函数自调用——递归
					pp.innerHTML=count+"秒自动跳转至百度首页";
				}
			}
		</script>
	</body>
</html>
```
### 23.长图滚动
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box{
				width:600px;
				height: 500px;
				border: 3px solid #333;
				margin:100px auto;
				overflow: hidden;
				position: relative;
			}
			span{
				width:600px;
				height:250px;
				position: absolute;
			}
			#imgs{
				position: absolute;
			}
			#tops{
				top:0;
			}
			#bottoms{
				top:250px;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<img src="img/QQ图片20190402085835.jpg" id="imgs"/>
			<span id="tops"></span>
			<span id="bottoms"></span>
		</div>
		<script type="text/javascript">			
			var box=$id("box");
			var tops=$id("tops");
			var bottoms=$id("bottoms");
			var imgs=$id("imgs");
			var num=0;
			var timer=null;	
			mouseover(tops,upMove);
			mouseover(bottoms,downMove);
			function $id(id){
				return document.getElementById(id);
			}
			function mouseover(name,fun){
				name.onmouseover=function(){				
					timer=setInterval(fun,1);				
				}
				name.onmouseout=function(){
					clearInterval(timer);
				}
			}			
			function downMove(){					
					if(num<=0){
						clearInterval(timer);
					}else{
						num--;
						imgs.style.top=-num+"px";
					}
				}
			function upMove(){
					if(num>=(1571-500)){
						clearInterval(timer);
					}else{						
						num++;
						imgs.style.top=-num+"px";
					}
				}					
		</script>
	</body>
</html>
```
### 24.自己写的一个小练习：点击按钮出现相应盒子。
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			button{
				width:80px;
				height:40px;
				display:block;
				float:left;
			}
			#father{
				clear: both;
			}
			#father div{
				width: 78px;
				height:500px;
				border:1px solid #666;
				margin:10px 0;
				text-align: center;
				line-height: 100px;
				visibility: hidden;
				float:left;
			}
		</style>
	</head>
	<body>
		<script type="text/javascript">
			var body=document.getElementsByTagName("body")[0];			
			var colors=["red","blue","yellow","purple","LightPink","Crimson","DoderBlue","ForestGreen","DarkKhaki","BlanchedAlmond","DimGray"];
			var num=colors.length;
			for(var i=0;i<num;i++){
				var cBtn=document.createElement("button");
				cBtn.innerHTML=i+1;
				body.appendChild(cBtn);					
			}
			var fatherDiv=document.createElement("div");
			fatherDiv.setAttribute("id","father");
			body.appendChild(fatherDiv);			
			for(var i=0;i<num;i++){
				var cDiv=document.createElement("div");
				cDiv.innerHTML=i+1;
				fatherDiv.appendChild(cDiv);					
			}
			var btns=document.getElementsByTagName("button");
			var fatherDiv=document.getElementById("father");
			var dvs=fatherDiv.getElementsByTagName("div");
			for(var i=0;i<btns.length;i++){
				btns[i].index=i;
				btns[i].onclick=function(){					
					for(var j=0;j<btns.length;j++){
						btns[j].style.backgroundColor="";
						dvs[j].style.visibility="hidden";
						dvs[j].style.backgroundColor="";
					}
					this.style.backgroundColor=colors[this.index];
					dvs[this.index].style.visibility="visible";
					dvs[this.index].style.backgroundColor=colors[this.index];
				}
			}
		</script>
	</body>
</html>
```
### 25.获取字符串长度方法封装
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			var str="i am strong not 虚胖";
			function getStringLength(str){
				var sum=0;
				var code=0;
				for(var i=0;i<str.length;i++){
					code=str.charCodeAt(i);
					if(code>=0&&code<=127){
						sum++;
					}else{
						sum+=2;
					}
				}
				return sum;
			}
			var length=getStringLength(str);
			console.log(length);
		</script>
	</body>
</html>
```
### 26.查找字符位置
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		请输入字符串：<input type="text" id="txt1"/><br />
		请输入要查找的字符：<input type="text" id="txt2"/><br />
		<button id="btn1">从前面查找</button>
		<button id="btn2">从后面查找</button>
		<script type="text/javascript">
			function $id(id){return document.getElementById(id)}
			$id("btn1").onclick=function(){
				alert("从前面查找，下标是："+($id("txt1").value).indexOf($id("txt2").value));
			}
			$id("btn2").onclick=function(){
				alert("从后面查找，下标是："+($id("txt1").value).lastIndexOf($id("txt2").value));
			}
		</script>
	</body>
</html>
```
### 27.网址编码解码
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			var str="https://hao.360.cn/?a1004";
			var bstr=encodeURIComponent(str);
			console.log(bstr);// https%3A%2F%2Fhao.360.cn%2F%3Fa1004
			var jstr=decodeURIComponent(bstr);
			console.log(jstr);// https://hao.360.cn/?a1004
		</script>
	</body>
</html>
```
### 28.三种保留两位小数的方式
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			var num=12342342345.6788656;
			two(num);
			two1(num);
			two2(num);
			function two(num){
				var str=num.toString();
				var end=str.indexOf(".")+3;
				var strNew=str.substr(0,end);
				var numNew=Number(strNew);
				console.log(numNew);
			}
			function two1(num){
				var num1=parseInt(num*100);
				var num2=num1/100;
				console.log(num2);
			}
			function two2(num){
				var str=num.toFixed(2);
				var num1=Number(str);
				console.log(num1);//具有四舍五入功能
			}
		</script>
	</body>
</html>
```
### 29.案例：判断上传文件类型
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<input type="file" id="files"/>
		<p id="pp"></p>
		<script type="text/javascript">
			var pp=document.getElementById("pp");
			var files=document.getElementById("files");
			files.onchange=function(){
				var filePath=this.value;
				var houzhui=filePath.substr(filePath.lastIndexOf(".")).toLocaleLowerCase();
				if(houzhui == ".jpg" || houzhui ==".png" || houzhui==".gif" ){
					pp.innerHTML="图片格式正确";
				}else{
					pp.innerHTML="图片格式不正确";
				}
			}
		</script>
	</body>
</html>
```
### 30.获取元素方式的封装
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			div{
				width:100px;
				height:100px;
			}
		</style>
	</head>
	<body>
		<div id="dv"></div>
		<div class="dv"></div>
		<div></div>
		<script type="text/javascript">
			function $(str){
				var firstLetter=str.charAt(0);
				var secound=str.substr(1);
				switch(firstLetter){
					case "#": 
						return document.getElementById(secound);
					case ".":
						return document.getElementsByClassName(secound);
					default:
						return document.getElementsByTagName(str);
				}
			}
			/*$("#dv").style.backgroundColor="red";
			$(".dv")[0].style.backgroundColor="yellow";
			$("div")[0].style.border="2px solid green";
			$("div")[1].style.border="2px solid green";
			$("div")[2].style.border="2px solid green";*/
			document.querySelector("#dv").style.backgroundColor="red";
			document.querySelector(".dv").style.backgroundColor="yellow";
			document.querySelector("div").style.border="2px solid green";
			document.querySelectorAll("div")[1].style.border="2px solid green";
			document.querySelectorAll("div")[2].style.border="2px solid green";
		</script>
	</body>
</html>
```
### 31.无缝滚动图
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:600px;
				height:238px;
				border:2px solid #333;
				position: relative;
				margin:100px auto;
				overflow: hidden;
			}
			#box ul{				
				position: absolute;
				left:0;
				width:1800px;
			}
			#box li{
				list-style: none;
				float: left;				
			}
			#box li img{
				vertical-align: top;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<ul>
				<li><img src="img/1.jpg"/></li>
				<li><img src="img/2.jpg"/></li>
				<li><img src="img/3.jpg"/></li>
				<li><img src="img/4.jpg"/></li>
				<li><img src="img/1.jpg"/></li>
				<li><img src="img/2.jpg"/></li>
			</ul>
		</div>
		<script type="text/javascript">
			var uu=document.querySelector("ul");
			var num=0;
			var timer=null;
			timer=setInterval(scrool,20);
			function scrool(){
				num++;
				num<1200?uu.style.left=-num+"px":num=0;
			}
			uu.onmouseover=function(){
				clearInterval(timer);
			}
			uu.onmouseout=function(){
				timer=setInterval(scrool,20);
			}
		</script>
	</body>
</html>
```
### 32.匀速运动的盒子
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			button{
				width:80px;
				height:40px;
				border-radius: 5px;
				background-color:deepskyblue;
				margin:5px;
			}
			#father{
				width:500px;
				height:500px;
				margin:10px;
				position: relative;
				border:2px solid red;
			}
			#son{
				width:100px;
				height:100px;
				background-color:yellow;
				position: absolute;
				top:0px;
				left:0;
			}
		</style>
	</head>
	<body>
		<button>开始</button>
		<button>暂停</button>
		<div id="father">
			<div id="son"></div>
		</div>
		<script type="text/javascript">
			var box=document.querySelector("#son");
			var btn1=document.querySelectorAll("button")[0];
			var btn2=document.querySelectorAll("button")[1];			
			var timer=null;
			var num=0;
			btn1.onclick=function(){				
				timer=setInterval(move,20);
			}
			btn2.onclick=function(){				
				clearInterval(timer);
			}			
			function move(){
				if(num>=400){
					clearInterval(timer);
				}else{
					num++;
					box.style.top=num+"px";
					box.style.left=num+"px";
				}				
			}
		</script>
	</body>
</html>
```
### 33.加速运动的盒子
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			div{
				width:100px;
				height:100px;
				background-color:yellow;
				position: relative;
				left:0;
			}
		</style>
	</head>
	<body>
		<button>Move</button>
		<div id="box"></div>
		<script type="text/javascript">
			var dv=document.querySelector("div");
			var btn=document.querySelector("button");
			var leader=0;
			var target=1000;
			btn.onclick=function(){
				setInterval(move,30);
			}
			function move(){
				leader=leader+(target-leader)/10;
				dv.style.left=leader+"px";
			}			
		</script>
	</body>
</html>
```
### 34.重写轮播图
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:300px;
				height:238px;
				margin:auto;
				border:2px solid #333;
				position: relative;
				overflow: hidden;
			}
			#box ul{
				list-style: none;
				width:1500px;
				position: absolute;
				left:0;
			}
			#box ul li{
				float: left;
			}
			#box ul li img{
				vertical-align: top;
			}
			#fatherBox{
				width:500px;
				height:300px;
				margin:100px auto;
				position: relative;
			}
			button{
				width:80px;
				height:40px;
				background-color:lightskyblue;
				color:yellow;
				font-size:20px;
				font-weight: 700;
				position: absolute;
				top:90px;
			}
			button:nth-child(1){
				left: 20px;
			}
			button:nth-child(2){
				right: 20px;
			}
		</style>
	</head>
	<body>
		<div id="fatherBox">
			<button>上一张</button>
			<button>下一张</button>
			<div id="box">			
				<ul>
					<li><img src="img/1.jpg"/></li>
					<li><img src="img/2.jpg"/></li>
					<li><img src="img/3.jpg"/></li>
					<li><img src="img/4.jpg"/></li>
				</ul>
			</div>
		</div>		
		<script type="text/javascript">
			var btns=document.querySelectorAll("button");
			var uu=document.querySelector("ul");
			var num=0;
			btns[0].onclick=function(){
				if(num==900){
					num=0;
					uu.style.left="0px";
				}else{
					num+=300;
					uu.style.left=-num+"px";
				}				
			}
			btns[1].onclick=function(){
				if(num==0){
					num=900;
					uu.style.left="-900px";
				}else{
					num-=300;
					uu.style.left=-num+"px";
				}				
			}
		</script>
	</body>
</html>
```
### 35.缓动盒子
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			div{
				width:100px;
				height:100px;
				background-color: yellow;
				position: relative;
			}
		</style>
	</head>
	<body>
		<button>开始移动</button>
		<div id="box"></div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			var btn=document.querySelector("button");
			var leader=0;
			var target=500;
			btn.onclick=function(){
				setInterval(function(){
					leader=leader+(target-leader)/20;
					box.style.left=leader+"px";
				},20);
			}			
		</script>
	</body>
</html>
```
### 36.焦点轮播图案例
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			img{
				vertical-align: top;
			}
			#box{
				width:590px;
				height:470px;
				margin:100px auto;
				border: 2px solid #333;				
				padding:10px;
				position: relative;
			}
			#content{
				width:100%;
				height:100%;
				overflow: hidden;
			}
			ul,ol{
				list-style: none;
			}
			ul{
				width:1000%;
				position: relative;
			}
			ul li{
				float:left;
			}
			ol{
				position: absolute;
				left:50%;
				bottom:15px;
			}
			ol li{
				width:40px;
				height:40px;
				background-color: white;
				text-align: center;
				line-height: 40px;
				border-radius: 20px;
				border:1px solid #333;
				float: left;
				margin-right:5px;
			}
			.bgc{
				background-color: yellow;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<div id="content">
				<ul>
					<li><img src="img/1.jpg"/></li>
					<li><img src="img/2.jpg"/></li>
					<li><img src="img/3.jpg"/></li>
					<li><img src="img/4.jpg"/></li>
				</ul>
			</div>
			<ol>
				<li class="bgc">1</li>
				<li>2</li>
				<li>3</li>
				<li>4</li>
			</ol>
		</div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			var uu=box.children[0].children[0];
			var oo=box.children[1];
			var lis=oo.children;
			for(var i=0;i<lis.length;i++){
				lis[i].index=i;
				lis[i].onmouseover=function(){					
					for(var j=0;j<lis.length;j++){
						lis[j].className="";
					}
					this.className="bgc";
					target=-590*(this.index);
				}				
			}
			var leader=0;
			var target=0;
			setInterval(function(){
				leader=leader+(target-leader)/20;
				uu.style.left=leader+"px";
			},20);
		</script>
	</body>
</html>
```
### 37.点击切换案例
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:590px;
				height:470px;
				margin:100px auto;
				border: 2px solid #333;				
				padding:10px;
				position: relative;
			}
			#content{
				width:100%;
				height:100%;
				overflow: hidden;
			}			
			ul{
				width:1000%;
				position: relative;
				list-style: none;
			}
			ul li{
				float:left;
			}
			ol{
				position: absolute;
				right:10%;
				bottom:15px;
				list-style: none;
			}
			ol li{
				width:40px;
				height:40px;
				background-color: white;
				text-align: center;
				line-height: 40px;
				border-radius: 20px;
				border:1px solid #333;
				float: left;
				margin-right:5px;
			}
			.bgc{
				background-color: yellow;
			}
			button{
				position: absolute;
				top:0;
				background-color:#666;
				opacity: .4;
				color:#ccc;
				height:80px;
				width:40px;
				font-size:30px;
				top:50%;
				margin-top:-40px;
				display: none;
			}
			#left{
				left:20px;
			}
			#right{
				right: 20px;
			}
		</style>
	</head>
	<body>		
		<div id="box">			
			<div id="content">
				<ul></ul><!--存放照片-->
			</div>
			<ol></ol><!--存放小圆点-->
			<button id="left"><</button>
		    <button id="right">></button>
		</div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			var uu=box.children[0].children[0];
			var oo=box.children[1];			
			var arr=["img/1.jpg","img/2.jpg","img/3.jpg","img/4.jpg"];
			for(var i=0;i<arr.length;i++){//创建ul中的li及图片列表
				var cImg=document.createElement("img");
				cImg.src=arr[i];
				var cLi=document.createElement("li");
				cLi.appendChild(cImg);
				uu.appendChild(cLi);
			}
			var uulis=uu.children;
			for(var i=0;i<uulis.length;i++){//创建ol中的小圆点列表
				var cLi=document.createElement("li");
				cLi.innerHTML=i+1;
				oo.appendChild(cLi);				
			}			
			var lis=oo.children;
			lis[0].className="bgc";			
			var left=document.getElementById("left");
			var right=document.getElementById("right");	
			box.onmouseover=function(){//鼠标经过，显示按钮
				left.style.display="block";
				right.style.display="block";
			}
			box.onmouseout=function(){//鼠标离开隐藏按钮
				left.style.display="none";
				right.style.display="none";
			}
			left.onclick=function(){//左边鼠标点击右移动							
				target+=590;
				var i=-target/590;
				if(i<=0){
					i=0;
				}
				for(var j=0;j<lis.length;j++){
					lis[j].className="";
				}
				lis[i].className="bgc";	
			}
			right.onclick=function(){//右边鼠标点击左移动				
				target-=590;
				var i=-target/590;
				if(i>=3){
					i=3;
				}
				for(var j=0;j<lis.length;j++){
					lis[j].className="";
				}
				lis[i].className="bgc";	
			}
			for(var i=0;i<lis.length;i++){
				lis[i].index=i;
				lis[i].onmouseover=function(){//鼠标经过小圆点，图片移动到对应的那张					
					for(var j=0;j<lis.length;j++){
						lis[j].className="";
					}
					this.className="bgc";
					target=-590*(this.index);
				}				
			}
			var leader=0;
			var target=0;
			setInterval(function(){//定时器，实现动态移动效果
				leader=leader+(target-leader)/20;
				if(target>=0){
					target=0;
				}else if(target<=-(590*3)){
					target=-(590*3);
				}
				uu.style.left=leader+"px";				
			},20);				
		</script>
	</body>
</html>
```
### 38.使用鼠标跟随写的导航栏
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			body{
				background-color: #CCCCCC;
			}
			#box{
				width:500px;
				height:50px;
				border:1px #333 solid;
				margin:50px auto;
				background-color: white;
				position: relative;
			}
			ul{
				list-style: none;
				position: absolute;
			}
			ul li{
				float: left;
				width:100px;
				height: 50px;
				text-align: center;
				line-height: 50px;	
			}
			span{
				display: inline-block;
				background: url(img/5.png) no-repeat;
				width:100px;
				height:50px;
				position: absolute;
				left: 0;
			}
		</style>
	</head>
	<body>
		<div id="box">	
			<span></span>
			<ul>				
				<li>首页</li>
				<li>首页</li>
				<li>首页</li>
				<li>首页</li>
				<li>首页</li>
			</ul>				
		</div>
		<script type="text/javascript">
			var lis=document.getElementsByTagName("li");
			var span=document.getElementsByTagName("span")[0];
			var flag=0;
			for(var i=0;i<lis.length;i++){
				lis[i].onmouseover=function(){
					target=this.offsetLeft;
				}
				lis[i].onmouseout=function(){
					target=flag;
				}
				lis[i].onclick=function(){
					flag=this.offsetLeft;
				}
			}
			var leader=0;
			var target=0;
			setInterval(function(){
				leader=leader+(target-leader)/10;
				span.style.left=leader+"px";
			},20);
		</script>
	</body>
</html>
```
### 39.移动的猴子
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:100px;
				height:100px;
				position: relative;
			}
			img{
				width:100px;
				height:100px;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<img src="img/猴子.gif"/>
		</div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			document.onmousemove=function(event){
				var event = event||document.event;
				targetX=event.clientX-box.offsetWidth/2;
				targetY=event.clientY-box.offsetWidth/2;
			}
			var leaderX=0,leaderY=0,targetX=0,targetY=0;
			setInterval(function(){
				leaderX=leaderX+(targetX-leaderX)/10;
				leaderY=leaderY+(targetY-leaderY)/10;
				box.style.left=leaderX+"px";
				box.style.top=leaderY+"px";
			},20);
		</script>
	</body>
</html>
```


### 40.获取容器的坐标
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box{
				width:400px;
				height: 400px;
				border:solid 1px #333;
				margin: 100px auto;
			}
		</style>
	</head>
	<body>
		<div id="box"></div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			box.onmousemove=function(event){
				var event=event||document.event;
				var x=event.clientX-box.offsetLeft;
				var y=event.clientY-box.offsetTop;
				box.innerHTML="x坐标为："+x+"，y坐标为："+y+"。"
			}
		</script>
	</body>
</html>
```
### 41.放大镜

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:400px;
				height:400px;
				margin:50px;
				border:1px solid #333;
				position: relative;
			}
			.small{
				width:400px;
				height:400px;
			}
			.zhe{
				width:150px;
				height:150px;
				background-color: yellow;
				opacity: .3;
				position: absolute;
				left:0;
				top:0;
				display: none;
				cursor: move;
			}
			.big{
				width:600px;
				height:600px;
				position: absolute;
				left:430px;
				top:0;
				border:1px solid red;
				display: none;
				overflow: hidden;
			}
			img{
				vertical-align: top;
			}
			.big img{
				position: absolute;
				left:0;
				top:0;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<div class="small">
				<div class="zhe"></div>
				<img src="img/QQ图片20190408112203.jpg"/>
			</div>
			<div class="big">
				<img src="img/QQ图片20190408112209.jpg"/>
			</div>
		</div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			var small=box.children[0];
			var zhe=small.children[0];
			var big=box.children[1];
			var bigImg=big.children[0];
			small.onmouseover=function(){
				zhe.style.display="block";
				big.style.display="block";
			}
			small.onmouseout=function(){
				zhe.style.display="none";
				big.style.display="none";
			}
			small.onmousemove=function(event){
				var event=event||document.event;
				shuBiaoX=event.clientX-box.offsetLeft;
				shuBiaoY=event.clientY-box.offsetTop;
				zheX=shuBiaoX-zhe.offsetWidth/2;
				zheY=shuBiaoY-zhe.offsetHeight/2;
				if(zheX<=0){
					zheX=0;
				}else if(zheX>=small.offsetWidth-zhe.offsetWidth){
					zheX=small.offsetWidth-zhe.offsetWidth;
				}
				if(zheY<=0){
					zheY=0;
				}else if(zheY>=small.offsetHeight-zhe.offsetHeight){
					zheY=small.offsetHeight-zhe.offsetHeight;
				}
				imgX=(big.offsetWidth-bigImg.offsetWidth)/(small.offsetWidth-zhe.offsetWidth)*zheX;
				imgY=(big.offsetHeight-bigImg.offsetHeight)/(small.offsetHeight-zhe.offsetHeight)*zheY;
				zhe.style.left=zheX+"px";
				zhe.style.top=zheY+"px";
				bigImg.style.left=imgX+"px";
				bigImg.style.top=imgY+"px";
			}
		</script>
	</body>
</html>
```
#### 在自己框内放大
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:400px;
				height:400px;
				margin:100px auto;
				border:1px solid #333;
				position: relative;
			}
			.small{
				width:400px;
				height:400px;
			}
			.small img{
				width:400px;
				height:400px;
			}			
			.big{
				width:400px;
				height:400px;
				position: absolute;
				left:0px;
				top:0;
				display: none;
				overflow: hidden;
			}
			img{
				vertical-align: top;
			}
			.big img{
				position: absolute;
				left:0;
				top:0;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<div class="small">
				<img src="img/1.jpg"/>
			</div>
			<div class="big">
				<img src="img/1.jpg"/>
			</div>
		</div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			var small=box.children[0];			
			var big=box.children[1];
			var bigImg=big.children[0];
			box.onmouseover=function(){
				big.style.display="block";
			}
			box.onmouseout=function(){
				big.style.display="none";
			}
			big.onmousemove=function(event){
				var event=event||document.event;
				var X=event.clientX-box.offsetLeft;
				var Y=event.clientY-box.offsetTop;				
				if(X<=0){
					X=0;
				}else if(X>=box.offsetWidth){
					X=box.offsetWidth;
				}
				if(Y<=0){
					Y=0;
				}else if(Y>=box.offsetHeight){
					Y=box.offsetHeight;
				}
				imgX=(box.offsetWidth-bigImg.offsetWidth)/(box.offsetWidth)*X;
				imgY=(box.offsetHeight-bigImg.offsetHeight)/(box.offsetHeight)*Y;				
				bigImg.style.left=imgX+"px";
				bigImg.style.top=imgY+"px";
			}
		</script>
	</body>
</html>
```
### 42.拖拽进度条
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box{
				height: 30px;
				width:500px;
				margin:100px;
				background-color:#ccc;
				position: relative;
			}
			.bar{
				display: inline-block;
				height:50px;
				width:10px;
				background-color:blue;
				position: absolute;
				top:-10px;
				left:0;
			}
			.content{
				display: inline-block;
				height:100px;
				width:480px;
				background-color:yellow;
				position: absolute;
				top:100px;
				left:0;
				font-size:20px;
				line-height: 100px;
				padding-left:20px;
			}
			.bgc{
				display: inline-block;
				width:0px;
				height:30px;
				background-color:blue;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<span class="bar"></span>
			<span class="bgc"></span>
			<span class="content">当前进度为：0%。</span>
		</div>
		<script type="text/javascript">
			var box=document.getElementById("box");
			var bar=document.querySelector(".bar");
			var bgc=document.querySelector(".bgc");
			var content=document.querySelector(".content");
			bar.onmousedown=function(){
				document.onmousemove=function(event){
					var event=event||document.event;
					var shubiaoX=event.clientX-box.offsetLeft;
					if(shubiaoX<0){
						shubiaoX=0;
					}else if(shubiaoX>box.offsetWidth-bar.offsetWidth){
						shubiaoX=box.offsetWidth-bar.offsetWidth;
					}
					bar.style.left=shubiaoX+"px";
					bgc.style.width=bar.style.left;
					var num=parseInt(shubiaoX/(box.offsetWidth-bar.offsetWidth)*100);
					content.innerHTML="当前进度为："+num+"%。"
					window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
				}
				document.onmouseup=function(){
					document.onmousemove=null;
				}
			}
			
			
		</script>
	</body>
</html>
```

### 43.模态框案例
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			.login{
				width:100%;
				height:50px;
				background-color:brown;
			}
			a{
				text-decoration: none;
				font-size:20px;
				color:white;
				line-height: 50px;
				margin-left:20px;
			}
			#box{
				width:500px;
				height:400px;
				position: absolute;
				left:50%;
				top:50%;
				margin-left:-250px;
				margin-top:-200px;
				background-color:#CCCCCC ;
				display: none;
			}
			.drag{
				width: 500px;
				height:50px;
				background-color: purple;
				color:white;
				font-size:20px;
				line-height: 50px;
				text-align: center;
				cursor: move;
			}
			span{
				display: block;
				width:40px;
				height:40px;
				border-radius: 5px;
				background-color:yellow ;
				color:red;
				font-size:24px;
				font-weight:700;
				text-align: center;
				line-height: 40px;
				float:right;
				cursor: pointer;
			}
		</style>
	</head>
	<body>
		<div class="login">
			<a href="javascript:;">注册登录</a>
		</div>
		<div id="box">
			<div class="drag">登录注册</div>
			<span class="close">X</span>
		</div>
		<script type="text/javascript">
			var login=document.querySelector("a");
			var box=document.getElementById("box");
			var close=document.querySelector("span");
			var drag=document.getElementsByClassName("drag")[0];
			login.onclick=function(){
				box.style.display="block";
			}
			close.onclick=function(){
				box.style.display="none";
			}
			drag.onmousedown=function(event){
				var event=event||document.event;
				var currentX=event.clientX-box.offsetLeft;//记录当前坐标
				var currentY=event.clientY-box.offsetTop;
				document.onmousemove=function(event){
					var event=event||document.event;
					var nowX=event.clientX-currentX+250;//调用前面记录的坐标
					var nowY=event.clientY-currentY+200;
					box.style.left=nowX+"px";
					box.style.top=nowY+"px";
					window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
				}
				document.onmouseup=function(){
					document.onmousemove=null;
				}
			}
			
		</script>
	</body>
</html>
```

### 44.Scroll封装
```
function scroll(){
	if(document.documentElement){
		return {
			top: document.documentElement.scrollTop,
			left: document.documentElement.scrollLeft
		}
	}else if(document.body){
		return {
			top: document.body.scrollTop,
			left: document.body.scrollLeft
		}
	}else if(window.pageXOffset){
		return {
			top: window.pageYOffset,
			left: window.pageXOffset
		}
	}
}
```

### 45.导航栏吸顶效果
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			.head{
				width:100%;
				height:200px;
				background-color: yellow;
			}
			.nav{
				width: 100%;
				height:80px;
				background-color:black;
			}
			.fixed{
				position: fixed;
				left:0;
				top:0;
			}
			.content{
				width:100%;
				height:10000px;
				background-color:#ccc;
			}
		</style>
	</head>
	<body>
		<div class="head"></div>
		<nav class="nav"></nav>
		<div class="content"></div>
	</body>
	<script src="js/scroll.js"></script>
	<script type="text/javascript">
		var headH=document.getElementsByClassName("head")[0].offsetHeight;
		var nav=document.getElementsByTagName("nav")[0];
		window.onscroll=function(){
			if(scroll().top>=headH){
				nav.className="nav fixed";
			}else{
				nav.className="nav";
			}
		}
	</script>
</html>
```
### 46.图片跟随
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			body{
				width:100%;
				height:10000px;
			}
			img{
				display: block;
				position: absolute;
				left: 0;
				top:300px
			}
		</style>
	</head>
	<body>
		<img src="img/QQ图片20190409143138.gif"/>
	</body>
	<script src="js/scroll.js"></script>
	<script type="text/javascript">
		var img=document.querySelector("img");
		var leader=0,target=0,timer=null;
		window.onscroll=function(){
			target=scroll().top+300;
			timer=setInterval(function(){				
				leader=leader+(target-leader)/10;
				img.style.top=leader+"px";
			},20);
		}
	</script>
</html>
```
### 47.回到顶部
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			body{
				height:10000px;
			}
			div{
				width:500px;
				height:5000px;
				background-color: red;
			}
			span{
				display: inline-block;
				width:80px;
				height:80px;
				border-radius: 8px;
				background-color: yellow;
				font-size:20px;
				line-height: 80px;
				text-align: center;
				position: fixed;
				right:20px;
				bottom:20px;
				display: none;
			}
			span:hover{
				background-color:black;
				color:white;
			}
		</style>
	</head>
	<body>
		<div></div>
		<span id="span">
			TOP
		</span>
	</body>
	<script src="js/scroll.js"></script>
	<script type="text/javascript">
		var span=document.getElementById("span");
		var leader=0,target=0,timer=null;
		window.onscroll=function(){
			if(scroll().top>0){
				span.style.display="block";
			}else{
				span.style.display="none";
			}
			leader=scroll().top;
			span.onclick=function(){
				timer=setInterval(function(){
					leader=leader+(target-leader)/20;
					if(leader<300){
						leader-=10;
					}
					console.log(leader)
					window.scrollTo(0,leader);
					if(leader<=0){
						leader=0;
						clearInterval(timer);
					}
				},30);				
			}
		}
	</script>
</html>
```
### 48.获取屏幕尺寸
```
function client(){
    if(window.innerWidth !=null){
        return {
            height:window.innerHeight,
            width:window.innerWidth
        }
    }else if(document.compatMode=="CSS1Compat"){
         return {
           height:document.documentElement.clientHeight,
            width:document.documentElement.clientWidth
        }
    }else{
        return {
           height:document.body.clientHeight,
            width:document.body.clientWidth
        }
    }
}
```
### 49.窗口自适应
- 当窗口宽度大于960px时，页面背景为黄色；大于640px时背景蓝色；其余为黑色。
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
	</body>
	<script src="js/scroll.js"></script>
	<script type="text/javascript">
		fun();
		window.onresize=fun;		
		function fun(){
			if(client().width>960){
				document.body.style.backgroundColor="yellow";
			}else if(client().width>640){
				document.body.style.backgroundColor="blue";
			}else{
				document.body.style.backgroundColor="black";
			}
		}
	</script>
</html>
```
### 50.forEach
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		<a href="javascript:;">点击</a>
		<a href="javascript:;">点击</a>
		<a href="javascript:;">点击</a>
		<a href="javascript:;">点击</a>
		<a href="javascript:;">点击</a>
		<a href="javascript:;">点击</a>
		<a href="javascript:;">点击</a>
	</body>
	<script type="text/javascript">
		var arr=[1,2,true,"字符串",2,2,3];
		arr.forEach(function(v,i){
			console.log(`下标${i}的值为:${v}`)
		});
		var allA=document.querySelectorAll("a");
		allA.forEach(function(v,i){
			v.onclick=function(){
				console.log(1);
			}
		});
	</script>
</html>
```

### 51.阻止事件冒泡

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			div{
				width:400px;
				height:400px;
				background-color:yellow;
				display: none;
			}
		</style>
	</head>
	<body>
		<button>点击显示</button>
		<div id="box">
			
		</div>
	</body>
	<script type="text/javascript">
		var btn=document.querySelector("button");
		var box=document.getElementById("box");
		btn.onclick=function(){
			event.stopPropagation();
			box.style.display="block";
		}
		document.onclick=function(){
			box.style.display="none";
		}
	</script>
</html>

```

### 52.阻止冒泡兼容写法

```
btn.onclick=function(event){
	var event=event||window.event;
	if(event.stopPropagation){
		event.stopPropagation();
	}else{
		event.cancelBubble=true;
	}
	box.style.display="block";
}
```
### 53.弹框和取消弹框

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{margin:0;padding:0;}
			body{
				height:2000px;
			}
			a{
				display: inline-block;
				width:80px;
				height:40px;
				background-color: skyblue;
				border-radius: 5px;
				font-size:16px;
				line-height: 40px;
				text-align: center;
				margin:20px;
				color:red;
			}
			#content{
				width:100%;
				height:100%;
				background-color:yellow;
				opacity: .3;
				position: fixed;
				top:0;
				left:0;
				display: none;
			}
			#login{
				width:400px;
				height:400px;
				background-color: white;
				position: fixed;
				top:50%;
				left:50%;
				margin-top:-200px;
				margin-left:-200px;
				display: none;
			}
		</style>
	</head>
	<body>
		<a href="javascript:;">点击登录</a>
		<div id="content"></div>
		<div id="login"></div>
	</body>
	<script type="text/javascript">
		var regiset=document.querySelector("a");
		var content=document.getElementById("content");
		var login=document.getElementById("login");
		regiset.onclick=function(event){
			var event=event||window.event;
			if(event.stopPropagation){
				event.stopPropagation();
			}else{
				event.cancelBubble=true;
			}
			content.style.display="block";
			login.style.display="block";
		}
		document.onclick=function(event){
			var event=event||window.event;
			var targetId=event.target.id||event.srcElement.id;
			if(targetId!="login"){
				content.style.display="none";
				login.style.display="none";
			}			
		}
	</script>
</html>

```
### 54.文字选择
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#content{
				width:400px;
				font-size:20px;
				line-height: 1.5em;
				margin:20px;
			}
			#box{
				width: 150px;
				height:auto;
				background-color: yellow;
				opacity: .7;
				color:red;
				padding:5px;
				text-align: justify;
				display: none;
				position: absolute;
				left:0;
				top:0;
			}
		</style>
	</head>
	<body>
		<div id="content">
			一张习近平总书记参加首都义务植树的照片点燃朋友圈。照片中，总书记扛着铁锹，正走向植树地点。网友们直呼：“真接地气”“这是真干过活的”……细心的网友发现，习近平总书记面带微笑、扛着铁锹的形象同30年前一幅老照片十分相像。那是1989年，时任宁德地委书记的习近平带领地直机关干部参加义务劳动，他一把锄头扛在肩上，意气风发，大步走在田埂上。
		</div>
		<div id="box"></div>
	</body>
	<script type="text/javascript">
		var content=document.getElementById("content");
		var box=document.getElementById("box");
		var txt;
		content.onmouseup=function(event){
			var event=event||window.event;
			
			if(window.getSelection){
				txt=window.getSelection().toString();
			}else{
				txt=document.selection.createRange().text;
			}
			setTimeout(function(){
				if(txt){
					var x=event.clientX+5;
					var y=event.clientY+5;
					box.style.display="block";
					box.style.left=x+"px";
					box.style.top=y+"px";
					box.innerHTML=txt;
				}				
			},400);	
		}
		document.onclick=function(event){
			var event=event||window.event;
			var targetId=event.target.id||event.srcElement.id;
			if(targetId!="content"){
				box.style.display="none";
			}			
		}
	</script>
</html>
```
### 55.最简单的运动框架
```
//使一个元素运动，num是步长，target是目标位置。(num:Number,target:Number)
function move(num,target){
	var timer=null;
	timer=setInterval(function(){
		box.style.left=box.offsetLeft+num+"px";
		if(box.offsetLeft>=target){
			console.log(box.offsetLeft);
			clearInterval(timer);
		}
	},20);	
}
```
### 56、forEach使用
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{margin:0;padding:0;}
			li{
				list-style: none;
				width:100px;
				height:100px;
				background-color: skyblue;
				margin:10px;
				float:left;
			}
			.bgc{
				background-color:red;
			}
		</style>
	</head>
	<body>
		<ul>
			<li class="bgc"></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
		</ul>
	</body>
	<script type="text/javascript">
		var lis=document.querySelectorAll("li");
		lis.forEach(function(v,i){							
			v.onclick=function(){
				lis.forEach(function(v){
					v.className="";
				});	
				this.className="bgc";
			}
		});
	</script>
</html>
```

### 57.使用sort方法进行数组排序

```
<script type="text/javascript">
	var arr=[1,2,3,2,1,4,55,2,111,42,2];
	var newArr=arr.sort(function(a,b){
		return a-b;//升序排列，需要降序排列，返回b-a就行了
	});
	newArr.forEach(function(v,i){
		console.log(`下标${i}的值为${v}`);
	})
</script>
```

### 58.点击按钮，出现对应下标，三种解决办法
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<button>按钮1</button>
		<button>按钮2</button>
		<button>按钮3</button>
		<button>按钮4</button>
		<button>按钮5</button>
		<button>按钮6</button>
		<button>按钮7</button>
	</body>
	<script type="text/javascript">
		var btns=document.getElementsByTagName("button");
		//第一种实现办法
		for(var i=0;i<btns.length;i++){
			btns[i].index=i;
			btns[i].onclick=function(){
				alert(this.index+1);
			}
		}
		//第二种实现办法
		for(var i=0;i<btns.length;i++){
			(function(i){
				btns[i].onclick=function(){
					alert(i+1);
				}
			})(i)
		}
		//第三种实现办法
		for(let i=0;i<btns.length;i++){
			btns[i].onclick=function(){
				alert(i+1);
			}
		}		
	</script>
</html>
```
### 59.简单的运动框架
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box {
				height: 150px;
				width: 150px;
				background-color: yellow;
				position: absolute;
			}
		</style>
	</head>
	<body>
		<button id="btn1">点击运动到300</button>
		<button id="btn2">点击运动到600</button>
		<button id="btn3">回到原点</button>
		<div id="box"></div>
	</body>
	<script src="js/move.js"></script>
	<script type="text/javascript">
		const btn1 = $id("btn1");
		const btn2 = $id("btn2");
		const btn3 = $id("btn3");
		const box = $id("box");
		btn1.onclick = function() {
			animate(box, 300);
		}
		btn2.onclick = function() {
			animate(box, 600);
		}
		btn3.onclick = function() {
			animate(box, 0);
		}		
	</script>
</html>
//move.js文件
function $id(id) {
	return document.getElementById(id);
}
function animate(obj, target) {
	clearInterval(obj.timer);
	let buchang = target > obj.offsetLeft ? 5 : -5;
	obj.timer = setInterval(function() {
		obj.style.left = obj.offsetLeft + buchang + "px";
		if(Math.abs(target - obj.offsetLeft) <= Math.abs(buchang)) {
			clearInterval(obj.timer);
			obj.style.left = target + "px";
		}
	}, 30);
}
```

### 60.轮播图
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding:0;
			}
			#box{
				width:590px;
				height:470px;
				border:5px solid #333;
				margin:100px auto;
				position: relative;
			}
			#content{
				width:590px;
				height:470px;
				overflow: hidden;
			}
			ul,ol{
				list-style: none;
			}
			ul{
				width:1000%;
				position: relative;
			}
			ul li{
				float:left;
			}
			ol{
				position: absolute;
				bottom:10px;
				right:20px;
			}
			ol li{
				width:50px;
				height:50px;
				background-color:white;
				margin-right: 5px;
				border-radius: 50%;
				float: left;
				text-align: center;
				line-height: 50px;
				font-size: 20px;
				cursor: pointer;
			}
			.bgc{
				background-color: deepskyblue;
			}
		</style>
	</head>
	<body>
		<div id="box">
			<div id="content">
				<ul>
					<li><img src="img/1.jpg" alt="1" /></li>
					<li><img src="img/2.jpg" alt="1" /></li>
					<li><img src="img/3.jpg" alt="1" /></li>
					<li><img src="img/4.jpg" alt="1" /></li>
				</ul>
			</div>
		</div>
	</body>
	<script src="js/common.js"></script>
	<script type="text/javascript">
		var box=$id("box");
		var uu=box.children[0].children[0];
		var img=document.querySelector("img");		
		var cOl=document.createElement("ol");
		box.appendChild(cOl);
		for(var i=0;i<uu.children.length;i++){
			var cLi=document.createElement("li");
			cLi.innerHTML=i+1;
			cOl.appendChild(cLi);
		}
		var lis=cOl.children;
		lis[0].className="bgc";
		for(var i=0;i<lis.length;i++){
			lis[i].index=i;
			lis[i].onmouseover=function(){
				for(var j=0;j<lis.length;j++){
					lis[j].className="";
				}
				this.className="bgc";
				animate(uu,-this.index*img.offsetWidth);
			}			
		}
		var timer=null;
		move();
		timer=setInterval(move,1000);
		function move(){			
			if(uu.offsetLeft==-(lis.length-1)*img.offsetWidth){
				animate(uu,0);
			}
			if(uu.offsetLeft==0){
				animate(uu,-(lis.length-1)*img.offsetWidth);
			}
			var circle=Math.round(Math.abs(-uu.offsetLeft/img.offsetWidth));
			for(var j=0;j<lis.length;j++){
				lis[j].className="";
			}
			lis[circle].className="bgc";						
		}
		box.onmouseover=function(){
			clearInterval(timer);			
		}
		box.onmouseout=function(){
			timer=setInterval(move,1000);
		}
	</script>
</html>
//common.js文件
function $id(id) {
	return document.getElementById(id)
}

//obj:运动对象 , target:运动目标位置
function animate(obj, target) {
	clearInterval(obj.timer)
	var buchang = obj.offsetLeft > target ? -5 : 5;
	obj.timer = setInterval(function() {
		var result = obj.offsetLeft - target;
		obj.style.left = obj.offsetLeft + buchang + "px";
		if(Math.abs(result) < Math.abs(buchang)) {
			clearInterval(obj.timer);
			obj.style.left = target + "px";
		}
	}, 20);
}
```

### 61.json遍历
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
	</body>
	<script type="text/javascript">
		var json={
			width:200,
			height:300,
			color:"red",
			"background-color":"yellow"			
		}		
		for(var key in json){
			console.log(`json.${key}:${json[key]};`);
		}
	</script>
</html>
```

### 62.简单的demo

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			div{
				width:150px;
				height: 150px;
				background-color:yellow ;
				position: absolute;
			}
		</style>
	</head>
	<body>
		<button id="btn1">leftMove</button>
		<button id="btn2">rightMove</button>
		<div id="box"></div>
	</body>
	<script type="text/javascript">
		function $(id){
			return document.getElementById(id);
		}
		var box=$("box");
		var btn1=$("btn1");
		var btn2=$("btn2");
		//第一种实现
		/*btn1.onclick=function(){
			box.style.left=box.offsetLeft-20+"px";
		}
		btn2.onclick=function(){
			box.style.left=box.offsetLeft+20+"px";
		}*/
		//第二种实现
		/*function go(buchang){
			box.style.left=box.offsetLeft+buchang+"px";
		}
		btn1.onclick=function(){
			go(-20);
		}
		btn2.onclick=function(){
			go(20);
		}*/
		//第三种实现
		function go(buchang){
			return function(){
				box.style.left=box.offsetLeft+buchang+"px";
			}
		}
		btn1.onclick=go(-20);//相当于立即执行go函数，事件触发时会调用内部函数（事件触发函数自动调用）
		btn2.onclick=go(20);
	</script>
</html>

```

### 63.给数组对象添加方法
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
	</body>
	<script type="text/javascript">
		Array.prototype.evenAdd=function(){
			var sum=0;
			for(var i=0;i<this.length;i++){
				if(this[i]%2==0){
					sum+=this[i];
				}
			}
			return sum;
		}
		var arr=[1,2,3,2,3,2,90,5,3,2];
		var result=arr.evenAdd();
		console.log(result);
		console.log(Array.prototype);
	</script>
</html>

```

### 64.数组sort方法
- 冒泡排序
- sort实现数组排序

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
	</body>
	<script type="text/javascript">
		var arr=[1,2,1,332,22,4,2,1];
		var newArr=arr.sort(function(a,b){
			return a-b;
		});
		console.log(newArr);//[1, 1, 1, 2, 2, 4, 22, 332]
	</script>
</html>

```

### 65.正则验证输入用户名
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		请输入用户名：<input type="text" />
	</body>
	<script type="text/javascript">
		var txt=document.querySelector("input");
		txt.onblur=function(){
			var reg=/^[a-z0-9_-]{3,16}$/;
			if(!reg.test(txt.value)){
				alert("请输入数字、字母或者下划线组成的，3-16位用户名！！");
			}
		}
	</script>
</html>
```

### 66.面向对象的demo案例
- Math.random();//生成0-1之间的随机数。
- 定时器，遍历生成20个小方块，把生成的小方块放入父容器
- 面向过程思想
- 面向对象思想
  - 对象：小方块对象（构造函数：宽度、高度、坐标、背景），随机数对象（工具）

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/index.css"/>
	</head>
	<body>
		<div id="father"></div>
	</body>
	<script src="js/tools.js"></script>
	<script src="js/Box.js"></script>
	<script src="js/main.js"></script>
</html>
//index.css
div{
	width:900px;
	height:600px;
	background-color: honeydew;
	position: relative;
}
//tools.js
var tools={
	random:function(min,max){
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}
}
//Box.js
function Box(father,options){
	var options=options||{};
	this.width=options.width||20;
	this.height=options.height||20;
	this.backgroundColor=options.backgroundColor||"black";
	this.x=options.x||0;
	this.y=options.y||0;
	this.div=document.createElement("div");
	father.appendChild(this.div);
	this.father=father;
	this.init();
	this.div.random1()
}
Box.prototype.random=function(){
	var x=tools.random(0,this.father.offsetWidth/this.width-1)*this.width;
	var y=tools.random(0,this.father.offsetHeight/this.height-1)*this.height;
	this.div.style.left=x+"px";
	this.div.style.top=y+"px";
}
Box.prototype.init=function(){
	this.div.style.width=this.width+"px";
	this.div.style.height=this.height+"px";
	this.div.style.backgroundColor=this.backgroundColor;
	this.div.style.position="absolute";
	this.div.style.left=this.x+"px";
	this.div.style.top=this.y+"px";
}
//main.js
var father=document.getElementById("father");
var arr=[];
for(var i=0;i<20;i++){
	var r=tools.random(0,255);
	var g=tools.random(0,255);
	var b=tools.random(0,255);
	var options={
		backgroundColor:"rgb("+r+","+g+","+b+")"
	}	
	var div=new Box(father,options);
	arr.push(div);
	div.random();
}
setInterval(function(){
	for(var i=0;i<arr.length;i++){
		arr[i].random();
	}
},1000);
```


---
### 学习网站
#### 1.[JavaScript Scroll家族以及封装](https://www.cnblogs.com/gchlcc/p/6709625.html)
#### 2.[JavaScript 标准参考教程](http://javascript.ruanyifeng.com/)
#### 3.[WebGI学习网站](http://www.hewebgl.com/)  
#### 4.[邀请码 N8HTN8 蓝灯专业版](https://github.com/getlantern/forum)
#### 5.[轮播图插件](https://www.swiper.com.cn/usage/animate/index.html)、jQuery插件
#### 6.[ES6 入门 阮一峰](http://es6.ruanyifeng.com/#docs/intro)
#### 7.课外了解知识：
- 浏览器怪异模式
- 怪异盒模型
- 标准盒模型
