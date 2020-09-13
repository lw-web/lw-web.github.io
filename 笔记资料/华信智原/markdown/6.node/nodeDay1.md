# `node Day1`

## 命令行

- `cmd`、终端、小黑屏、`shell`
- 打开方式：`window+R`

### 常用指令
- `dir`：展示`user/admin`下面的文件目录
- `cd desktop`：回到桌面
- `d：`——切换到d盘
- `write`——写字板
- `mspaint`——画图板

[cmd常用指令](https://www.cnblogs.com/accumulater/p/7110811.html)
### git
- `dir`
- 在哪里打开路径就在那里

### 常用命令
- `md：liwei`——创建文件夹
- `cd ../`——回到上一级目录
- `rd liwei`——删除文件
- `table`键有提示功能

### 环境变量
- `path`：文件路径名，中间以`;`隔开
- 重启命令行就行了

## nodeJS
- 在服务器端运行JavaScript的开放源代码、跨平台`JavaScript`运行环境
- 采用谷歌开发的V8引擎运行JS代码，使用事件驱动、非阻塞和异步I/O（输入/输出）模型等技术来提高定能，可优化应用程序的传输量和规模。
- 模块：工具——文件读取、HTT模块等
- `nodejs.org`
- 命令行输入：`node`就进入`node`交互环境了，退出使用`ctrl+c`，连按两次
- `node --vision`

### node服务器
- 单线程：对硬件要求比较低，适合小项目
- 没有`DOM`和`BOM`，只有`ECMAScript`相同
- 提供了一些服务器级别的API
- 操作文件、网络服务搭建、网络通信等等
- `highcharts`：图标插件
- `js`引擎：解析`JS`最快的引擎 

### node编写
- `ctrl+shfit`+右键，打开命令行

### node 文件模块
- `require（）`——引入模块的方法
- `var fs=require('fs');`——引入文件模块；
- `fs.readFile('../data/data.txt',function (error,data){console.log(data);})`
  - 参数一文件路径；参数二回调函数，回调函数参数一error，函数第二个参数data。
  - 如果读取失败：`error`就是错误对象，`data`就是`undefined`；
  - 如果都区成功：`error`就是`null`，`data`就是读取到的数据（文件——二进制——十六进制然后输出）
  - 想要得到能看懂的数据，使用`.toString();`方法
- 上下方向键能够调出我们输入过的命令
- `cls`——清除屏幕内容（`git`清屏使用`clear`）

### 文件写入
- `fs.writeFile('../data/write.txt','我的第一个node程序',function(error){console.log(error);})`
  - 参数一：写入文件路径
  - 参数二：写入内容
  - 参数三：回调函数
  - 如果写入成功，`error`就是`null`；如果写入失败，`error`就是错误对象。
  - `if(error){console.log('写入失败，检查原因')}else{console.log('写入成功');}`

```javascript
var fs=require('fs');
fs.readFile('../data/write.html',function(error,data){
	if(error){
		console.log('文件读取失败');
	}else{
		console.log('文件读取成功，文件内容为：'+data.toString());
	}
});
fs.writeFile('../data/write.html','<p>hello world</p>',function(error){
	if(error){
		console.log('写入失败，失败原因：'+error);
	}else{
		console.log('写入成功');
	}
});
```

### 创建服务器
- 服务器模块：`http`
- `var http=require('http');`
- `var sever=http.createSever();`
- `request`:请求事件
- `sever.on('request',function(request,response){console.log('请求收到了')})`
- 参数一：请求事件；参数二：回调函数（参数一：请求信息，参数二：响应信息）
- `response.end('心情很好');`
- 端口号：`sever.listen(3333,function(){console.log('服务器已经建好了，端口号是3333')})`
- `127.0.0.1:3333(127.0.0.1——本地服务器)`

```javascript
var http=require('http');
var sever=http.createServer();
sever.listen(3333,function(){
	console.log('服务器搭建好了，请访问');
})
sever.on('request',function(request,response){
	console.log('请求收到了');
	response.end('心情不错');	
})
```
### 服务器增强版
```javascript
var http=require('http');//请求http模块
var server=http.createServer();//创建服务器
server.on('request',function(req,res){//请求事件，当请求事件发生时执行函数
	console.log('请求收到了');
	res.writeHead(200,{'content-type':'text/html;charset=utf8'})//设置响应字符集
	res.write('<h1>你好</h1>');
	res.write('<h2>你好得很</h2>');
	res.end('结束了');//结束服务器输出
	
})
server.listen(4444,function(){//创建服务器端口号
	console.log('服务器建好了，请访问')
})

```
### request参数
- `req.url`返回的是域名和端口号后面的内容
- 实现页面跳转功能
- 路由：

### npm
- `npm`是随着node一起安装的
- `npm install -g cnpm --registry=https://registry.npm.taobao.org`——配置cmd到淘宝镜像
- 安装软件：`cnpm install jquery@3`

### supervisor小工具
- `supervisor` 文件名`.js`执行

[B站讲师笔记](https://nodejs.lipengzhou.com/00-course_introduction.html#学什么)