## 通过className获取元素
- IE8及以下不兼容：getElementsByClassName
- 带有ID名的getClass函数封装：
```
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
```
## event
- IE中使用的是：window.event
- 兼容写法：

```
var event=event||window.event;
```
## scroll
- Safari中使用的是：window.pageXOffset
- 没有文档声明的IE6、7、8使用的是：document.body.scroll
- 正常高级浏览器使用的是：document.documentElement.scroll
- 兼容封装：
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
[JavaScript Scroll家族以及封装](https://www.cnblogs.com/gchlcc/p/6709625.html)  

## 获取屏幕尺寸
- IE9+：使用window.innerWidth
- 标准浏览器：使用document.documentElement.clientWidth
- 非标准浏览器：使用document.body.clientWidth
- 兼容处理：
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
## forEach
- forEach()方法在IE8及以下不兼容，只能使用for循环代替。

## 阻止冒泡
- IE低版本使用：window.event.cancelBubble=true;
- 正常浏览器使用：event.stopPropagation();
- 兼容写法：
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
## 获取点击元素本身
- IE低版本中使用的是：srcElement
- 正常浏览器中使用的是：event.target
- 兼容写法：

```
var targetId=event.target.id||event.srcElement.id;
```
## 输入内容时
- 正常浏览器使用的是：oninput 
- IE6、7、8使用的是：onpropertychange
- 兼容写法：

```
element.oninput=element.onpropertychange=function(){};
```
## opacity
- 正常浏览器使用的是：opacity：.5;
- IE低版本使用的是：filter:alpha(opacity=50);
- 兼容写法：
```
opacity:0.5;
filter:alpha(opacity=50);  //filter 过滤器   兼容IE678
```
[opacity兼容性以及存在问题处理](http://www.cnblogs.com/cleaverlove/p/6309013.html)

## 获取选中文字
- 正常浏览器使用的是：window.getSelection().toString();
- IE低版本使用的是：document.selection.createRange().text;
- 兼容写法：
```
if(window.getSelection){
	txt=window.getSelection().toString();
}else{
	txt=document.selection.createRange().text;
}
```
## 节点兼容
- IE低版本使用的是：
  - nextSibling
  - previousSbling
  - firstChild
  - lastChild
- 高级浏览器使用的是：
  - nextElementSibling
  - previousElementSibling
  - firstElementChild
  - lastElementChild
- 兼容写法
  - 使用||符号连接，高级浏览器适用的写在前面。

## 获取css样式
- obj.currentStyle.width    ==IE6、7、8使用的方式==
- window.getComputedStyle(obj,null).width   ==高版本浏览器==
- 兼容处理
```
function getAttr(obj,attribute){
	if(obj.currentStyle){
		return obj.currentStyle[attribute];
	}else{
		return window.getComputedStyle(obj,null)[attribute];
	}
}
```
## 事件监听
- 高版本浏览器识别的是：addEventListener，添加事件监听
  - btn.addEventListener("click",function(){},false);
  - 第一个参数，事件名；第二个参数，要执行的函数；第三个参数，布尔值，是否在捕获阶段执行，一般都是false。
  - 这样添加的事件，后面添加的同名事件不会覆盖前面的同名事件，==先添加的先执行,执行函数中this指向的是事件调用者==。
- IE6、7、8不兼容，替代方法attachEvent,添加多个同名事件，==先执行后添加的，执行函数中this指向的是window==;
  - btn.attachEvent("onclick",function(){});
- 兼容处理：
  - function bind(obj,eventName,callback){};

```
<script type="text/javascript">
	function bind(obj,eventName,callBack){
		if(obj.addEventListener){
			obj.addEventListener(eventName,callBack);
		}else{
			obj.attachEvent("on"+eventName,function(){
				callBack.call(obj);
			});
		}
	}
	var btn=document.getElementById("btn");
	bind(btn,"click",function(){
		console.log(this);
	})
</script>
```