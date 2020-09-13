# `node Day6`

## 修改操作

修改流程：

- ==唯一的标识符ID==
- 获取到点击项的ID
- 通过读取文件找到==原文件中ID和点击项ID相同的那一项==数据
- 将拿到的数据渲染到`edit.html`文件中
- 在`edit.html`中修改数据信息，然后提交
- 读取源文件，用提交的==数据替换==原文件中的数据
- 将修改后的数据==重新写入==数据文件
- 跳转到首页，重新渲染列表页

修改操作：

- 获取点击项id：
  - 通过a标签跳转地址后面拼接`?id={{val.id}}`的方式传递id
  - 通过`req.query.id`获取问号后拼接的id信息

- 获取原文件相同id的数据项：
  - 读取原文件信息

```javascript
fs.readFile('./data.json',function(err,data){
    var goods=JSON.parse(data.toString()).goods//获取到的goods是一个数组
})
```

​		遍历，找到原文件中相同id的数据项

```javascript
var good=goods.find(function(item){
    return item.id==id//这个id是通过点击获取到的
})
```

​		`find`ES6中的新的数组方法

```javascript
var arr=[12,34,56,89]
var myItem=arr.find(item=>{//只有一个参数时（）可以省略
    return item>78//返回大于78的那一项
})
console.log(myItem)//89
```

- 将拿到的数据信息渲染到`edit.html`页面中

```javascript
res.render('edit.html',{
    good:good//查找到的数据项
})
```

- `edit.html`页面设置

```javascript
//通过value值渲染需要修改的数据信息
value="{{good.id}}"
value="{{good.pingpai}}"
value="{{good.xinghao}}"
value="{{good.jiage}}"
```

- post方式提交修改后的信息

```javascript
router.post('/edit',(req.res)=>{
    var good=req.body    
})
```

- 将提交的信息重新写入数据文件

```javascript
fs.readFile('./data.json',function(err,data){//读取原文件
    var goods=JSON.parse(data.toString()).goods//获取到的goods是一个数组
    var item=goods.find(function(item){//找到修改项
        return item.id==good.id
    })
    for(var key in good){//替换修改信息
        item[key]=good[key]
    }
    var fileData=goods.JSON.stringify({//将数组转换成字符串型
        goods:goods
    })
    fs.writeFile('./dada.json',fileData,err=>{//将数据重新写入原文件
        if(err){
            return res.status(500).send('Server Error')
        }
        redirect('/')//重定向到首页，更新渲染首页
    })
})
```

- 注意细节：表单设置disabled之后提交是获取不到数据内容的

## 删除操作

删除流程：

- 根据用户点击传递的id，找到原文件中的对应项
- 删除对应项并保存数据到原文件
- 跳转到列表页

删除操作：

```javascript
router.get('/delete',(req,res)=>{
    var deleteId=req.query.id
    fs.readFile('./data.json',function(err,data){
        var goods=JSON.parse(data.toString()).goods//获取到的goods是一个数组
        var index=goods.findIndex(item=>{
            return item.id==deleteId
        })
        goods.splice(index,1)
        var fileData=JSON.stringify({
            goods:goods
        })
        fs.writeFile('./data.json',fileData,err=>{
            if(err){
                return res.status(500).send('Server Error')
            }
            res.redirect('/')
        })
    })
})
```

## 完整项目

- `app.js`文件

```javascript
var express=require('express')
var bodyParser=require('body-parser')
var router=require('./router')

var app=express()

app.use('/public/',express.static('./public/'))
app.use('/node/',express.static('./node_modules/'))
app.engine('html',require('express-art-template'))
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.use(router)

app.listen(3000,()=>{
	console.log('Runing...')
})
```

- `router.js`文件

```javascript
var express=require('express')
var method=require('./method')

var router=express.Router()

router.get('/',(req,res)=>{
	method.read((err,goods)=>{
		method.err(err)
		res.render('index.html',{
			goods:goods
		})
	})	
})

router.get('/add',(req,res)=>{
	res.render('add.html')
})

router.post('/add',(req,res)=>{
	method.read((err,goods)=>{
		method.err(err)		
		method.add(req.body,goods,(err)=>{
			method.err(err)
			res.redirect('/')
		})
	})
})

router.get('/update',(req,res)=>{
	method.find(req.query.id,(err,good)=>{
		method.err(err)
		res.render('update.html',{
			good:good
		})
	})
})

router.post('/update',(req,res)=>{
	method.update(req.body,err=>{
		method.err(err)
		res.redirect('/')
	})
})

router.get('/delete',(req,res)=>{
	method.delete(req.query.id,err=>{
		method.err(err)
		res.redirect('/')
	})
})

module.exports=router
```

- `method.js`文件

```javascript
var fs=require('fs')

var dbPath='./db.json'

exports.read=function(callback){
	fs.readFile(dbPath,(err,data)=>{
		if(err){
			callback(err)
		}
		callback(null,JSON.parse(data.toString()).goods)
	})
}

exports.add=function(good,goods,callback){
	if(goods[goods.length-1]){
		good.id=goods[goods.length-1].id+1
	}else{
		good.id=1
	}		
	goods.push(good)
	var fileData=JSON.stringify({
		goods:goods
	})
	fs.writeFile(dbPath,fileData,(err)=>{
		if(err){
			callback(err)
		}
		callback(null)
	})
}

exports.find=function(id,callback){
	fs.readFile(dbPath,(err,data)=>{
		if(err){
			callback(err)
		}
		callback(null,JSON.parse(data.toString()).goods.find(item=>{
			return item.id==parseInt(id)
		}))
	})
}

exports.update=function(dataObj,callback){
	fs.readFile(dbPath,(err,data)=>{
		if(err){
			callback(err)
		}
		var goods=JSON.parse(data.toString()).goods
		var good=goods.find(item=>{
			return item.id==parseInt(dataObj.id)
		})
		for(var key in dataObj){
			good[key]=dataObj[key]
		}
		var fileData=JSON.stringify({
			goods:goods
		})
		fs.writeFile(dbPath,fileData,err=>{
			if(err){
				callback(err)
			}
			callback(null)
		})
	})
}

exports.delete=function(id,callback){
	fs.readFile(dbPath,(err,data)=>{
		if(err){
			callback(err)
		}
		var goods=JSON.parse(data.toString()).goods
		var index=goods.findIndex(item=>{
			return item.id==id
		})
		goods.splice(index,1)
		var fileData=JSON.stringify({
			goods:goods
		})
		fs.writeFile(dbPath,fileData,err=>{
			if(err){
				callback(err)
			}
			callback(null)
		})
	})
}

exports.err=function(err){
	if(err){
		return res.status(500).send('Server Error')
	}
}
```

- `index.html`文件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="node/bootstrap/dist/css/bootstrap.css"/>
		<style type="text/css">
			a{
				margin-bottom: 10px!important;
			}
		</style>
	</head>
	<body>
		<div class="container">
			<div class="panel panel-default">
			    <div class="panel-body">
			    	<h1 class="text-center">商品列表页</h1>
			    </div>
			</div>
			<a href="/add" class="btn btn-info">添加商品</a>
			<table class="table table-bordered text-center">
				<thead>
					<tr>
						<th class="text-center">品牌</th>
						<th class="text-center">型号</th>
						<th class="text-center">价格</th>
						<th class="text-center">编辑</th>
					</tr>
				</thead>
				<tbody>
					{{each goods val i}}
					<tr>
						<td>{{val.brand}}</td>
						<td>{{val.model}}</td>
						<td>{{val.price}}</td>
						<td>
							<a href="delete?id={{val.id}}" class="btn btn-success">删除</a>
							<a href="update?id={{val.id}}" class="btn btn-success">修改</a>
						</td>
					</tr>
					{{/each}}
				</tbody>
			</table>
		</div>
	</body>
</html>
```

- `add.html`文件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="node/bootstrap/dist/css/bootstrap.css"/>
		<style type="text/css">
			a{
				margin-bottom: 10px!important;
			}
		</style>
	</head>
	<body>
		<div class="container">
			<div class="panel panel-default">
			    <div class="panel-body">
			    	<h1 class="text-center">商品添加页</h1>
			    </div>
			</div>			
			<a href="/" class="btn btn-info">返回列表页</a>
			<form action="/add" method="post">
				<div class="form-group">
					品牌：
					<input type="text" name="brand" class="form-control"/>
				</div>
				<div class="form-group">
					型号：
					<input type="text" name="model" class="form-control"/>
				</div>
				<div class="form-group">
					价格：
					<input type="number" name="price" class="form-control"/>
				</div>
				<input type="submit" value="保存" class="btn btn-success" />
			</form>
		</div>
	</body>
</html>
```

- `update.html`文件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="node/bootstrap/dist/css/bootstrap.css"/>
		<style type="text/css">
			a{
				margin-bottom: 10px!important;
			}
		</style>
	</head>
	<body>
		<div class="container">
			<div class="panel panel-default">
			    <div class="panel-body">
			    	<h1 class="text-center">商品添加页</h1>
			    </div>
			</div>			
			<a href="/" class="btn btn-info">返回列表页</a>
			<form action="/update" method="post">
				<input type="hidden" name="id" value="{{good.id}}" />
				<div class="form-group">
					品牌：
					<input type="text" name="brand" value="{{good.brand}}" class="form-control"/>
				</div>
				<div class="form-group">
					型号：
					<input type="text" name="model" value="{{good.model}}" class="form-control"/>
				</div>
				<div class="form-group">
					价格：
					<input type="number" name="price" value="{{good.price}}" class="form-control"/>
				</div>
				<input type="submit" value="确认修改" class="btn btn-success" />
			</form>
		</div>
	</body>
</html>
```

