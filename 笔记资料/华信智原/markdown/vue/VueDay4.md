# `Vue Day4`

## 动画

### `transition`

#### 使用`transition`标签包裹要执行动画效果元素

```html
<transition name='my'>
    <p v-if='flag'>{{msg}}</p>
</transition>
```

- `transition`的`name`属性可以自定义私有动画

#### 动画的六个过渡类名

-  `v-enter/leave`：进入/离开过渡的开始状态
- `v-enter/leave-active`：进入/离开的过程
- `v-enter/leave-to`：进入/离开的结束状态![过渡类名](assets/animate.png)

### `animate`实现动画

```html
<transition
	enter-active-class="bounceIn" //进入时的动画
    leave-active-class="bounceOut" //离开时的动画
    :duration="{ enter: 200, leave: 400 }">//分别定义进入和离开的动画持续时间
	<h3 v-if="flag" class="animated">这是一个H3</h3>
</transition>
```

### 钩子函数实现动画

```html
<transition
  v-on:before-enter="beforeEnter"//设置元素开始动画之前的起始样式
  v-on:enter="enter"//设置小球完成动画之后的结束状态，动画执行过程（时间、方式等）
  v-on:after-enter="afterEnter"//动画完成之后，调用 >
  <!--需要执行动画的元素-->
</transition>
```

```javascript
methods: {
    // el，表示 要执行动画的那个DOM元素，是个原生的 JS DOM对象   
    beforeEnter(el){
        // 设置小球开始动画之前的，起始位置
        el.style.transform = "translate(0, 0)"
    },
    enter(el, done){
        // 这句话，没有实际的作用，但是，如果不写，出不来动画效果；
        el.offsetWidth
        // 设置小球完成动画之后的，结束状态
        el.style.transform = "translate(150px, 450px)"
        el.style.transition = 'all 1s ease'
        // 这里的 done 是 afterEnter 函数的调用
        done()
    },
    afterEnter(el){
        // 动画完成之后，调用 afterEnter
        this.flag = !this.flag
    }
}
```

### 列表组动画

- 列表组动画需要使用 `<transition-group></transition-group>`包裹
- 要为 `v-for` 循环创建的元素设置动画，必须为每一个元素设置 `:key` 属性
- 给 `transition-group` 添加`appear` 属性，能实现页面刚展示出来时候的入场效果 
- 通过 为 `transition-group` 元素，设置`tag `属性，可以明确将` transition-group` 渲染为指定的元素
  - 如果不指定 `tag `属性，默认渲染为 `span` 标签
- `.v-move` 和` .v-leave-active` 配合使用，能够实现列表后续的元素，慢慢地漂上来的效果

```css
.v-move {
	transition: all 0.6s ease;
}
.v-leave-active{
	position: absolute;
}
```

## 组件

### 组件作用

- 拆分`Vue`代码量
- 按不同功能划分组件
- 根据需求调用组件
- 方便复用

### 组件化、模块化区别

- 模块化： 
  - 是从==代码逻辑==的角度进行划分的
  - 方便代码分层开发，保证每个功能模块的职能单一
- 组件化： 
  - 是从==`UI`界面==的角度进行划分的
  - 前端的组件化，方便`UI`组件的重用

### 创建组件

#### 全局组件

- 创建组件

```javascript
var tem1=Vue.extend({//创建模板
    template:'<div><h1>一级标题</h1><span>我是sapn</span></div>'//必须有唯一的根标签包裹
})
Vue.component('firstCom',tem1)//将模板挂载到组件上
```

- 使用组件

```html
<first-com></first-com> <--这里不能使用驼峰命名法，需要转成‘-’形式-->
```

- 最常用简化创建方式

```javascript
Vue.component('com',{template:'#temp'})
```

#### 私有组件

```javascript
components:{
    login:{template:'#login'}
}
```

- 默认先找私有组件，找不到才会找全局组件

#### 组件中的`data`

```html
<template>
	<div>
        <p>{{msg}}</p>
    </div>
</template>
```

```javascript
Vue.component('login',{
    template:'#login',
    data:function(){//data必须是函数形式
        return {//必须return一个对象的形式传递data数据
            msg:'我是组件内部的data'
        }
    }，
    methods：{//组件也可以有方法
    	add(){}
	}
})
```

#### 组件切换

##### 双组件切换

```html
<a @cilck.prevent='flag=true'>Login</a>
<a @cilck.prevent='flag=false'>Register</a>
<login v-if='flag'></login>
<register v-else='flag'></register>
```

##### 多组件切换

```html
<a @cilck.prevent='comname="login"'>Login</a>
<a @cilck.prevent='comname="register"'>Register</a>
<a @cilck.prevent='comname="logout"'>Login</a>
<component :is="comname"></component>
```

##### 组件添加动画

```html
<transition mode='out-in'>
    <component :is="comname"></component>
</transition>
```

## 案例

### 动画实现方式一

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			.m-enter,.m-leave-to{
				opacity: 0;
				transform: translateX(100px) translateY(100px);
			}
			.m-enter-active,.m-leave-active{
				transition: all 1s ease;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<button @click="flag=!flag">toggle</button>
			<transition name="m">
				<p v-if="flag">{{msg}}</p>
			</transition>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				flag:false,
				msg:'今天好热的！！'
			},
			methods:{}
		})
	</script>
</html>
```

### 动画实现方式二

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/animate.css"/>
	</head>
	<body>
		<div id="app">
			<button @click="flag=!flag">toggle</button>
			<transition enter-active-class='tada' leave-active-class='jello' :duration='{enter:200,leave:800}'>
				<p v-if="flag" class='animated'>{{msg}}</p>
			</transition>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				msg:'今天星期一',
				flag:false
			},
			methods:{}
		})
	</script>
</html>
```

### 动画实现方式三

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			.ball{
				width: 20px;
				height: 20px;
				background-color: red;
				border-radius: 50%;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<button @click="flag=!flag">toggle</button>
			<transition @before-enter='beforeEnter' @enter='enter' @after-enter='afterEnter'>
				<div class="ball" v-if="flag"></div>
			</transition>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				flag:false
			},
			methods:{
				beforeEnter(el){
					el.style.transform='translate(0,0)'
				},
				enter(el,done){
					el.offsetWidth
					el.style.transform='translate(150px,450px)'
					el.style.transition='all 2s ease'
					done()
				},
				afterEnter(el){
					this.flag=!this.flag
				}
			}
		})
	</script>
</html>
```

### 列表组动画

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			li {
				list-style: none;
				border: 2px solid #000000;
				padding: 10px 5px;
				width: 100%;
			}
			li:hover {
				background-color: yellow;
				transition: all .5s;
			}
			.my-enter,.my-leave-to{
				opacity: 0;
				transform: translateY(50px);
			}
			.my-enter-active,.my-leave-active{
				transition: all 1s ease;
			}
			.my-move{
				transition: all 1s ease;
			}
			.my-leave-active{
				position: absolute;
			}
			[v-cloak]{
				display: none;
			}
		</style>
	</head>
	<body>
		<div id="app">
			ID:<input type="text" v-model="id"/>
			姓名:<input type="text" v-model="name" @keyup.enter="add"/>
			<input type="button" value="添加人物" @click="add" />
			<transition-group name='my' appear tag='ul'>
				<li v-for="(item,index) in list" :key='item.id' @click="del(index)" v-cloak>{{item.id}}---{{item.name}}</li>				
			</transition-group>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				id:'',
				name:'',
				list:[
					{id:1,name:'张三'},
					{id:2,name:'李四'},
					{id:3,name:'王五'},
					{id:4,name:'马六'}
				]
			},
			methods:{
				add(){
					this.list.push({id:this.id,name:this.name})
					this.id=this.name=''
				},
				del(index){
					this.list.splice(index,1)
				}
			}
		})
	</script>
</html>
```

###  全局组件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<com1></com1>
			<com2></com2>
			<com3></com3>
		</div>
		<template id="tem3">
			<h1>我还是一级标题</h1>
		</template>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var tem1=Vue.extend({
			template:'<h1>一级标题</h1>'
		})
		Vue.component('com1',tem1)
		Vue.component('com2',Vue.extend({
			template:'<h1>我也是一级标题</h1>'
		}))
		Vue.component('com3',{template:'#tem3'})
		var vm=new Vue({
			el:'#app'
		})
	</script>
</html>
```

### 组件中的`data`和`methods`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<com></com>
		</div>
		<template id="temp">
			<div>
				<h1>我是一级标题</h1>
				<p>{{msg}}</p>
				<button @click="add">点击</button>
			</div>
		</template>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		/*Vue.component('com',{
			template:'#temp',
			data(){
				return {
					msg:'我是组件内部的data'
				}
			},
			methods:{
				add(){
					this.msg+='我是通过add方法追加的内容'
				}
			}
		})*/
		var vm=new Vue({
			el:'#app',
			components:{
				com:{
					template:'#temp',
					data(){
						return {
							msg:'我是组件内部的data'
						}
					},
					methods:{
						add(){
							this.msg+='我是通过add方法追加的内容'
						}
					}
				}
			}
		})
	</script>
</html>
```

### 组件切换

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			.v-enter,.v-leave-to{
				opacity:0 ;
				transform: translateX(100px);
			}
			.v-enter-active,.v-leave-active{
				transition: all 1s ease;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<a href="" @click.prevent='comname="login"'>login</a>
			<a href="" @click.prevent='comname="register"'>register</a>
			<a href="" @click.prevent='comname="logout"'>logout</a>
			<transition mode='out-in'>
				<component :is='comname'></component>
			</transition>			
		</div>
		<template id="login">
			<div>
				<h1>Login</h1>
			</div>
		</template>
		<template id="register">
			<div>
				<h1>Register</h1>
			</div>
		</template>
		<template id="logout">
			<div>
				<h1>logout</h1>
			</div>
		</template>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		Vue.component('login',{template:'#login'})
		Vue.component('register',{template:'#register'})
		Vue.component('logout',{template:'#logout'})
		var vm=new Vue({
			el:'#app',
			data:{
				comname:'login'
			}
		})
	</script>
</html>
```

