### 1.原生Js
- jQuery：JS类库
- 框架、插件都是基于JS，让开发变得简单。
- swiper插件——JS都不用写，直接改HTML+CSS就能达到效果

### 2.jQuery
- 版本：1.x兼容IE678、2.x放弃兼容IE678、3.x
- 文件引入：直接下载到本地，使用script标签导入；CDN使用远程服务器上的文件，没有本地的快，但是不占地方，节省资源。
- 文件：压缩版min.js，上线时使用，节省体积、正常版，没有压缩
- jQuery是一个类库

### 3.语法
-  选择器$()
-  后代选择器$("div span")拿到div下面的span
-  window.onload=function(){...};
-  $(document).ready(function(){...})
-  $(function(){...})
-  原生JS中入口函数只能写一个，后面的会覆盖前面的
-  jQuery中的入口函数可以写多个，后面的不会覆盖前面的
-  JQuery的入口函数是dom元素加载完毕之后就开始执行
-  JS原生的入口函数是等dom元素、图片、外部引入文件等所有内容都加载完毕才开始执行。

### 4.jQuery事件
-  点击隐藏元素$(this).hide();
-  jQuery一大特性：隐式迭代
-  mouseenter()事件
-  mouseleave()事件
-  mousedown()、mouseup()事件
-  hover()事件
-  focus、blur事件
-  .css("样式名","样式值")也可以直接传一个属性名和属性值组成的json

### 5.jQuery效果
- 显示隐藏hide、show方法
  - 淡入淡出fadeIn、fadeOut方法
  - fadeToggle循环显示、隐藏
  - fadeTo允许给定显示隐藏的透明度
- 滑动效果
  - 滑入滑出slideDown、slideUp
  - slideToggle滑入滑出的组合
- 动画
  - animate方法，可以传三个函数，第一个参数是样式的json，第二个参数是动画执行的时间，第三个参数回调函数

### 6.jQuery与JS的区别
- 原生JS是一门编程语言
- jQuery是JS的一个类库，封装了很多的方法，可以直接调用
- jQuery能做的事JS都能做，JS能做的事jQuery不一定都能实现

### 7.jQuery版本
- 三个大版本，最新版本的放弃兼容IE6、7、8了

### 8.两个文件的区别
- 压缩版min.js，上线时使用，节省空间
- 非压缩版，开发的时候会用到

### 9.发布时间
- 第一版：2006年1月

### 10.jQuery的使用
- 本地文件的引入，CDN（百度、阿里等）服务器资源引入
- 直接使用，需要注意引入顺序的问题，首先需要引入jQuery，然后才能使用

### 11.入口函数
- window.onload(function(){...});页面（包括图片、外部引入资源等）加载完毕才会执行JS代码
- $(document).ready(function(){...});等HTML骨架（DOM元素）加载完毕后就开始执行
- $(function(){...});

### 12.为什么用jQuery等类库？
- 原生JS会遇到的问题
  - 容易写错，代码量比较大，浏览器兼容问题比较麻烦，动画的实现很麻烦，出错后不容易找到。。。
- jQuery可以完美的解决JS存在的问题，并且能达到相同的效果，所以使用jQuery等类库。

### 13.jQuery的简单demo实现
- $("div")获取到的是一个jQuery对象
- $("div")使用过程中存在隐式迭代，可以使用链式编程达到目的
- show()方法可以传“slow”、“fast”、“毫秒数”参数，来达到动画显示效果
- .css()方法只传一个属性名得到的是该属性对应的值

### 14.css方法的使用
- css方法可以传一个参数、两个参数、一个json对象、一个属性字符串和一个回调函数
- ul>li{我是li$$}*3可实现快速打出多个li
- json：键要加双引号
- 链式编程
- 稍微复杂的应用：
  - Chrome、firfox默认的字体是16px；Chrome默认最小字体是12px，firfox多小的字体都能显示。
  - $("li").css("font-size",function(index,value){if(index==2){return index*10+"px"}});

### 15.$和jQuery
- jQuery库占用了$和jQuery两个变量；
- jQuery中的顶级对象就是$和jQuery
- JS的顶级对象是window(BOM)、document(DOM)

### 16.事件
- mouseover、mouseout鼠标经过、离开事件；mousemove鼠标滑动，每像素都会执行。
- mouseenter、mouseleave鼠标穿过、离开事件
- mouseover与mouseenter的区别：mouseover事件，鼠标进入子元素会再次触发mouseover事件；mouseenter事件，只有进入父元素时才会触发事件。

### 17.简单二级菜单
- show、hide
- slideToggle
- fadeToggle

### 18.jQuery和JS对象的转换
- 使用$(DOM对象)能够把DOM对象转成jQUery对象
- $("div"). ==get(0)== 能够把jQuery对象转成DOM对象
- $("div")[0]也能够把jQuery对象转成DOM对象

### 19.开关灯案例
- 原生JS实现
- jQuery实现：val()方法，不传参数就是获取值，传参数就是设置值。

### 20.find方法
- 获取元素下面的子元素：$("p").find("span");
- 只能找后代元素

### 21.节点关系
- siblings()方法获取所有兄弟元素；
- next()方法获取下一个兄弟元素；
- prev()方法获取上一个兄弟元素；
- parent()方法获取父元素；
- parents()方法能获取所有的祖先元素，里面可以传选择器参数；

### 22.尺寸获取
- height()、width()获取数字类型的值，获取的是css中设置的值
- innerHeight()、innerWidth()包含padding的尺寸
- outerHeight()、outerWidth()包含外边框的尺寸

### 23.特殊选择器
- .eq下标获取元素
- .odd奇数
- .even偶数

### 24.动画
- show();三个参数，第一个speed，第二个参数easing（默认swing，可以设置linear），第三个参数回调函数（动画执行完之后调用）。
- eq();方法，通过下标获取元素，从0开始。有两种用法：
  - $("div:eq(0)");
  - $("div").eq(0);
- animate();自定义动画
- stop();停止动画，解决二级菜单重复动画效果，先添加stop，再添加animate。

### 25.下标
- index();方法获取元素下标，从0开始。
- 选项卡案例重写
- 使用sibling();方法清空除了当前元素的兄弟元素的class

### 26.属性
- attr();
- removeAttr();

### 27.offset
- 获取匹配元素在==当前视口==的指定偏移，只对可见元素有效；
- $("div").offset().top;//获取数值类型结果，不带px；
- $("div").css("width");//获取到的是字符串类型，"200px";
- 包含关系中offset的效果：
  - 子元素的offset不受父元素的影响，拿到的还是距离当前视口的指定偏移；

### 28.position
- 获取==相对父元素==的相对偏移，获取到的也是数值型；

### 29.scrollTop
- 获取元素相对滚动条顶部的偏移。
- 整个页面的滚动一般用$(document).scrollTop();调用
- scroll：滚动事件，一般都是用$(window).scroll(function(){...})调用
- 定位的静态定位、取消定位：static；

### 30.使用jQuery核心函数时，参数不加引号的情况：
- this、window、document、DOM对象

### 31.事件
- bind()；方法
- $("button").bind("mouseenter click",function(){...});
- $("button").bind({"mouseenter":function(){...},"click":function(){...}});
-  $("button").bind("click",{name:"json",age:29},function(e){alert(e.data);})

### 32.只触发一次的事件
- one("click",function(){...});

### 33.事件委托（delegate：委托）
- 隐式迭代会给所有元素隐式添加事件，但是会造成内存负担
- 通过delegate();给父元素添加事件
- $("ul").delegate("li","click",function(){console.log(this.html());});
- 也能够解决动态创建元素的事件添加问题

### 34.终极事件绑定方式
- on();所有的事件添加都可以通过on实现
  - 添加一个事件：
  
```
$("button").on("click",function(){
	alert("click");
});
```
  - 添加多个事件

```
$("button").on("mouseenter click",function(){
	alert("event");
})
$("button").on({
	"mouseenter":function(){
		alert("enter");
	},
	"click":function(){
		alert("click");
	}
})
```

  - 添加事件委托

```
$("ul").on("click","li",function(){
	console.log($(this).text());
});

```

### 35.解除事件绑定
- off（对应on）
- unbind（对应bind）
- undelegate（对应delegate）

### 36.事件对象
- e事件对象
- pageX、pageY；clientX、clientY

### 37.jQuery
- 选择器
- DOM操作
- 样式操作
- 动画
- 事件处理
- ajax（暂时没学）
- 丰富的插件

### 38.动态创建表格
- border-collapse：collapse；边框合并

### 39.for—in遍历对象
- for(var key in obj){console.log(key);console.log(obj[key]);}

### 40.权限选择
- multiple=""；//展开options；

### 41.多库共存
- 释放$符号：jQuery.noConflict();
- IIFE：公开方式，通过window.name=name;

### 42.插件
- plugins
- UI插件，动效
- validate插件，表单验证
- jQuery-UI

---
## 案例部分
### 1.导航栏吸顶效果案例
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
			.tops{
				width: 100%;
				height: 80px;
				background-color: yellow;
			}
			.nav{
				width: 100%;
				height: 100px;
				background-color: black;
			}
			.content{
				width:100%;
				height:10000px;
				background-color: skyblue;
			}
		</style>
		<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
		<script type="text/javascript">
			$(function(){
				$(window).scroll(function(){
					var sTop=$(document).scrollTop();
					var h=$(".tops").height();
					if(sTop>=h){
						$(".nav").css({
							"position":"fixed",
							"top":0
						});
					}else{
						$(".nav").css({
							"position":"static"
						});
					}
				});
			});
		</script>
	</head>
	<body>
		<div class="tops">
			
		</div>
		<div class="nav">
			
		</div>
		<div class="content">
			
		</div>
	</body>
</html>

```
### 2.广告跟随效果案例：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin:0;
				padding: 0;
			}
			div{
				width:100px;
				height:300px;
				background-color: yellow;
				position: relative;
				top:300px;
			}
			body{
				height:10000px;
			}
		</style>
		<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
		<script type="text/javascript">
			$(function(){
				$(window).scroll(function(){
					var sTop=$(document).scrollTop();
					$("div").animate({
						"top":sTop+300
					},20);
				});
			});
		</script>
	</head>
	<body>
		<div class="box">
			
		</div>
	</body>
</html>

```
### 3.bind用法案例
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<button>点击</button>
	</body>
	<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
	<script type="text/javascript">
		/*$("button").bind("mouseenter click",function(){
			alert("event");
		});*/
		/*$("button").bind({
			"mouseenter":function(){
				alert("enter");
			},
			"click":function(){
				alert("click");
			}
		});*/
		$("button").bind("click",{
			name:"张三",
			age:29,
			gender:'男'
		},function(e){
			$.each(e.data,function(index,value){
				console.log(`${index}:${value};`);
			});
		});
	</script>
</html>

```

### 4.事件委托

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
		<script type="text/javascript">			
			$(function(){
				$("button").click(function(){
					var cLi=$("<li>我是新增的li</li>");
					$("ul").append(cLi);
				});
				$("ul").delegate("li","click",function(){
					console.log($(this).text());
				});
			});			
		</script>
	</head>
	<body>
		<button>点击</button>
		<ul>
			<li>我是01号li</li>
			<li>我是02号li</li>
			<li>我是03号li</li>
			<li>我是04号li</li>
			<li>我是05号li</li>
			<li>我是06号li</li>
			<li>我是07号li</li>
			<li>我是08号li</li>
			<li>我是09号li</li>
			<li>我是10号li</li>
		</ul>
	</body>
</html>

```
### 5.动态创建表格
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
			table{
				width:600px;
				margin:100px auto;
				border: 2px solid #000;
				border-collapse: collapse;/*边框合并*/
			}
			table th,table td{
				border: 1px solid #000;
				text-align: center;
			}
		</style>
		<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
		<script type="text/javascript">
			$(function(){
				var data=[
				{
					"number":1,
					"name":"天龙八部",
					"renwu":"乔峰、段誉、虚竹",
					"star":"四星"
				},
				{
					"number":2,
					"name":"水浒传",
					"renwu":"宋江、林冲、李逵",
					"star":"四星半"
				},
				{
					"number":3,
					"name":"都挺好",
					"renwu":"苏大强、苏明玉、苏明哲",
					"star":"五星"
				},
				{
					"number":4,
					"name":"封神演义",
					"renwu":"杨戬、武吉、姜子牙",
					"star":"四星"
				}];//数组对象
				var html="";
				for(var i=0;i<data.length;i++){
					html+="<tr>";
					html+=		"<td>"+data[i].number+"</td>";
					html+=		"<td>"+data[i].name+"</td>";
					html+=		"<td>"+data[i].renwu+"</td>";
					html+=		"<td>"+data[i].star+"</td>";
					html+="</tr>";
					/*html+= `<tr>
								<td>${data[i].number}</td>
								<td>${data[i].name}</td>
								<td>${data[i].renwu}</td>
								<td>${data[i].star}</td>
							</tr>`;*/
				}//动态创建元素
				$("#content").append(html);//插入元素
			});			
		</script>
	</head>
	<body>
		<table>
			<thead>
				<tr>
					<th>编号</th>
					<th>名称</th>
					<th>任务</th>
					<th>推荐指数</th>
				</tr>
			</thead>
			<tbody id="content"></tbody>			
		</table>
	</body>
</html>

```
### 6.表单拖拽
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			select{
				width:200px;
				height:600px;
				font-size: 24px;
				text-align: center;
			}
			span{
				display: inline-block;
				position: relative;
				top:-400px;
			}
			button{
				display: block;
				width:40px;
				height:30px;
				font-size: 20px;
				margin:10px 0;
			}
		</style>
		<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
		<script type="text/javascript">
			$(function(){
				var one=$("select:first");
				var two=$("select:last");
				var btns=$("button");
				btns.eq(0).on("click",function(){
					two.append(one.children());
				});
				btns.eq(1).on("click",function(){
					one.append(two.children());
				});
				btns.eq(2).on("click",function(){
					two.append($("select:first option:selected"));
				});
				btns.eq(3).on("click",function(){
					one.append($("select:last option:selected"));
				});				
			});
		</script>
	</head>
	<body>
		<select name="sec" multiple="">
			<option value="1">天龙八部</option>
			<option value="2">飞狐外传</option>
			<option value="3">雪山飞狐</option>
			<option value="4">连城诀</option>
			<option value="5">射雕英雄传</option>
			<option value="6">鹿鼎记</option>
			<option value="7">陆小凤</option>
		</select>
		<span>
			<button>>></button>
			<button><<</button>
			<button>></button>
			<button><</button>
		</span>		
		<select name="sec" multiple=""></select>
	</body>
</html>

```
### 7.省市选项菜单
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		<select name="sheng" id="sheng">
			
		</select>
		<select name="shi" id="shi">
			
		</select>
	</body>
	<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
	<script type="text/javascript">
		var data=[{
			"sheng":"陕西",
			"shi":["西安","商洛","安康","咸阳","兴平","乾县","宝鸡"]
		},{
			"sheng":"贵州",
			"shi":["贵阳","黔南","黔东南","黔西南","福泉","都匀","凯里","三都"]
		},{
			"sheng":"广西",
			"shi":["南宁","桂林","北海","柳州","贵港","玉林","百色","贺州"]
		},{
			"sheng":"北京",
			"shi":["东城区","西城区","海淀区","朝阳区","丰台区","石景山区","门头沟区","通州区"]
		},{
			"sheng":"深圳",
			"shi":["罗湖区","西山区","海淀区","朝阳区","丰台区","石景山区","门头沟区","通州区"]
		}];
		$(function(){
			/*var html="";
			for(var i=0;i<data.length;i++){
				html+=`
					<option value="${data[i].sheng}">${data[i].sheng}</option>
				`;
			}
			$("#sheng").html(html);
			$("#sheng").change(function(){
				var shengName=$(this).val();
				var html="";
				for (var i=0;i<data.length;i++) {
					if(data[i].sheng==shengName){
						var shiArr=data[i].shi;
						for(var j=0;j<shiArr.length;j++){
							html+=`
								<option value="${shiArr[j]}">${shiArr[j]}</option>
							`;
						}
					}
				}
				$("#shi").html(html);
			});
			$("#sheng").triggerHandler("change");*/
			var shengArr=[];
			for(var i=0;i<data.length;i++){
				shengArr.push("<option value=\""+data[i].sheng+"\">"+data[i].sheng+"</option>");
			}
			$("#sheng").html(shengArr.join(""));			
			$("#sheng").change(function(){
				var shiArr=[];
				var val=$(this).val();
				for(var i=0;i<data.length;i++){
					if(data[i].sheng==val){
						var shi=data[i].shi;
						for(var j=0;j<shi.length;j++){
							shiArr.push("<option value=\""+shi[j]+"\">"+shi[j]+"</option>");
						}
					}
				}
				$("#shi").html(shiArr.join(""));
			});
			$("#sheng").triggerHandler("change");
		});
	</script>
</html>

```
---
## 学习网站
[前端常用框架对比](https://www.cnblogs.com/leolovexx/p/5691402.html)  
[JavaScript插件](https://www.jqhtml.com/category/article/plugs)  
[jQuery之家](http://www.htmleaf.com/)  
[json在线解析](https://www.json.cn/)