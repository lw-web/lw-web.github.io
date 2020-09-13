### 1、基本语法
- 基本标记：<?php...?>
- 页面输出：echo "hello world!";(分号不能少)echo不能输出复杂类型
- 注释：//、/**/
- 字符串：""
- 声明变量：$str="今天好像过秋天！";
- 数值类型：$num=10;
- 复杂类型：数组、对象
  - 数组：$arr=array();
  - $arr[0]="贾宝玉";
  - $arr["name"]="和田玉";
  - print_r($arr);
  - for($i=0;$i<count($arr);$i++){echo $arr[$i];}
  - if(){}else{}
  - 字符串拼接：.符号
  - $arr1=array("林冲","张飞");
  - $arr2=array("name1"=>"张三","name2"=>"马云");
  - foreach($arr as $key=>$value){echo $key.$value;}
  - json_encode:把数组转成字符串；
- 函数：function add($a,$b){return $a+$b;};

```
foreach($arr4 as $key=>$value){
	echo "<br/>";
	echo $key."<br/>";
	print_r($value);
	echo "<br/>";
	echo $value["name"]."<br/>";
	echo $value["age"]."<br/>";
	echo $value["gender"]."<br/>";
}
function add($a,$b){
	return $a+$b;
}
echo add(1,2);
```
99乘法表：

```
<table border="1px">
	<?php for($i=1;$i<10;$i++): ?>
	<tr>
		<?php for($j=1;$j<=$i;$j++): ?>
			<td>
				<?php 
					echo $i." * ".$j." = ".$i*$j;
				?>
			</td>
		<?php endfor; ?>
	</tr>
	<?php endfor; ?>
</table>

```

### 2、变量作用域
- 局部访问全局变量：
```
<?php
	$x=10;
	$y=20;
	function fun(){
		global $x,$y;
		echo $x+$y;
		echo "<br/>";
	}
	fun();
	function fun1(){
		echo $GLOBALS["x"]+$GLOBALS["y"];
	}
	fun1();
?>
```
### 3、数据提交
- get提交：显示提交信息
- $_GET[];
- post提交：提交信息不会在地址栏显示出来
- $_POST[];
- response：响应
- request：请求
- array_key_exists($key,$arr); 查询数组是否存在指定信息；

### 4、ajax
- type="button";可阻止button提交跳转。
- 阿贾克斯：异步的JavaScript和xml（一种数据类型，json替代了xml）
- 异步无刷新技术；和后台做数据交互。
- 不是编程语言，是一门技术或者一套标准，属于JS的一个分支。
- ajax使用：
  - 创建ajax对象
  - open方法，三个参数：提交方式、提交地址、同步还是异步（默认异步）
  - 发送：send()方法，参数——get方式下传null；
  - onreadystatechange=function(){xhr.responseText;}

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<h1>登录验证</h1>
		<form action="" method="">
			用户名：<input type="text" name="txt" id="txt" value="" />
			密码：<input type="password" name="psw" id="psw" value="" />
			<input type="button" value="验证" id="btn"/>
			<span id="span"></span>
		</form>
	</body>
	<script type="text/javascript">
		var btn=document.getElementById("btn");
		btn.onclick=function(){
			var val1=document.getElementById("txt").value;
			var val2=document.getElementById("psw").value;
			var ajax=new XMLHttpRequest();//1.创建ajax对象
			ajax.open("get","ajax.php?uname="+val1+"&psw="+val2);//2.调用ajax对象open方法
			ajax.send(null);//3.向后台发送请求
			ajax.onreadystatechange=function(){//4.根据后台返回数据改变页面内容
				var result=ajax.responseText;
				document.getElementById("span").innerHTML=result;				
			}			
		}
	</script>
</html>

```