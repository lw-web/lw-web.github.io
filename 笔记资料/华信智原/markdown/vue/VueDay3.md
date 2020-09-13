# `Vue Day3` 

## 生命周期钩子函数

生命周期：从创建到销毁的整个过程。

==生命周期钩子函数中不要使用箭头函数，因为箭头函数会改变`this`指向。==

### 创建阶段

#### `beforeCreate`

- 实例中的`data`、`methods`等成员被创建之前
- 在这个钩子函数中，还访问不到`data`、`methods`等成员的信息

#### `created`

- 实例中的`data`、`methods`等成员已经创建完成
- 在这个钩子函数中，已经能够访问`data`、`methods`等成员的信息了

#### `beforeMount`

- 模板已经在内存中编译好了，但还没有挂在都页面中，页面中的内容还是原本的模板字符串

#### `mounted`

- 模板已经挂载到页面上，页面中的内容已经更新完成了

### 运行阶段

#### `beforeUpdate`

- 数据已经发生改变，但是页面内容还没有更新

#### `updated`

- 页面内容已经更新完成

### 销毁阶段

#### `befoerDestroy`

- 实例被销毁之前，在这个钩子函数中实例中的`data`、`methods`等成员还可以访问得到

#### `destroyed`

- 实例已经完全销毁，实例中的成员全部都访问不到了

![vue生命周期](assets/lifecycle.png)

## `vue`中的`ajax`实现

- `vue`中实现`ajax`请求的第三方包

### `vue-resource`安装、引入

- 必须先引入`vue.js`，因为`vue-resource`是基于`vue.js`的

### 请求

#### `get`请求

```javascript
this.$http.get('url').then(sucessCallback,errCallback)
```

- 通过`vue-resource`获取的结果一般都在`result.body`中存放数据

#### `post`请求

```javascript
this.$htpp.post('url',{data},{emulateJSON: true}).then(sucessCallback,errCallback)
```

#### `jsonp`请求

```javascript
this.$http.get('url').then(sucessCallback,errCallback)
```

- 除了 `vue-resource` 之外，也可以使用 `axios` 的第三方包实现实现数据的请求

- [axios参考文档](![img](file:///C:\Users\Administrator.CFWHR8MI0SO0IW5\AppData\Roaming\Tencent\QQ\Temp\%W@GJ$ACOF(TYDYECOKVDYB.png)https://www.kancloud.cn/yunye/axios/234845)

## 案例

### 通过`jsop`获取淘宝数据

#### 方案一

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<!--通过v-model动态获取输入数据-->
			输入内容：<input type="text" v-model="keywords" />
			<!--用requireData(keywords)方法返回的动态数据更新页面-->
			<ul v-for="list in requireData(keywords)">
				<li>{{list}}</li>
			</ul>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/vue-resource.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm = new Vue({
			el: '#app',
			data: {
				keywords: '',
				arr:[]
			},
			methods: {
				requireData(keywords) {
					if(keywords==''){
						return this.arr=[]//关键字为空的时候，清空arr数组
					}
					var _this = this//箭头函数会改变this指向，预先保存
					this.$http.jsonp('https://suggest.taobao.com/sug?q='+keywords+'&callback=haha').then(ret=>{
						haha(ret.body.result)//通过回调函数返回异步访问数据
					})
					function haha(data) {//处理拿到的异步返回结果
						_this.arr = []//每次给arr遍历添加成员之前先清空
						data.forEach(item => {
							_this.arr.push(item[0])
						})
					}
					return this.arr
				}				
			}
		})
	</script>
</html>
```

#### 方案二

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/vue-resource.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app">
			<input type="text" v-model="keywords" @input="requireData"/>
			<ul v-for="list in lists" :key="list.id">
				<li>{{list[0]}}</li>
			</ul>
		</div>		
	</body>	
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				keywords:'',
				lists:''
			},
			methods:{
				requireData(){
					this.$http.jsonp('https://suggest.taobao.com/sug?q='+this.keywords+'&callback=haha').then(function(ret){
						this.lists=ret.body.result
					})
				}
			}
		})
	</script>
</html>
```

### 手写实现`jsonp`

- 客户端：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body></body>
	<script type="text/javascript">
		function show(data){
			console.log(data)
		}
	</script>
	<script src="http://127.0.0.1:3000/?callback=show"></script>
</html>
```

- 服务器端：

```javascript
var http=require('http')
var url=require('url')

var server=http.createServer()

server.on('request',function(req,res){
	var obj=url.parse(req.url,true)
	var pathname=obj.pathname
	if(pathname=='/'){
		var data={
			name:'xjj',
			age:18,
			gender:'女孩子'
		}
		var scriptStr=`${obj.query.callback}(${JSON.stringify(data)})`
		res.end(scriptStr)
	}else{
		res.end('404')
	}	
})

server.listen(3000,function(){
	console.log('Runing...')
})
```

