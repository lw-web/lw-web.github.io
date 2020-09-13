# `Vue Day2`

## 过滤器

### 全局过滤器

- 参数一：过滤器名
- 参数二：处理函数

```javascript
Vue.filter('myfilter',function(str){
    return str.replace('从前','以后')//只能替换第一个
    return str.replace(/从前/g,'以后')//替换所有
})
```

- 使用：`{{str|myfilter}}`
- 可以给同一个字符串使用多个过滤器：`{{str|myfilter|第二个过滤器|第三个过滤器...}}`

- 过滤器传参：

```javascript
{{str|myfilter(strNew)}}
Vue.filter('myfilter',(str,strNew)=>{
    return str.replace(/从前/g,strNew)
})
```

- 全局过滤器可以再任何需要的地方使用

### 私有过滤器

- 私有过滤器需要使用`filters`定义
- 私有过滤器也能定义多个
- 调用过滤器先找私有的，没有的话再找全局的

```javascript
var vm=Vue({
    filters:{
        firstFilter(msg,newStr){
            return msg.replace(/今天/g,newStr)
        }
    }
})
```

## `Vue`中的样式

### 添加`class`样式

#### 使用属性绑定

```html
<p ：class='["red","italic"]'>{{msg}}</p>
```

#### 使用三元表达式

```html
<p ：class='["red","italic",flag?"bgc":""]'>{{msg}}</p>
```

#### 数组中使用对象

```html
<p ：class='["red","italic",{"bgc":flag}]'>{{msg}}</p>
```

#### 直接使用对象

```html
<p ：class='{red:true,italic:true}'>{{msg}}</p>
```

- 对象中的键名可以不加引号

#### 使用`data`数据添加

```html
<p ：class='obj'>{{msg}}</p>
```

```javascript
data:{
	obj:{
		red:true,
		italic:false
	}
}
```

### 添加`style`样式

#### 行内直接添加

```html
<p ：style="{color:'red',"font-size":'30px'}">{{msg}}</p>
```

#### 使用`data`数据添加

```html
<p ：style="obj">{{msg}}</p>
```

```javascript
obj:{
    color:'red',
    'background-color':'yellow',
    "letter-spacing":'0.5em'
}
```

## 综合案例知识点

### `some`方法的使用

```javascript
del(id) {
    //findIndex方法
    var delIndex=this.heroes.findIndex(item=>item.id==id)
    this.heroes.splice(delIndex,1)					
    //some方法
    this.heroes.some((item,index)=>{
        if(item.id==id){
            this.heroes.splice(index,1)
            return
        }
    })
}
```

- `some` 英语翻译为一些,`every`翻译为所有、每个
- 所以`some`方法 只要其中一个为`true `就会返回`true`的
- `every`方法必须所有都返回`true`才会返回`true`，哪怕有一个`false`，就会返回`false`
- `every`和 `some`目的：确定数组的所有成员是否满足指定的条件

### `padStrat`方法

- `padStrat`方法接收两个参数：参数一，指定字符串填充后的长度；参数二：填充的内容。

```javascript
str.padStart(2,'0')//指定字符串必须是两位，不够两位的用‘0’填充
```

### `includes()`方法

- `includes()`可以来简化`indexOf()`方法
- 因为`indexOf()`方法返回的是包含字符串的位置，如果是` -1`的话，表明不包含这个字符串
- 而`includes()`方法返回的是布尔值，也就是`true`和`false`，可以直接明确是否包含指定字符串

```javascript
if(item.name.indexOf(keywords)!=-1){
    arr.push(item)
}
if(item.name.includes(keywords)){
    arr.push(item)
}
```

### 键盘修饰符

- 通过`@keyup.enter="add"`的形式绑定键盘事件
  - `enter`：绑定键盘上的回车键
  - `add`：绑定`add`函数
- 如需要自定义键盘修饰符，通过`Vue.config.keyCodes.f2 = 113;`方式定义
- 使用方式：`@keyup.f2="add"`
  - `f2`：绑定键盘`f2`键
  - `113`：键盘按键相对应的编码
  - [js键盘按钮keyCode及示例大全](https://www.cnblogs.com/daysme/p/6272570.html)

### 自定义指令

- 通过`Vue.directive()`方式可自定义指令

```javascript
Vue.directive('focus',{
    //钩子函数
    bind(el,binding){
        //el就是绑定这个自定义指令的原生的js里面的DOM对象，也就是说可以直接给el添加DOM操作
        el.focus();
    },
    inserted(el,binding){
        el.focus();
    },
    update(el){}
});
```

- 使用：`v-focus`

#### 钩子函数

一个指令定义对象通常使用如下几个钩子函数 (均为可选)：

- `bind`：指令绑定到元素上的时候立即执行,只执行一次
  - 绑定指令后并没有插入到`DOM`中
  - 一般样式属性通过`bind`指定
- `inserted`：表示元素插入到`DOM`中时绑定指令
  - 一般元素的行为相关操作通过`inserted`指定，因为要确保元素加载出来
- `update`：当组件更新的时候执行,可能执行多次

#### 钩子函数参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM 元素。
- `binding`：一个对象，包含以下属性
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"`中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。
- `vnode`：Vue 编译生成的虚拟节点
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用

```javascript
//使用指令
<div id="app">
    <input type="text" v-color="'blue'" />
</div>
//定义指令
var vm=new Vue({
    el:'#app',
    directives:{
        color:{
            bind(el,binding){
                el.style.color=binding.value
            }
        }
    }
})
```

## 两个新指令

### `v-if`

- `v-if`的特点是每次都会重新==删除或者创建==元素
- 如果元素涉及到频繁的切换，不建议使用`v-if`

### `v-show`

- `v-show`的特点是每次不会重复` DOM`的==删除和创建==操作
- 只是将元素`disply`的值切换为`none`或`block`

## 案例

### 全局过滤器

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<p>{{msg|firstFilter|secoundFilter|thirdFilter}}</p>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		Vue.filter('firstFilter',msg=>msg.replace(/今天/g,'明天'))
		Vue.filter('secoundFilter',msg=>msg.replace(/天/g,'地'))
		Vue.filter('thirdFilter',msg=>msg.replace(/真/g,'假'))
		var vm=new Vue({
			el:'#app',
			data:{
				msg:'今天的天气真晴朗，今天的早餐真好吃，今天的心情真美好！'
			}
		})
	</script>
</html>
```

### 私有过滤器

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<p>{{msg|firstFilter('明天')|secoundFilter('地')|thirdFilter}}</p>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		Vue.filter('secoundFilter',(msg,newStr)=>msg.replace(/天/g,newStr))
		Vue.filter('thirdFilter',msg=>msg.replace(/真/g,'假'))
		var vm=new Vue({
			el:'#app',
			data:{
				msg:'今天的天气真晴朗，今天的早餐真好吃，今天的心情真美好！'
			},
			filters:{
				firstFilter(msg,newStr){
					return msg.replace(/今天/g,newStr)
				}
			}
		})
	</script>
</html>
```

### 自定义指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<div id="app">
			<input type="text" v-color v-focus />
		</div>		
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
        //自定义全局指令
		Vue.directive('color',{
			bind(el){
				el.style.color="red"
			}
		})
		Vue.directive('focus',{
			inserted(el){
				el.focus();
			}
		})
		var vm=new Vue({
			el:'#app',
            //自定义私有指令
			directives:{
				color:{
					bind(el){
						el.style.color='red'
					}
				},
				focus:{
					inserted(el){
						el.focus()
					}
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
		<link rel="stylesheet" type="text/css" href="css/bootstrap.min.css" />
	</head>
	<body>
		<div id="app">
			<div class="panel panel-default">
				<div class="panel-body text-center">
					<h1>梁山英雄榜</h1>
				</div>
			</div>
			<div class="container">
				<div class="panel panel-default">
					<div class="panel-body">
						<h3 class="text-center">添加英雄</h3>
						<div class="form-group form-inline">
							<!--ID-->
							<label for="id">ID:</label>
							<input type="number" id="id" v-model="id" class="form-control" />
							<!--Name-->
							<label for="name">姓名:</label>
							<input type="text" id="name" v-model="name" class="form-control" />
							<!--Nickname-->
							<label for="nickname">外号:</label>
							<input type="text" id="nickname" v-model="nickname" class="form-control" @keyup.enter="add"/>
							<input type="button" class="btn btn-info" value="添加" @click="add" />
							<div class="pull-right">
								<label for="search">搜索:</label>
								<input type="text" id="search" v-model="keywords" class="form-control" v-focus/>
							</div>
						</div>
					</div>
				</div>
				<table class="table table-bordered table-hover text-center">
					<tr>
						<td>ID</td>
						<td>姓名</td>
						<td>外号</td>
						<td>时间</td>
						<td>操作</td>
					</tr>
					<tr v-for='hero in search(keywords)'>
						<td>{{hero.id}}</td>
						<td>{{hero.name}}</td>
						<td>{{hero.nickname}}</td>
						<td>{{hero.time|newTime}}</td>
						<td>
							<a href="" @click.prevent='del(hero.id)' class="btn btn-danger">删除</a>
						</td>
					</tr>
				</table>				
			</div>
		</div>
	</body>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		var vm = new Vue({
			el: '#app',
			data: {
				id: '',
				name: '',
				nickname: '',
				keywords: '',
				heroes: [{
						id: 1,
						name: '宋江',
						nickname: '及时雨',
						time: new Date()
					},
					{
						id: 2,
						name: '李逵',
						nickname: '黑旋风',
						time: new Date()
					},
					{
						id: 3,
						name: '林冲',
						nickname: '豹子头',
						time: new Date()
					},
					{
						id: 4,
						name: '卢俊义',
						nickname: '玉麒麟',
						time: new Date()
					},
					{
						id: 5,
						name: '燕青',
						nickname: '浪子',
						time: new Date()
					},
				]
			},
			methods: {
				add() {
					this.heroes.push({id:this.id,name:this.name,nickname:this.nickname,time:new Date()})
					this.id='';
					this.name='';
					this.nickname='';
				},
				del(id){
					this.heroes.some((item,index)=>{
						if(item.id==id){
							this.heroes.splice(index,1)
							return 
						}
					})
				},
				search(keywords){
					var arr=[];
					this.heroes.forEach(item=>{
						if(item.name.includes(keywords)){
							arr.push(item)
						}
					})
					return arr
				}
			},
			filters:{
				newTime(date){
					var date=new Date(date);
					var y=date.getFullYear();
					var m=(date.getMonth()+1).toString().padStart(2,'0');
					var d=date.getDate().toString().padStart(2,'0');
					var h=date.getHours().toString().padStart(2,'0');
					var mm=date.getMinutes().toString().padStart(2,'0');
					var s=date.getSeconds().toString().padStart(2,'0');
					return `${y}-${m}-${d}  ${h}:${mm}:${s}`;
				}
			},
			directives:{
				focus:{
					inserted(el){
						el.focus()
					}
				}
			}
		})
	</script>
</html>
```

