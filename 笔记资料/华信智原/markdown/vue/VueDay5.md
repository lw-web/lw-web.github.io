# `Vue Day5`

## 组件传值

### 父组件给子组件传值

- 父组件传值：
  - 使用`v-bind:`属性绑定

```html
<login :fathermsg='fathermsg'></login>
```

- 子组件接收：

```javascript
props:[ 'fathermsg' ]
```

- 调用：

```html
<p>{{fathermsg}}</p>
```

### 父组件向子组件传递方法

- 父组件传递方法：
  - 使用`v-on:`事件绑定

```html
<son @fun='fatherfun'></son>
```

- 子组件触发事件：

```javascript
add(){
    this.$emit('fun')	
}
```

- 元素绑定使用：

```html
<button @click='add'>点我</button>
```

### 子组件向父组件传值

- 子组件传值：

```javascript
data(){
    return {msg:'我是子组件信息'}
},
methods:{
    add(){
        this.$emit('fun',this.msg)	
    }						
}
```

- 父组件接收：

```javascript
data:{
    msg:''
},
methods:{
    fatherfun(data){
        this.msg=data
    }
}
```

- 父组件调用：

```html
<p>{{msg}}</p>
<son @fun='fatherfun'></son>
```

- 子组件触发：

```html
<button @click='add'>点我</button> //事件触发之后，传值才会执行
```

## 获取`DOM`元素

- 获取：

```html
<h1 ref='hb' @click="fun">天气不错</h1>
```

- 使用：

```javascript
fun(){
    this.$refs.hb.innerText='一点都不热'
}
```

## 路由

### `Vue Router`

- 单页面应用：`SPA(single page web application)`单页面应用程序

- 后端路由：所有地址都对应服务器上的资源
- 前端路由：通过`hash(#)`来实现不同页面之间的切换

### 设置默认页面

```javascript
{path:'/',redirect:'/login'}//重定向
```

### 选中项高亮

- 通过给`.router-link-active`添加样式，实现选中项高亮
- 使用`linkActiveClass`自定义属性替代`.router-link-active`

```javascript
router=new VueRouter{
    routes:[],
    linkActiveClass:'muactive'
} 
```

### 路由添加动画

- 使用`transition`标签包裹`router-view`标签

```html
<transition mode='out-in'>
    <router-view></router-view>
</transition>
```

- 设置样式

```css
.v-enter,.v-leave-to{
    opacity: 0;
    transform: translateY(100px);
}
.v-enter-active,.v-leave-active{
    transition: all .5s ease;
}
```

### 路由参数

#### 传参方式一

- 传递参数：

```html
<router-link to='/login?id=10&name=jams'>登录</router-link>
```

- 获取参数：

```javascript
created(){
    console.log(this.$route.query.id)//通过query获取
}
```

#### 传参方式二

- 参数配置：

```javascript
{path:'/register/:id/:name',component:register},
```

- 参数传递：

```html
<router-link to='/register/20/jams'>注册</router-link>
```

- 获取参数：

```javascript
created(){
    console.log(this.$route.params.id)//通过params获取
}
```

## 案例

### 组件传值

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<p>{{msg}}</p>
			<son :fathermsg='fathermsg' @fatherfun='fatherfun'></son>
		</div>
		<template id="son">
			<div>
				<p>{{fathermsg}}</p>
				<button @click="sonfun">点我传值</button>
			</div>			
		</template>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				fathermsg:'我是父组件的信息',
				msg:''
			},
			methods:{
				fatherfun(data){
					this.msg=data
                    console.log('父组件方法被调用')
				}
			},
			components:{
				son:{
					template:'#son',
					data(){
						return {
							sonmsg:'我是子组件的信息'
						}
					},
					methods:{
						sonfun(){
							this.$emit('fatherfun',this.sonmsg)
						}
					},
					props:['fathermsg']
				}
			}
		})
	</script>
</html>
```

### 综合案例

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/bootstrap.min.css"/>
		<style type="text/css">
			.name{
				width: 200px;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<div class="container">
				<fabiao @fun='updatefun'></fabiao>
				<table class="table text-center table-bordered table-striped">
					<tr>
						<td>ID</td>
						<td>姓名</td>
						<td>名言</td>
						<td>时间</td>
					</tr>
					<tr v-for="list in lists" :key='list.id'>
						<td>{{list.id}}</td>
						<td>{{list.name}}</td>
						<td>{{list.say}}</td>
						<td>{{list.time|time}}</td>
					</tr>
				</table>	
			</div>			
		</div>
		<template id="fabiao">
			<div>
				<div class="panel panel-default">
				    <div class="panel-body text-center bg-success">
				    	<h1>添加名言</h1>
				    </div>
				</div>	
				<div class="form-group form-inline">
					<label for="">
						姓名:	<input type="text" v-model="name" class="name form-control" v-focus/>
					</label>
				</div>
				<div class="form-group">
					<label for="">
						人生信条:	<textarea cols="150" rows="5" v-model="say" class="form-control" @keyup.enter='add'></textarea>
					</label>				
					<button class="btn btn-primary" @click="add">添加</button>	
				</div>
			</div>
		</template>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var fabiao={
			template:'#fabiao',
			data(){
				return {
					name:'',
					say:''
				}
			},
			methods:{
				add(){
					var list={id:Date.now(),name:this.name,say:this.say,time:Date.now()}
					var lists=JSON.parse(localStorage.getItem('message')||'[]')
					lists.push(list)
					localStorage.setItem('message',JSON.stringify(lists))
					this.$emit('fun')
					this.name=this.say=''
				}
			},
			directives:{
				focus:{
					inserted(el){
						el.focus()
					}
				}
			}
		}	
		var vm=new Vue({
			el:'#app',
			data:{
				lists:[]
			},
			methods:{
				updatefun(){
					var data=JSON.parse(localStorage.getItem('message')||'[]')
					this.lists=data
				}
			},
			created(){
				this.updatefun()
			},
			components:{
				fabiao
			},
			filters:{
				time(date){
					var date=new Date(date)
					var y=date.getFullYear()
					var m=(date.getMonth()+1).toString().padStart(2,'0')
					var d=date.getDate().toString().padStart(2,'0')
					var h=date.getHours().toString().padStart(2,'0')
					var mm=date.getMinutes().toString().padStart(2,'0')
					var s=date.getSeconds().toString().padStart(2,'0')
					return `${y}-${m}-${d}  ${h}:${mm}:${s}`
				}
			}
		})		
	</script>
</html>
```

### 基本路由

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<router-link to='/login'>登录</router-link>
			<router-link to='/register'>注册</router-link>
			<router-link to='/logout'>退出</router-link>
			<router-view></router-view>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/vue-router.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var login={
			template:'<h1>Login</h1>'
		}
		var register={
			template:'<h1>Register</h1>'
		}
		var logout={
			template:'<h1>Logout</h1>'
		}
		var router=new VueRouter({
			routes:[
				{path:'/login',component:login},
				{path:'/register',component:register},
				{path:'/logout',component:logout}
			]
		})
		var vm=new Vue({
			el:'#app',
			router
		})
	</script>
</html>
```

### 路由动画

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			.myactive{
				background-color: yellow;
				color: red;
			}
			.v-enter,.v-leave-to{
				opacity: 0;
				transform: translateY(100px);
			}
			.v-enter-active,.v-leave-active{
				transition: all .5s ease;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<router-link to="/login">登录</router-link>
			<router-link to="/register">注册</router-link>
			<router-link to="/logout">退出</router-link>
			<transition mode='out-in'>
				<router-view></router-view>
			</transition>			
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/vue-router.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var login={
			template:'<h1>Login</h1>'
		}
		var register={
			template:'<h1>Register</h1>'
		}
		var logout={
			template:'<h1>Logout</h1>'
		}
		var router=new VueRouter({
			routes:[
				{path:'/',redirect:'/login'},
				{path:'/login',component:login},
				{path:'/register',component:register},
				{path:'/logout',component:logout}
			],
			linkActiveClass:'myactive'
		})
		var vm=new Vue({
			el:'#app',
			router
		})
	</script>
</html>
```

### 路由传参

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<router-link to='/login?msg=Tuesday'>登录</router-link>
			<router-link to='/register/Tuesday'>注册</router-link>
			<router-view></router-view>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/vue-router.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var login={
			template:'<h1>Login---{{msg}}</h1>',
			data(){
				return {msg:''}
			},
			created(){
				this.msg=this.$route.query.msg
			}
		}
		var register={
			template:'<h1>Register---{{msg}}</h1>',
			data(){
				return {msg:''}
			},
			created(){
				this.msg=this.$route.params.msg
			}
		}
		var router=new VueRouter({
			routes:[
				{path:'/login',component:login},
				{path:'/register/:msg',component:register}
			],
			linkActiveClass:'myactive'
		})
		var vm=new Vue({
			el:'#app',
			router
		})
	</script>
</html>
```











