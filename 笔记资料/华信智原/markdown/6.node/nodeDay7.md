# `node Day7`

## `find`方法

`find()`会有一个返回值

- 拿到你需要的那一项
- 拿不到会返回`undefined`

```javascript
var arr=[1,{"name":"张无忌"},true,"helloworld"]
for(var i=0;i<arr.length;i++){
    console.log(arr[i])//遍历数组元素
    if(arr[i]=="helloworld"){
        console.log(arr[i])//helloworld
    }
}
var item=arr.find(function(item){
    return item=="helloworld"
})
console.log(item)//helloworld
var item1=arr.find(item=>item==1)//只有一个参数时，()可以省略，只有一个返回值时return和{}也可以省略
console.log(item1)//1
```

## `findIndex`方法

返回对应项的下标

```javascript
var index=arr.findIndex(function(item){
    return item=="helloworld"
})
console.log(index)//3拿到的是对应项的下标
```

## 箭头函数

- 简化代码

- 改变`this`指向，永远指向离他最近的那个对象
- 参考文档：[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## 模块化

### node服务端模块化

`commonjs`规范：

- 暴露模块：`exports`、`module.exports`
- 加载模块：`require`

### 浏览器端模块化

- 使用`script`标签引入js文件
- `AMD（require.js）`和`CMD（sea.js）`第三方包，非官方指定标注
- `ES6`中的模块化`API`，官方指定标志

## `mongodb`

### 数据库类型

`mysql`属于关系型数据库

`mongodb`属于非关系型数据库

### 安装

- 全部下一步，最后一个不要勾选

- 配置环境变量

- `cmd`输入`mongod --version`
- 手动创建`data/db`文件目录
- 启动数据库`mongod`

- 默认端口是：27017

### 数据库操作

#### 连接、退出

- 连接数据库：重开一个`git`窗口`mongo`回车
- 退出`exit`

#### 基本命令

- `show dbs`查看所有数据库
- `db`查看当前正在操作数据库
- `use+数据库名`创建数据库
- `db.student.insertOne({"name":"张三"})`插入数据
- `show collections`查看集合
- `db.student.find()`查看数据

## `mongoose`

### 安装引入

- [mongoose官网](https://mongoosejs.com/)

- 安装`npm install mongoose --save`

- 引入`var mongoose=require('mongoose')`

- 连接数据库`mongoose.connect('mongodb://localhost:27017/student')`
  - 没有的数据库会自动新建
- 设计数据模型`var Cat=mongoose.model('Cat',{name:String})`
  - 大写的单数字符串，将来会自动转成小写复数作为数据集合名

- 创建数据`var kitty=new Cat({name:"kitty"})`
- 保存数据

```javascript
kitty.save(err=>{
    if(err){
        console.log(err)
    }else{
        console.log('success')
    }
})
```

### 基本使用案例

- 数据库初步使用完整过程

```javascript
var mongoose=require('mongoose')

mongoose.connect('mongodb://localhost:27017/liwei')

var Cat=mongoose.model("Cat",{
	name:String
})
var kitty=new Cat({name:"kitty"})
kitty.save(function(err){
	if(err){
		console.log(err)
	}else{
		console.log("success")
	}
})
```

### `mongodb`结构

- 数据对象的集合
- 数据库-->集合（数组）-->文档（对象）

## 数据结构设计

### 连接数据库

```javascript
var mongoose=require('mongoose')
mongoose.connect('mongodb://localhost:27017/数据库名',{ useNewUrlParser: true})
```

### 设计`Schema`模型

```javascript
var Schema=mongoose.Schema
var blogSchema=new Schema({
    title:String,
    author:String,
    body:String,
    comments:{
        type:String,
        required:true,
        default:"hello world"
    }
})
```

### 发布`Schema`数据模型

```javascript
var Blog=mongoose.model('Blog',blogSchema)
```

### 使用模型创建数据

```javascript
var blog1=new Blog({
    title:'天气',
    author:'李伟',
    body:'你好世界'
})
```

### 保存创建数据

```javascript
blog1.save(err=>{
    if(err){
		console.log(err)
	}else{
		console.log("success")
	}
})
```

### 查看数据

```shell
mongo：链接数据库
use liwei：切换到liwei数据库
show collections：显示数据集合
db.cats.find()：查找数据集合中所有数据
```

### 案例

```javascript
//引入mongoose
var mongoose=require('mongoose')
//连接数据库
mongoose.connect('mongodb://localhost:27017/data',{ useNewUrlParser: true})
//引入Schema
var Schema=mongoose.Schema
//设计Schema
var dataSchema=new Schema({
	name:{
		type:String,
		required:true
	}
})
//发布Schema模型
var User=mongoose.model('User',dataSchema)
//创建数据
var user1=new User({
	name:"李伟"
})
//保存数据
user1.save(err=>{
	if(err){
		console.log(err)
	}else{
		console.log('sucess')
	}
})

```

## 数据库基本操作

### 数据库操作流程

- 引入`mongoose`

```javascript
var mongoose=require('mongoose')
```

- 连接数据库

```javascript
mongoose.connect('mongodb://localhost:27017/数据库名',{ useNewUrlParser: true})
```

- 设计表结构

```javascript
//引入Schema
var Schema=mongoose.Schema
//设计Schema
var dataSchema=new Schema({...})
```

- 发布为模型

```javascript
var User=mongoose.model('User',dataSchema)
```

- 操作数据（增删改查）

### 插入数据

- `save`方法

```javascript
user1.save(err=>{
    if(err){
        console.log(ee)
    }else{
        console.log('sucess')
    }
})
```

### 查找数据

#### 查找所有数据

- `find`方法

```javascript
User.find((err,ret)=>{
    if(err){
        console.log(err)
    }else{
        console.log(ret)
    }
})
```

#### 条件查找数据

```javascript
User.find({
    name:"张三"
},(err,ret)=>{
    if(err){
        console.log(err)
    }else{
        console.log(ret)
    }    
})
```

- `find`方法找到的结果即使只有一个也会以数组形式返回结果`[{...},{...}...]`

#### 查找单个数据

- `findOne`方法

```javascript
User.findOne({
    name:"张三"
},(err,ret)=>{
    if(err){
        console.log(err)
    }else{
        console.log(ret)
    }    
})
```

- 只返回匹配的第一项，以对象形式返回结果`{...}`

### 删除数据

- `remove`方法

```javascript
User.remove({
    name:"张三"
},err=>{
    if(err){
        console.log(err)
    }else{
        console.log('sucess')
    }
})
```

### 修改数据

- `findByIdAndUpdate`方法

```javascript
User.findByIdAndUpdate("id",{
    name:"李四"
},err=>{
    if(err){
        console.log(err)
    }else{
        console.log('sucess')
    }
})
```

## 回调地狱

### `callback hell`

- 异步的JavaScript程序，或者说使用了回调函数的JavaScript程序，要想控制执行顺序，必须通过多层嵌套的方式实现，但是这样的嵌套的代码阅读起来晦涩难懂，并不直观，难以维护

### `promise`

- `promise`是`ES6`提供的一个`API`
- `promise`是一个构造函数
- `promise`里面有一个异步任务，返回结果有两种情况`resolve`或`reject`

```javascript
var p1=new Promise(function(resolve,reject){
    fs.readFile('./a.txt',(err,data)=>{
        if(err){
            reject(err)//调用p1的then的第二个形参函数
        }
        resolve(data)//调用p1的then的第一个形参函数
    })
})
var p2=new Promise(function(resolve,reject){
    fs.readFile('./b.txt',(err,data)=>{
        if(err){
            reject(err)//调用p2的then的第二个形参函数
        }
        resolve(data)//调用p2的then的第一个形参函数
    })
})
p1.then(function(data){
    	console.log(data)//p1的resolve传递过来的参数
    	return p2
	},function(err){
    	console.log(err)//p1的reject传递过来的参数
	})
	.then(function(data){
         console.log(data)//p2的resolve传递过来的参数
	})
```

### 案例

```javascript
var fs=require('fs')

function fun(path){
	var p=new Promise((resolve,reject)=>{
		fs.readFile(path,'utf8',(err,data)=>{
			if(err){
				reject(err)
			}
			resolve(data)
		})
	})
	return p
}

var p1=fun('./data/a.txt')
var p2=fun('./data/b.txt')
var p3=fun('./data/c.txt')
var p4=fun('./data/d.txt')

p1
	.then(data=>{
		console.log(data)
		return p2
	})
	.then(data=>{
		console.log(data)
		return p3
	})
	.then(data=>{
		console.log(data)
		return p4
	})
	.then(data=>
        console.log(data)
	)
```

### `ES6`参考文档

- [阮一峰ES6](http://es6.ruanyifeng.com/#docs/destructuring)

## `mongodb`版`goods`案例

### `app.js`

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

### `router.js`

```javascript
var express=require('express')
var fs=require('fs')
var model=require('./goodModel.js')

var router=express.Router()

router.get('/',(req,res)=>{
	model.find((err,goods)=>{
		if(err){
			return res.status(500).send('Server Error')
		}
		res.render('index.html',{
			goods:goods
		})
	})
})

router.get('/add',(req,res)=>{
	res.render('add.html')
})

router.post('/add',(req,res)=>{
	new model(req.body).save(err=>{
		if(err){
			return res.status(500).send('Server Error')
		}
		res.redirect('/')
	})
})

router.get('/delete',(req,res)=>{
	var id=req.query.id.replace(/"/g,"")
	model.findByIdAndRemove(id,err=>{
		if(err){
			return res.status(500).send('Server Error')
		}
		res.redirect('/')
	})
})

router.get('/update',(req,res)=>{
	var id=req.query.id.replace(/"/g,"")
	model.findById(id,(err,good)=>{
		if(err){
			return res.status(500).send('Server Error')
		}
		res.render('update.html',{
			good:good
		})
	})
})

router.post('/update',(req,res)=>{
	var id=req.body.id.replace(/"/g,"")
	model.findByIdAndUpdate(id,req.body,err=>{
		if(err){
			return res.status(500).send('Server Error')
		}
		res.redirect('/')
	})
})

module.exports=router

```

### `goodModel.js`

```javascript
var mongoose=require('mongoose')

mongoose.connect('mongodb://localhost:27017/goodsData',{ useNewUrlParser: true})

var Schema=mongoose.Schema
var goodSchema=new Schema({
	brand:{
		type:String,
		required:true
	},
	model:{
		type:String,
		required:true
	},
	price:{
		type:Number,
		required:true
	}
})

var goodModel=mongoose.model('Good',goodSchema)

module.exports=goodModel

```

