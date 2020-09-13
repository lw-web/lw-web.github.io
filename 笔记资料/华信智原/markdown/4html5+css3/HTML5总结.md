### 1.基本介绍：
- 下一代新版本；
- 2014年正式公布；
- 为移动端而生；
- 还在完善，浏览器兼容还存在问题；
- 新特性应该基于HTML、CSS、DOM、JavaScript；
- 减少外部插件的需求；
- 获取更多代脚本标记；
- 新特性：
  - canvas（画布）绘画
  - video和audio
- 对本地存储更好地支持；
- 新的特殊内容的元素：article、footer、header、nav、section
- 新的表单控件：calendar、date、time、email、url、search
- CSS3和JS的新的API（应用程序编程接口）。

### 2.什么是HTML5？（面试题）
- HTML：HTML的扩展
- CSS：CSS3
- JS：增加了新的属性和接口（document.querySelector();/document.querySelectorAll();）

### 3.新的标签
- HTML负责结构，只负责语义
- header：头部
- nav：导航
- footer：底部
- article：文章
- aside：侧边栏
- section：区段、章节、页眉、页脚的块。
- 这些标签都是块级元素
- IE9以上才支持这些标签
- 兼容处理：引入兼容包

### 4.应用程序标签
- datalist：结合option使用，使用id、list和input标签关联，达到动态提示效果。（datalist内容写在value属性中）
- progress:进度条，value：设置完成度，100%默认是1；max设置自定义100%是多少；无法操作样式，不好用。

### 5.新的属性的添加
- data-*：自定义属性


```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<ul>
			<li data-name="张三">张三</li>
			<li data-name="李四">李四</li>
			<li data-name="王五">王五</li>
			<li data-name="马六">马六</li>
		</ul>
	</body>
	<script type="text/javascript">
		var uu=document.querySelector("ul");
		/*uu.addEventListener("click",function(e){//addEventListener一种事件添加方式，可以解决给同一对象添加多个事件
			var e=e||window.event;//通过事件对象获取当前触发事件的元素
			var dataName=e.target.getAttribute("data-name");//获取当前元素的属性
			alert(dataName);
		});*/
		uu.onclick=function(e){
			var e=e||window.event;//事件委托是一种思想，事件监听是一种事件添加的实现方式。
			var dataName=e.target.getAttribute("data-name");
			alert(dataName);
		}
		//通过createElement创建自定义标签
		var liwei=document.createElement("liwei");
		liwei.innerHTML="我是李伟";
		uu.appendChild(liwei);
	</script>
</html>

```
### 6.智能表单
- submit、reset、file、password、text、button、image、radio、checkbox...
- email、url、number、range（进度：step设置步长）、search、color、date
- max、min、step、value
- month、week、time、datetime、datatime-local

### 7.svg
- 可伸缩矢量图形
- 图像放大改变尺寸质量不会改变，不会失真，任何分辨率下都能够高质量打印

### 8.音频、视频
- audio：src、controls
- if(audio.paused){audio.play();}else{audio.pause();};
- bgsond:添加背景音乐（没啥用，淘汰了）；
- autoplay、loop、controls
- video

### 9.拖拽
- dragenter、dragleave：测试事件是否发生，没实际意义
- dragover(e.preventDefault:阻止浏览器的默认事件；e.stopPropagation：阻止事件冒泡；)
- drop(这个事件要触发必须dragover阻止他的默认事件);
- e.dataTransfer.setData("text/plain：普通文本",e\.target\.id)；
- e.dataTransfer.getData("text/plain")；
- e.dataTransfer.setData("text/uri-list：图片",e\.target\.id)；

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box{
				width: 500px;
				height:500px;
				border: 2px solid #000;
				text-align: center;
				color:red;
			}
		</style>
	</head>
	<body>
		<img src="img/05big.jpg"/>
		<p id="content">hW3CSchool 每月接受上百万人次的用户访问，并产生数千万的页面浏览量。W3Cschool是一个专业的编程入门学习及技术文档查询应用，提供包括HTML，CSS，Javascript，jQuery，C，PHP，Java，Python，Sql，Mysql等编程语言和开源技术的在线教.</p>
		<div id="box">			
		</div>
	</body>
	<script type="text/javascript">
		var box=document.getElementById("box");
		var content=document.getElementById("content");
		box.addEventListener("dragenter",function(){
			console.log(1);
		});
		box.addEventListener("dragleave",function(){
			console.log(2);
		});
		box.addEventListener("dragover",function(e){
			console.log(3);
			e.preventDefault();
			e.stopPropagation();
		});
		box.addEventListener("drop",function(e){
			console.log(4);
			var data=e.dataTransfer.getData("text/plain");			
			console.log(data);
			if(/^http/.test(data)){
				var data=e.dataTransfer.getData("text/uri-list");
				var cImg=document.createElement("img");
				cImg.src=data;
				this.appendChild(cImg);
			}else{
				this.innerHTML=data;
			}			
		});		
	</script>
</html>

```

### 10.markdown文件类型
- 类似于html

### 11.storage
- localStorage:没有时间限制的存储；
- sessionStorage：有时间限制的存储（浏览器关闭就不存在了）；
- localStorage.setItem("key","value");如果key相同，会覆盖。
- localStorage.getItem("key");
- 替代了cookie，cookie存在只能存储很小数据；cookie需要前端开发者自己封装 setCookie ， getCookie；不可以跨域调用；Cookie 的内容会随着请求一并发送的服务器（带宽浪费） 等缺点。   

**[web storage和cookie的区别](https://www.nowcoder.com/questionTerminal/20d711b3651a4413bf96481b73794ac1)**
### 12.classList（IE9都不支持）
- 类名列表
- method：add、remove、toggle、contains

### 13.history
- window.history.back();//后退
- window.history.forword();//前进
- window.history.go();//刷新

### 14.web存储
- localStorage.setItem("key","value");//value可以是数组、对象（必须是字符串形式，引号必须是外单内双）；
- localStorage.getItem("key");
- 读取localStorage中的对象value值时，需要使用==JSON.parse()//String转Json==，因为获取到的是str类型;
- ==JSON.stringfy();//Json转String==

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		
	</body>
	<script type="text/javascript">
		localStorage.setItem("friends",'{"name":"张三","age":23}');
		localStorage.setItem("colors",'[red,blue,yellow,purple]');
		var str=localStorage.getItem("friends");
		var str1=localStorage.getItem("colors");
		var end=str1.lastIndexOf("]");
		str2=str1.slice(1,end);
		var arr=str2.split(",");
		var obj=JSON.parse(str);
		for(var key in obj){
			console.log(obj[key]);
		}
	</script>
</html>

```

### 15.canvas
- var c=document.getElementById("xxx");
- var ctx=c.getContext("2d");
- ctx.moveTo(x,y);//起点
- ctx.lineTo(x,y);//终点（多个终点形成折线）
- ctx.closePath();//闭合路径
- - ctx.fillStyle="yellow";//设置填充颜色
- ctx.fill();//填充颜色，默认是黑色（设置填充颜色后必须再调用填充命令才生效）
- ctx.stroke();//划线
- ctx.strokeStyle="red";//设置划线的颜色
- ctx.lineWidth=20;//设置线宽（线宽会继承）
- ctx.beginPath();//打断前面的绘制，重新开始


```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<canvas id="myCan" width="600" height="600"></canvas>
	</body>
	<script type="text/javascript">
		var c=document.getElementById("myCan");
		c.style.border="1px solid black";
		var ctx=c.getContext("2d");
		var width=20;
		var height=20;
		for(var i=0;i<c.width/width;i++){
			//横线
			ctx.beginPath();
			ctx.moveTo(0,i*height);
			ctx.lineTo(600,i*height);
			if(i%2==0){
				ctx.strokeStyle="red";
			}else{
				ctx.strokeStyle="black";
			}
			ctx.stroke();
			//竖线
			ctx.beginPath();
			ctx.moveTo(i*width,0);
			ctx.lineTo(i*width,600);
			if(i%2==0){
				ctx.strokeStyle="green";
			}else{
				ctx.strokeStyle="black";
			}
			ctx.stroke();
		}
		ctx.beginPath();
		ctx.moveTo(0,600);
		ctx.lineTo(100,500);
		ctx.lineTo(200,450);
		ctx.lineTo(300,300);
		ctx.lineTo(400,400);
		ctx.lineTo(500,250);
		ctx.lineTo(600,0);
		ctx.strokeStyle="red";
		ctx.lineWidth=5;
		ctx.stroke();		
	</script>
</html>

```