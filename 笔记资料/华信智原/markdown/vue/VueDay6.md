# `Vue Day6`

## 路由嵌套

- 在路由匹配规则中，使用`children`属性配置子路由

```javascript
{
    path:'/login',
    component:login,
    children:[
        {path:'qq',component:qq},//这里不需要再写'/login/'
        {path:'tel',component:tel}//也不能写成‘/tel’，因为‘/’会默认跳转到根路径
    ]
}
```

- 子路由的切换、展示要在父路由中实现

```html
<template id='login'>
    <div>
        <h1>Login</h1>
        <router-link to='/login/qq'>登录QQ验证</router-link>
        <router-link to='/login/tel'>登录手机验证</router-link>
        <router-view></router-view>
    </div>
</template>
```

## 组件布局

- 定义组件：

```java
const router=new VueRouter({
    routes:[
        {
            path:'/',
            components:{
                'default':header,
                'left':left,
                'right':right,
                'footer':footer
            }
        }
    ]
})		
```

- 使用`name`属性展示组件：

```html
<router-view></router-view>
<div class="container">
    <router-view name='left'></router-view>
    <router-view name='right'></router-view>
</div>			
<router-view name="footer"></router-view>
```

## 拼接字符串

### `methods`方式

```javascript
methods:{
    fun(){
        this.fullname=this.firstname+'-'+this.lastname
    }
}
```

### `watch`方式

```javascript
watch:{
    'firstname':function(newVal,oldVal){
        this.fullname=newVal+'-'+this.lastname
    },
    'lastname':function(newVal,oldVal){
        this.fullname=this.firstname+'-'+newVal
    }
}
```

### `comouted`方式

```javascript
computed:{
    'fullname':function(){//在data中就不能再定义这个属性了
        return this.firstname+'-'+this.lastname
    }
}
```

### 三种方式对比

- `computed`属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算，主要当作属性来使用

- `methods`方法表示一个具体的操作，主要书写业务逻辑

- `watch`一个对象，键是需要观察的表达式，值是对应回调函数
  - 主要用来监听某些==特定数据==（比如`url`）的变化，从而进行某些具体的业务逻辑操作
  - 可以看作是`computed`和`methods`的结合体

 ## `webpack`

- 安装`webpack`和`webpack-cli`

```shell
cnpm install webpack webpack-cli --save-dev
```

- 打包编译文件

```shell
webpack ./mian.js -o ../dist/bundle.js
```

## 案例

### 路由嵌套

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<router-link to="/login">Login</router-link>
			<router-link to="/register">Register</router-link>
			<router-view></router-view>
		</div>
		<template id='login'>
			<div>
				<h1>Login</h1>
				<router-link to='/login/qq'>登录QQ验证</router-link>
				<router-link to='/login/tel'>登录手机验证</router-link>
				<router-view></router-view>
			</div>
		</template>
		<template id='register'>
			<div>
				<h1>Register</h1>
			</div>
		</template>
		<template id="qq">
			<div>
				<h2>QQ验证</h2>
			</div>
		</template>
		<template id="tel">
			<div>
				<h2>手机验证</h2>
			</div>
		</template>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/vue-router.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		const login = {
			template: '#login'
		}
		const register = {
			template: '#register'
		}
		const qq = {
			template: '#qq'
		}
		const tel = {
			template: '#tel'
		}
		const router = new VueRouter({
			routes: [{
					path: '/login',
					component: login,
					children: [{
							path: 'qq',
							component: qq
						},
						{
							path: 'tel',
							component: tel
						}
					]
				},
				{
					path: '/register',
					component: register
				}
			]
		})
		const vm = new Vue({
			el: '#app',
			router
		})
	</script>
</html>
```

