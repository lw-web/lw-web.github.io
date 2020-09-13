### 1.ajax
- 创建xhr对象
  - xhr兼容IE6使用new ActiveXObject("Microsoft.XMLHTTP");
- open方法调用，参数一：提交方式，参数二：提交地址，参数三：异步或者同步；
- 发送send，get方式参数传null；
- 回调函数
  - xhr.onreadystatechange=function(){if(xhr.readystate==4//请求完成&&xhr.status==200//OK){var result=xhr.responseText}}
  - readyState：请求状态，0、1、2、3、4；
  - status：200、404；

get请求：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<form action="" method="post">
			用户名：<input type="text" name="txt" id="txt" value="" />
			<button type="button">验证</button>
			<span></span>
		</form>
	</body>
	<script type="text/javascript">
		var btn=document.querySelector("button");
		btn.onclick=function(){
			var uname=document.getElementById("txt").value;
			if(window.XMLHttpRequest){
				var xhr=new XMLHttpRequest();
			}else{
				var xhr=new ActiveXObject("Microsoft.XMLHTTP");
			}
			xhr.open("get","register.php?uname="+uname);
			xhr.send(null);
			xhr.onreadystatechange=function(){
				if( xhr.readyState==4 && xhr.status==200 ){
					var result=xhr.responseText;
					document.querySelector("span").innerHTML=result;
				}
			}
		}
	</script>
</html>

```

post请求

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
			body{
				padding:20px;
			}
			.nav{
				height:40px;
				background-color: yellow;
				line-height: 40px;
				text-align: center;
			}
			input,button{
				height: 40px;
				line-height: 40px;
				font-size: 18px;
				width:200px;
				outline: none;
				border: none;
				border: 1px solid #000;
				vertical-align: top;
				display: block;
				float: left;
			}
			input{
				box-sizing: border-box;
				padding-left:20px;
			}
			button{
				width: 60px;
			}
			.box{
				display: inline-block;
				height: 40px;
				line-height: 40px;
				text-align: center;
				width:200px;
				background-color: skyblue;
				font-size: 20px;
			}
		</style>
	</head>
	<body>
		<div class="nav">
			登录验证
		</div>
		<input type="text" name="txt" id="txt" value="" />
		<button>验证</button>
		<div class="box"></div>
	</body>
	<script type="text/javascript">
		var btn=document.querySelector("button");
		btn.onclick=function(){
			var uname=document.getElementById("txt").value;
			var xhr=null;
			if(window.XMLHttpRequest){
				xhr=new XMLHttpRequest();
			}else{
				xhr=new ActiveXObject("Microsoft.XMLHTTP");
			}
			xhr.open("post","post.php");
			xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
			var parments="uname="+uname;
			xhr.send(parments);
			xhr.onreadystatechange=function(){
				if(xhr.readyState==4 && xhr.status==200){
					var result=xhr.responseText;
					document.querySelector(".box").innerHTML=result;
				}
			}
		}
	</script>
</html>

```
接口文档综合练习

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div class="box">
			<nav></nav>
			<form action="" method="">
				用户名：<input type="text" name="" id="username" value="" /><span id="usernameText"></span><br />
				邮&nbsp;&nbsp;&nbsp;箱：<input type="text" name="" id="useremail" value="" /><span id="useremailText"></span><br />
				手机号：<input type="text" name="" id="userphone" value="" /><span id="userphoneText"></span><br />
			</form>
		</div>
	</body>
	<script type="text/javascript">
		//验证用户名
		var username=document.getElementById("username");
		username.onblur=function(){
			var usernametxt=this.value;
			var xhr=new XMLHttpRequest();
			xhr.open("get","server/checkUname.php?uname="+usernametxt);
			xhr.send(null);
			xhr.onreadystatechange=function(){
				if(xhr.readyState==4 && xhr.status==200){
					var result=xhr.responseText;
					if(result=="error"){
						document.getElementById("usernameText").innerHTML="用户名被占用";
					}else if(result=="ok"){
						document.getElementById("usernameText").innerHTML="用户名可以使用";
					}
				}
			}
		}
		//验证邮箱
		var useremail=document.getElementById("useremail");
		useremail.onblur=function(){
			var useremailtxt=this.value;
			var xhr=new XMLHttpRequest();
			xhr.open("post","server/checkEmail.php");
			var parm="email="+useremailtxt;
			xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
			xhr.send(parm);
			xhr.onreadystatechange=function(){
				if(xhr.readyState==4 && xhr.status==200){
					var result=xhr.responseText;
					if(result==0){
						document.getElementById("useremailText").innerHTML="邮箱名可用";
					}else if(result==1){
						document.getElementById("useremailText").innerHTML="邮箱名不可用";
					}
				}
			}
		}
		//验证手机号码
		var userphone=document.getElementById("userphone");
		userphone.onblur=function(){
			var userphonenum=this.value;
			var xhr=new XMLHttpRequest();
			xhr.open("post","server/checkPhone.php");
			var parm="key="+userphonenum;
			xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
			xhr.send(parm);
			xhr.onreadystatechange=function(){
				if(xhr.readyState==4 && xhr.status==200){
					var result=xhr.responseText;
					var resuJson=JSON.parse(result);
					if(resuJson.status==0){
						document.getElementById("userphoneText").innerHTML=resuJson.message.tips;
					}else if(resuJson.status==1){
						document.getElementById("userphoneText").innerHTML=resuJson.message;
					}
				}
			}
		}
	</script>
</html>

```

### 2.xml——json
-  xml

```
<script type="text/javascript">
	window.onload=function(){
		var xhr=new XMLHttpRequest();
		xhr.open("get","xml");
		xhr.send(null);
		xhr.onreadystatechange=function(){
			if(xhr.readyState==4 && xhr.status==200){
				var result=xhr.responseXML;
				var books=result.children[0].children;
				var html=document.querySelector("table").innerHTML;
				for(var i=0;i<books.length;i++){
					var name=books[i].children[0].textContent;
					var author=books[i].children[1].textContent;
					var disc=books[i].children[2].textContent;
					html+="<tr><td>"+name+"</td><td>"+author+"</td><td>"+disc+"</td></tr>";
				}
				document.querySelector("table").innerHTML=html;
			}
		}
	}
</script>
```

-  json

```
<script type="text/javascript">
	window.onload=function(){
		var xhr=new XMLHttpRequest();
		xhr.open("get","person.json");
		xhr.send(null);
		xhr.onreadystatechange=function(){
			if(xhr.readyState==4 && xhr.status==200){
				var result=xhr.responseText;
				var resuJson=JSON.parse(result);
				var html=document.querySelector("table").innerHTML;
				for(var i=0;i<resuJson.length;i++){
					var name=resuJson[i].name;
					var age=resuJson[i].age;
					var sex=resuJson[i].sex;
					html+=`
						<tr>
							<td>${name}</td>
							<td>${age}</td>
							<td>${sex}</td>
						</tr>
					
					`;
				}
				document.querySelector("table").innerHTML=html;
			}
		}
	}
</script>
```

-  web数据


```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			table{
				width:1000px;
				border: 2px solid #000;
				margin: 10px auto;
			}
			table tr th{
				background-color: yellow;
			}
			table tr td{
				background-color: skyblue;
				text-align: center;
			}
			#box{
				width: 80%;
				margin:10px auto;
				display: flex;
				justify-content:space-around;
				flex-wrap: wrap;
			}
			.content{
				width: 300px;
				height: 300px;
				border: 1px solid #ccc;
				border-radius: 10px;
				text-align: center;
				margin: 10px;
				background-color: #ccc;
			}
			.content a{
				text-decoration: none;
				color: black;
			}
			.content img{
				width: 200px;
			}
		</style>
	</head>
	<body>
		<div id="box"></div>
		<table>
			<tr>
				<th>login</th>
				<th>id</th>
				<th>node_id</th>
				<th>avatar_url</th>
				<th>type</th>
				<th>html_url</th>				
			</tr>			
		</table>		
	</body>
	<script type="text/javascript">
		var xhr=new XMLHttpRequest();
		xhr.open("get","https://api.github.com/users");
		xhr.send(null);
		xhr.onreadystatechange=function(){
			if(xhr.readyState==4 && xhr.status==200){
				var result=xhr.responseText;
				var resuJson=JSON.parse(result);
				console.log(resuJson);
				var html1=document.querySelector("table").innerHTML;
				var html2=document.getElementById("box").innerHTML;
				for(var i=0;i<resuJson.length;i++){
					var login=resuJson[i].login;
					var id=resuJson[i].id;
					var node_id=resuJson[i].node_id;
					var avatar_url=resuJson[i].avatar_url;
					var type=resuJson[i].type;
					var html_url=resuJson[i].html_url;
					html1+=`
						<tr>
							<td>${login}</td>
							<td>${id}</td>
							<td>${node_id}</td>
							<td>${avatar_url}</td>
							<td>${type}</td>
							<td>${html_url}</td>
						</tr>					
					`;
					html2+=`
						<div class="content">
							<a href="${html_url}">
								<h3>${login}</h3>
								<img src="${avatar_url}"/>
							</a>
						</div>
					`;
				}
				document.querySelector("table").innerHTML=html1;
				document.getElementById("box").innerHTML=html2;
			}
		}
	</script>
</html>

```
### 3.手机号归属地查询
- [web接口大全](https://www.showapi.com/)
- 用户名：lw6989661；密码：lw6989661
- 调用接口：http://route.showapi.com/6-1?showapi_appid=94587&showapi_sign=70ab91282bfc42218286c14a0cd65528&num="+手机号；

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
				padding: 30px;
			}
			label,input,button{
				display: inline-block;
				width:150px;
				height:30px;
				line-height: 30px;
				font-size: 18px;
				text-align: center;
			}
			input{
				width: 300px;
				text-align: left;
				padding-left: 20px;
			}
			table{
				width:800px;
				border: 2px solid #000;
				margin: 10px;
			}
			table tr th{
				background-color: yellow;
			}
			table tr td{
				background-color: skyblue;
				text-align: center;
			}
		</style>
	</head>
	<body>
		<label for="">请输入手机号：</label><input type="text" id="phone" value="" />
		<button>查询</button>
		<table>
			<tr>
				<th>卡类名称</th>
				<th>所属省份</th>
				<th>所属城市</th>
				<th>所属城市编码</th>
				<th>所属城市区号</th>
				<th>所属号段</th>
			</tr>			
		</table>
	</body>
	<script type="text/javascript">
		var btn=document.querySelector("button");
		btn.onclick=function(){
			var phone=document.querySelector("input").value;
			console.log(phone);
			var xhr=new XMLHttpRequest();
			xhr.open("get","http://route.showapi.com/6-1?showapi_appid=94587&showapi_sign=70ab91282bfc42218286c14a0cd65528&num="+phone);
			xhr.send(null);
			xhr.onreadystatechange=function(){
				if(xhr.readyState==4 && xhr.status==200){
					var result=xhr.responseText;
					var resuJson=JSON.parse(result).showapi_res_body;
					var html=document.querySelector("table").innerHTML+`
						<tr>
							<td>${resuJson.name}</td>
							<td>${resuJson.prov}</td>
							<td>${resuJson.city}</td>
							<td>${resuJson.cityCode}</td>
							<td>${resuJson.areaCode}</td>
							<td>${resuJson.num}</td>
						</tr>					
					`;
					document.querySelector("table").innerHTML=html;
				}
			}
		}		
	</script>
</html>

```