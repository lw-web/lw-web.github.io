# `node Day2`

## nodeJS
- 是一个JS运行时的环境（平台）
- 单线程
- 异步I/O
- 事件驱动
- 基于Chrome V8引擎

## 命令行的基本操作
- 切换盘符——`C：、D：`
- 切换目录——`cd windows`
- 查看目录详情——`dir`
- cmd快捷键——`Windows+R`

## 安装node
- 环境变量匹配
- admin里面的path添加node路径
- 测试`node -v`
- npm测试`npm -v`
- cnpm -v配置cnpm之后npm命令替换成cnpm就可以了

## nodeJS核心模块
- 文件操作：`"fs"`
- 服务器模块：`"http"`
- 路径模块：`"path"`
- 系统模块：`"os"`

## 创建一个服务器
- 引入核心模块：```var http=require("http"); ```
- 创建服务器：```var server=http.createServer(); ```
- 添加请求事件：```server.on("request",function(req,res){var url=req.url; if(url==="/"){res.end("hello world!")}})```
- 设置响应头编码：```res.setHeader("content-type","text/html;charset=utf-8");```
- 添加监听端口：```server.listen(3000,function(){console.log("server is runing......")})```

## 模块
- 核心模块
- 第三方模块
- 自己定义的模块

### 文件模块
- 引入：require
  - ```var goods=require("./goods"); console.log(goods.str);```
- 导出：exports
  - 是一个空对象
  - ```exports.str="hello world!";```

## 各种资源的加载
-  ```res.writeHead(200,{"content-type":"text/plain;charset=utf8"});```
-  ```var url=req.url;if(url=="/page"){fs.readFile("/page.html",function(err,data){res.end(dat)})}```
-  各种资源对应的`content-type`：
  - `html：text/html`
  - `css：text/css`
  - `jpg：image/jpeg`
  - `javascript：application/x-javascript`

```javascript
var http=require("http");
var fs=require("fs");
var server=http.createServer();
server.on("request",function(req,res){
	var url=req.url;
	if(url=="/"){
		fs.readFile("html.html",function(err,data){
			if(err){
				return "资源不存在";
			}
			res.writeHead(200,{"content-type":"text/html;charset=utf-8"});
			res.end(data);
		});
	}else if(url=="/css"){
		fs.readFile("css.css",function(err,data){
			if(err){
				return "资源不存在";
			}
			res.end(data);
		})
	}else if(url=="/js"){
		fs.readFile("js.js",function(err,data){
			if(err){
				console.log("资源不存在");
			}
			res.writeHead(200,{"content-type":"text/html;charset=utf-8"});
			res.end(data);
		});
	}else if(url=="/image"){
		fs.readFile("image.jpg",function(err,data){
			if(err){
				console.log("资源不存在");
			}
			res.end(data);
		});
	}else{
		res.end("404 Not Found.");
	}
});
server.listen(3000,function(){
	console.log("runing......");
})

```

[HTTP Content-type对照表](http://tool.oschina.net/commons)
## 模拟Apache
- `shift+！`可生成html模板
- `readdir`：获取目录列表
  - 获取到的是数组形式的文件列表
- `replace`：替换
- `art-template`
  - `template('data',{files:files});`
  - `{{each files val i}}...{{val}}...{{/each}}`

```javascript
var http = require('http');
var fs = require('fs');
var template = require('art-template');
var server = http.createServer();
server.on('request',(req, res)=>{
	var url = req.url;
	if(url == "/www") {
		fs.readFile("page.html", (err, data)=>{
			if(err) {
				return console.log("error...");
			}
			fs.readdir("C:/Users/Administrator.CFWHR8MI0SO0IW5/Desktop/www", (err, files)=>{
				if(err) {
					return console.log("error...");
				}
				data = template.render(data.toString(), {
					files: files
				});
				res.writeHead(200, {
					"content-type": "text/html;charset=utf-8"
				});
				res.end(data);
			})
		})

	} else {
		res.end('404 Not Found.');
	}
});
server.listen(5000, ()=>{
	console.log('服务器启动了');
})
```

