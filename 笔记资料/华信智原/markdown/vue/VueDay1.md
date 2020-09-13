# `Vue Day1`

## 初步了解

前端三大框架：`Vue/Angularjs/React`

提高开发效率

### 库和框架的区别

- 库：也可以叫插件，对项目侵入性较小，使用、切换更加灵活
- 框架：一个完整的解决方案，对项目的侵入性较大，如果要更换框架，就需要重构整个项目

### `Vue`简介

- 一套只关注视图层的框架

- 便于和其它框架整合使用
- 前端`MVVM`分层思想：`M`模型层、`V`视图层、`VM`层沟通`M`层和`V`层
- 核心理念：让用户不再操作`DOM`

- 渐进式框架

## 基本使用

### 创建实例

```javascript
var vm=new Vue({   
    el:'#app', //element,定义vm操作的元素区域
    data:{//数据页面存放
        msg:'helloworld'
    }
})
```

### 使用实例

```html
<div id='app'>
    <p>{{msg}}</p> //插值表达式
</div>
```

### 常用指令

#### `v-cloak`

- `v-cloak`：解决闪烁

```html
<style>
    [v-cloak]{
        display:none
    }
</style>
<p v-cloak>
    {{msg}}
</p>
```

#### `v-text`

- `v-text`：功能类似于差值表达式，区别：
  - `v-text`默认没有闪烁问题，会覆盖元素原本内容
  - 插值表达式不会覆盖原内容

```html
<div>
    <p v-text="msg"></p>
</div>
```

#### `v-html`

- `v-html`：能够将字符串中的`html`标签解析出来

```html
<div>
    <p v-html="msg"></p>
</div>
```

#### `v-bind`

- `v-bind`：绑定属性

```html
<input type="button" v-bind:title="title" value="button" />
```

- `v-bind`可以简写为`:`

#### `v-on`

- `v-on`：绑定事件，绑定的事件如`click`、`dbclick`、`mouseover`等前面用过的都可以。

```html
<input type="button" v-on:click='hello' value="button" />
```

```javascript
methods:{
    hello:function(){
        aletr(this.msg)//通过this可以调用上面定义的数据
    }
}
```

- `v-on`可以简写为`@`

```html
<input type="button" @click='hello' value="button" />
```

- 也可以不通过事件直接触发函数

```html
<p> {{hello()}} </p>
```

- 函数也可以传参

```javascript
methods:{
    hello:function(name){
        aletr('hello'+name)
    }
}
```

```html
<p> {{hello('李伟')}} </p>
```

#### `v-model`

- `v-model`：实现数据的双向绑定，只能运用在表单元素中。

- `eval()`：能够把字符串中的`JavaScript`代码解析出来并执行。

  - 使用`eval()`能够把计算器案例中的`switch`里面的所有内容用一行代码实现：

  ```javascript
  this.ret=eval('parseInt(this.num1)'+this.symbol+'parseInt(this.num2)');
  ```

#### `v-for`

- `v-for='(item,index) in items'`：遍历`data`中的数组和对象以及数字

```html
<ul v-for='(value,index) of arr'>
    <li>{{index+1}}---{{value}}</li>
</ul>
<ul v-for="(value,name,index) in obj">
    <li>{{index+1}}---{{name}}---{{value}}</li>
</ul>
<p v-for="num in 10">{{num}}</p>
```

`v-for`使用的时候一般都给后面添加`:key="item.id"`标识符，来确保元素的唯一性。

### 事件修饰符

- `.stop`：阻止事件冒泡
- `.onece`：事件只触发一次
- `.self`：只有当事件在本身上触发时，才会执行，但不阻止事件冒泡
- `.prevent`：阻止默认行为
- `.capture`：使用事件捕获模式（与事件冒泡执行顺序刚好相反）

- 事件修饰符可以串联使用

### 案例

#### 年龄

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			[v-cloak]{
				display: none;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<span v-cloak>我今年{{age}}岁了。</span><br />
			<input type="button" value="涨一岁" @click="fun(1)"/><br />
			<input type="button" value="年轻一岁" @click="fun(-1)" /><br />
			<input type="button" value="涨十岁" @click="fun(10)" /><br />
			<input type="button" value="年轻十岁" @click="fun(-10)" /><br />
		</div>		
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				age:30
			},
			methods:{
				fun:function(num){
					this.age+=num
				}
			}
		})
	</script>
</html>
```

#### 坐标展示

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{				
				margin: 0;
				padding: 0;
			}
			.box{
				width:500px;
				height: 500px;
				border: 1px solid #000;
				cursor: move;
				text-align: center;
				line-height: 500px;
				font-size: 40px;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<div class="box" @mousemove="show">
				{{x}},{{y}}
			</div>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				x:0,
				y:0
			},
			methods:{
				show:function(e){
					this.x=e.clientX;
					this.y=e.clientY;
				}
			}
		})
	</script>
</html>
```

#### 切换背景色

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			.box{
				width: 400px;
				height: 400px;
				background-color:yellow;
			}
			.red{
				background-color: red;
			}
		</style>
	</head>
	<body>
		<div id="app">
			<div :class="color" @click="change"></div>			
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				color:'box'
			},
			methods:{
				change:function(){
					this.color+=' red'
				}
			}
		})
	</script>
</html>
```

#### 滚动文字

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<input type="button" @click="go" value="开始"/>			
			<input type="button" @click="stop" value="暂停"/>	
			<p>{{msg}}</p>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				timer:null,
				msg:'陕西欢迎你，西安欢迎你！！'
			},
			methods:{
				go(){
					if(this.timer!=null){
						return
					}
					this.timer=setInterval(()=>{
						var first=this.msg.substring(0,1);
						var end=this.msg.substring(1);
						this.msg=end+first;
					},500)
				},
				stop(){
					clearInterval(this.timer);
					this.timer=null;
				}
			}
		})
	</script>
</html>
```

#### 简易计算器

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<input type="text" v-model="num1" />
			<select v-model="symbol">
				<option value="+">+</option>
				<option value="-">-</option>
				<option value="*">*</option>
				<option value="/">/</option>
			</select>
			<input type="text" v-model="num2" />
			<input type="button" value="=" @click="result" />
			<input type="text" v-model="ret" />
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				symbol:'+',
				num1:0,
				num2:0,
				ret:0
			},
			methods:{
				result(){
					switch(this.symbol){
						case '+':
							this.ret=parseInt(this.num1)+parseInt(this.num2);
							break;
						case '-':
							this.ret=parseInt(this.num1)-parseInt(this.num2);
							break;
						case '*':
							this.ret=parseInt(this.num1)*parseInt(this.num2);
							break;
						case '/':
							this.ret=parseInt(this.num1)/parseInt(this.num2);
							break;
						default:
							break;
					}
				}
			}
		})
	</script>
</html>
```

#### 添加人物

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		<div id="app">
			<div>
				ID:<input type="text" v-model="id"/>
				Name:<input type="text" v-model="name"/>
				<input type="button" value="添加" @click="add"/>
			</div>
			<div v-for="p in person" :key='p.id'>
				<input type="checkbox"/>
				<span>{{p.id}}</span>
				<span>{{p.name}}</span>
			</div>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#app',
			data:{
				id:'',
				name:'',
				person:[
					{id:1,name:'乔峰'},
					{id:2,name:"段誉"},
					{id:3,name:"虚竹"}
				]
			},
			methods:{
				add(){
					this.person.unshift({id:this.id,name:this.name})
				}
			}
		})
	</script>
</html>
```

