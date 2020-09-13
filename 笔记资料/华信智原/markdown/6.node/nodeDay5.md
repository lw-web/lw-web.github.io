# `node Day5`

## 使用express搭建服务
- `var express=require('express')`
- `var app=express()`
- `app.get('/',(req,res)=>{...})`
- `app.listen(3000,()=>{console.log('Runing...')})`

## 使用express-art-template
- 安装
  - `npm install --save art-template express-art-template`
- 配置
  - `app.engine('html',require('express-art-template'))`
- 使用
  - `res.render('index.html',{data:data})`

## 使用body-parser
- 安装
  - `npm install body-parser --save`
- 配置
  - `app.use(bodyParser.urlencoded({ extended: false }))`
  - `app.use(bodyParser.json())`
- 使用
  - `req.body`

## 注意细节
- res.end()里面的参数只能写字符串类型，其他的都不可以，包括数值型123
- [art-template](https://aui.github.io/art-template/)
- [express body-parser](https://expressjs.com/en/resources/middleware/body-parser.html)
- [express中文官网](https://expressjs.com/zh-cn/)

## 使用express重写评论案例

```javascript
var express=require('express')
var fs=require('fs')
var bodyParser=require('body-parser')
var app=express()

app.use('/public/',express.static('./public/'))
app.engine('html',require('express-art-template'))
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.get('/',(req,res)=>{
	fs.readFile('./data.json','utf8',(err,data)=>{
		if(err){
			return res.status(500).send('Server error')
		}
		var messages=JSON.parse(data).messages
		res.render('index.html',{
			messages:messages
		})
	})	
})

app.get('/post',(req,res)=>{
	res.render('post.html')
})

app.post('/post',(req,res)=>{
	var message=req.body
	message.time=setTime()	
	fs.readFile('./data.json','utf8',(err,data)=>{
		if(err){
			return res.status(500).send('Server error')
		}
		var messages=JSON.parse(data).messages
		message.id=messages[messages.length-1].id+1
		messages.push(message)
		var fileData=JSON.stringify({
			messages:messages
		})
		fs.writeFile('./data.json',fileData,(err)=>{
			if(err){
				return res.status(500).send('Server error')
			}
			res.redirect('/')
		})
	})	
})

app.get('/delete',(req,res)=>{
	fs.readFile('./data.json','utf8',(err,data)=>{
		if(err){
			return res.status(500).send('Server error')
		}
		var messages=JSON.parse(data).messages
		var deleteId=messages.findIndex(function(item){
			return item.id==req.query.id
		})
		messages.splice(deleteId,1)
		var fileData=JSON.stringify({
			messages:messages
		})
		fs.writeFile('./data.json',fileData,(err)=>{
			if(err){
				return res.status(500).send('Server error')
			}
			res.redirect('/')
		})
	})	
})

app.get('/update',(req,res)=>{
	fs.readFile('./data.json','utf8',(err,data)=>{
		if(err){
			return res.status(500).send('Server error')
		}
		var messages=JSON.parse(data).messages
		var message=messages.find(function(item){
			return item.id==req.query.id
		})
		res.render('update.html',{
			message:message
		})
	})	
})

app.post('/update',(req,res)=>{
	var message=req.body
	message.time=setTime()	
	fs.readFile('./data.json','utf8',(err,data)=>{
		if(err){
			return res.status(500).send('Server error')
		}
		var messages=JSON.parse(data).messages
		var mess=messages.find(function(item){
			return item.id==message.id
		})
		for(var key in message){
			mess[key]=message[key]
		}
		var fileData=JSON.stringify({
			messages:messages
		})
		fs.writeFile('./data.json',fileData,(err)=>{
			if(err){
				return res.status(500).send('Server error')
			}
			res.redirect('/')
		})
	})	
})

app.listen(3000,()=>{
	console.log("Runing......")
})

function setTime() {
    var date = new Date();
    var Y = date.getFullYear() + '-';
    var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
    var D = date.getDate() + ' ';
    var h = date.getHours() + ':';
    var m = date.getMinutes() + ':';
    var s = date.getSeconds();
    return Y+M+D+h+m+s;
}

```
## 实现分离
- app.js
```javascript
var express=require('express')
var router=require('./router.js')
var app=express()

app.use('/public/',express.static('./public/'))

app.use(router)

app.listen(3000,()=>{
	console.log('Runing...')
})

```
- router.js

```javascript
var express=require('express')
var methods=require('./methods.js')
var router=express.Router()

router.get('/',(req,res)=>{
	methods.fun(20,(ret)=>{
		res.send('Hello world! '+ret)
	})	
})

module.exports=router
```
- methods.js

```javascript
exports.fun=function(num,callback){
	num+=10
	callback(num)
}
```
##  路由分离
第一种方式  
- mian1.js
```javascript
var express=require('express')
var router=require('./router1')
var bodyParser=require('body-parser')

var app=express()

app.use('/public/',express.static('./public/'))
app.engine('html',require('express-art-template'))
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

router(app)

app.listen(3000,()=>{
	console.log('Runing...')
})
```
- router1.js

```javascript
var fs=require('fs')

module.exports=function(app){
	app.get('/',(req,res)=>{
		res.send('Hello world!')
	})
}
```
第二种方式
- mian2.js
```javascript
var express=require('express')
var router=require('./router2')
var bodyParser=require('body-parser')

var app=express()

app.use('/public/',express.static('./public/'))
app.engine('html',require('express-art-template'))
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.use(router)

app.listen(3000,()=>{
	console.log('Runing...')
})
```
- router2.js

```javascript
var fs=require('fs')
var express=require('express')
var router=express.Router()

router.get('/',(req,res)=>{
	res.send('Hello world!')
})

module.exports=router
```