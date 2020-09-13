# `node Day3`

## 原生nodejs实现简单博客页面
```javascript
//引入核心模块
var http=require('http');
var fs=require('fs');
var template=require('art-template');
//创建服务器
http.createServer((req,res)=>{
	var url=req.url;
	if(url=='/'){
		fs.readFile('./views/data.json',(err,content)=>{//读取数据文件
			if(err){
				return res.end('404 error...');
			}			
			fs.readFile('./views/index.html',(err,data)=>{
				if(err){
					return res.end('404 error...');
				}
				res.end(template.render(data.toString(),{
					content:JSON.parse(content).content//拿到的是二进制数据，转成json格式
				}));
			});
		});
	}else if(url=='/post'){
		fs.readFile('./views/post.html',(err,data)=>{
			if(err){
				return res.end('404 error again...');
			}
			res.end(data);
		})
	}else if(url.indexOf('/public/')==0){//公开public目录
		fs.readFile('.'+url,(err,data)=>{
			if(err){
				return res.end('访问的资源不存在');
			}
			res.end(data);
		})
	}else{
		fs.readFile('./views/notFound.html',(err,data)=>{
			if(err){
				return res.end('404 error again...');
			}
			res.end(data);
		})
	}
})
//监听3000端口
.listen(3000,()=>{
	console.log('Server is runing at import 3000.');
});

```
## 临时重定向

```javascript
res.statusCode=302;
res.setHeader('location','/');
res.end();
```

