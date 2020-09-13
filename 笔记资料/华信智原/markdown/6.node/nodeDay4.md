# `node Day4`

## 模块
- 核心模块
  - 用得最多
  - http/fs/url
  - require('模块名称')
- 第三方模块
  - art-template:模板引擎
  - 用之前先安装
  - npm install art-template
  - require('art-template')
- 自定义模块
  - a.js
  - require('./a')

## 模块之间的通信
- 使用exports来公开暴露需要公开的内容
- exports默认是一个共对象，通过exports.add=function(){}方式来公开成员
- 使用直接引入文件，通过.(exports公开成员)来调用公开成员
- var content=require(./a);
- content.add()
- 第二种通信方式
  - module.exports='hello world'
  - var content=require('./a')
  - console.log('content') //hello world
  - 这种暴露方式只能暴露单一成员，重复使用，后面的会覆盖前面的
  - 要暴露多个成员，要使用对象方式

```javascript
var str='hello world'
function add(x,y){
	console.log(x+y)
}
exports.str=str
exports.add=add
/*module.exports={
	str:str,
	add:add
}*/
```
## package.json文件
- 描述项目内容
- 下载并保存文件依赖
- cnpm install art-template --save
- cnpm i --save jquery
- cnpm i bootstrap -S
- denpendencies:依赖
- 自动生成package.json文件
  - cnpm init ——初始化一个package.json文件
  - 安装依赖：cnpm install art-template --save
- 重装依赖文件：cnpm install
- npm会按照package.jon文件依赖自动重装依赖文件

## 第三方包查找机制
- 默认寻找当前目录中是否存在node_modules文件
- 如果找到，会继续找node_modules文件中的art-template文件，然后找package.jon文件，再找该文件中的main属性，通过该属性指定的入口文件找到目标文件
- 如果找不到，会到该目录的上一级目录中寻找node_modules文件，如果还是找不到，就再到上一级目录中查找
- 一直找到磁盘根目录也找不到的话，就会报错
- 所以，我们的node_modules文件最好放在项目根目录下面
- node_modules文件最好只有一个，并且不要随便改该文件目录文件
- package.json 文件名称是固定写法，init自动生成该文件，快捷方式：npm init -y可以直接生成

## npm命令总结
- npmjs.com——npm的网站
- npm -v——查看版本
- npm init -y——快速生成一个package.json 文件
- npm install art-template --save 安装art-template文件并保存依赖信息
- npm install——根据package文件中的依赖信息安装所有依赖模块
- npm install --global npm——升级npm

## express
- koa框架也比较火
- 安装：
  - cnpm init -y
  - cnpm install express --save
  
```javascript
var express=require('express')
var app=express()

app.get('/',(req,res)=>{
	res.send('我是首页')
})

app.get('/about',(req,res)=>{
	res.send('我是关于页')
})

app.get('/news',(req,res)=>{
	res.send('我是新闻页')
})

app.listen(3000,()=>{
	console.log('Runing......')
})
```
## 公开静态资源文件夹
- app.use('/public/',express.static('./public/'))——使用/public/来替代/.public/
- app.use('/a/',express.static('./public'))——使用/a/来替代/.public/
- app.use(express.static('./public'))——直接省略/.public/

## nodemon
- npm install nodemon --global
- 启动服务时使用：nodemon app.js
- 当服务器js文件重新保存时，会自动重启服务器

## 创建项目使用命令总结
- 安装第三方模块
  - cnpm init -y
  - cnpm install express --save
  - cnpm install art-trmplate express-art-trmplate --save
  - cnpm install body-parser --save
- 配置第三方模块
  - 配置art-template
    - app.engine('html', require('express-art-template'))
  - 配置body-parser
    - app.use(bodyParser.urlencoded({ extended: false }))
    - app.use(bodyParser.json())

## URI和URL
- URI统一资源标识符
- URL统一资源定位符