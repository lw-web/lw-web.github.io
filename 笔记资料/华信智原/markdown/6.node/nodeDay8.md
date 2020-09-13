# `node Day8`

## 文件路径问题

### `node`新成员

- `node`每个模块中除了`require`和`exports`以外还有两个新成员：`__dirname`和`__filename`。

- `__dirname`：动态获取文件所在目录的绝对路径

- `__filename`：动态获取包括文件名在内的绝对路径

### `node`文件查找机制

- `node`文件查找是相对于当前命令行执行时所在路径，查找需要的文件

- 当命令行执行的路径发生变化时，相对路径引用的文件查找就会出现错误

### `path.join()`方法

- 该方法具有拼接多个路径的作用

### 动态获取文件路径

```javascript
var path=require('path')
path.join(__dirname,'./a.txt')
```

## 模块化

把复杂的程序拆分成简单模块，使用时在组合起来。

### 不使用模块化的缺点

- 文件越写越大
- 容易出现变量重复使用
- 维护性差
- 不可重复利用... ...

### 解决办法

#### 使用对象

使用对象包裹变量的方法，通过对象属性的方式调用对象成员

```javascript
<script type="text/javascript">
    var obj={
        str:"hello world",
        fun:function(){
            console.log(this.str)
        }
    }
	obj.fun()
</script>
```

- 存在问题：如果给对象属性重新赋值，那么对象属性原来的引用就会断开，原来辛辛苦苦写的方法、属性就没用了。

#### 使用`IIFE`

- 对象属性名和属性值一样的时候可以简写成一个（`ES6`特性）。

- 依赖注入：把需要以来的的模块引入文件

```javascript
(function(window,$){
	var str='你好世界'
	function fun(){
		console.log(str)
	}
	$("body").css("background-color","yellow")
	window.func={
        fun
    }
})(window,jQuery)
```

### 模块化优势

- 避免命名冲突
- 更好的分离，按需加载
- 更高的复用性
- 高度的可维护性... ...

### `script`标签存在的问题

- 每个`script`的加载都会向服务器发送一次请求，多了之后会耗费大量资源

- 依赖复杂（顺序不能错）

- 可维护性差 ...
- 我们需要的是一次引入所有模块化文件——`commonjs`

## `commonjs`

### 在`node`服务端的使用

- `modules`

  - `module1.js`
    - 暴露方式：`exports`或者`module.exports`
  - `module2.js`
  - `module3.js`

- `app.js`

  - 引入模块`require(./modules/module1)`

- `npm init -y`创建`package.json`文件

- `uniq`第三方包

  - ```shell
    npm install uniq --save
    ```

  - ```javascript
    let uniq=require('uniq')
    var result=uniq(arr)//uniq具有数组去重，并按编码给数组成员排序的作用
    ```

  - [npm官网](https://www.npmjs.com/)

### 在`browser`浏览器端的使用

#### 文件目录

- `js`文件

  - `dist`打包编译后的文件

    - `bundl.js`最后`index.html`引入的文件

  - `src`源文件

    - `app.js`入口文件

      - ```javascript
        let module1=require('./module1')//引入加载模块文件
        ```

    - `module1.js`模块，暴露方式：`exports`或者`module.exports`

- `index.html`浏览器端执行文件

#### `browserify`

- 主要作用就是打包编译模块化源文件，使其能够在浏览器端运行

- 安装：

```shell
npm install browserify -g 
```

```shell
npm install browserify --save-dev
```

`-dev`开发时依赖的包，上线的时候自动就去掉了

- 编译：

```shell
browserify js/src/app.js -o js/dist/bundl.js
```

- 在`index.html`中引入使用：

```html
<script src='./js/dist/bundl.js'></script>
```

#### `DOM`操作

可以单独编写操作`DOM`的模块，经过编译后可以在浏览器端正常执行。

## `AMD`

`require.js`用于浏览器端处理模块化，模块加载是异步的。

### 手动实现模块依赖加载

- `a.js`

```javascript
(function(window){
	var str='hello world'
	function fun(){
		console.log(str)
	}
	window.fun=fun	
})(window)
```

- `b.js`

```javascript
(function(window,fun){
	fun()
	var str='hello china'
	function func(){
		console.log(str)
	}
	window.func=func
})(window,fun)
```

- `index.html`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
	</body>
	<script src="js/modules/a.js" type="text/javascript" charset="utf-8"></script>
	<script src="js/modules/b.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		func()
	</script>
</html>
```

### 使用`require.js`

#### 定义模块

- 定义没有依赖的模块：`define(function(){...})`

- 暴露需要公开的成员：`return { fun }`

- 定义依赖于`module1`的模块：`define(['module1'],function(m1){...})`

- 使用`module1`里面的成员：`m1.foo()`

#### 配置入口文件

- 配置：`requirejs.config({paths:{module3:'./mudules3'}})`，`path`配置文件路径
- 配置起始路径：`baseUrl:'js/modules'`

- 引入模块：`requirejs(['module3'],function(m3){...})`

- 使用：`m3.bar()`

#### 在`index.html`中加载

```html
<script data-main="./js/modules/app.js" src="./js/libs/require.js"></script>
```

#### 完整案例

- `module1.js`

```javascript
define(function(){
	var str='modeule1 内容'
	function fun1(){
		console.log(str)
	}
	return { fun1 }
})
```

- `module2.js`

```javascript
define(['module1'],function(m1){
	m1.fun1()
	var str='module2 内容'
	function fun2(){
		console.log(str)
	}
	return { fun2 }
})
```

- `module3.js`

```javascript
define(['module2'],function(m2){
	m2.fun2()
	var str='module3 内容'
	function fun3(){
		console.log(str)
	}
	return { fun3 }
})
```

- `module4.js`

```javascript
define(['jquery'],function($){
	$('button').click(function(){
		$('#box').css('background-color','yellow')
	})
})
```

- `app.js`

```javascript
requirejs.config({
	paths:{
		module1:'./module1',
		module2:'./module2',
		module3:'./module3',
		module4:'./module4',
		jquery:'../libs/jquery'//这里的jquery不能使用大写的jQuery，这是它的源码中的约定，约定使用小写。
	}
})
requirejs(['module3','module4'],function(m3){
	m3.fun3()
})
```

- `index.html`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			#box{
				width: 200px;
				height: 200px;
				border: 1px solid #000;
			}
		</style>
	</head>
	<body>
		<button>按钮</button>
		<div id="box"></div>
	</body>
	<script data-main="./js/modules/app.js" src="./js/libs/require.js"></script>
</html>
```

## `CMD`

[CMD参考文档](https://www.zhangxinxu.com/sp/seajs/)

`sea.js`类似于`require.js`，国内阿里创建的，就是`commonjs`和`AMD`的结合体。但是相对来说受用面较小。

`AMD、CMD`都是非官方标准，官方标准是`ES6`中提供的模块化`API`。

### 定义模块

```javascript
define(function(require,exports,module){
    var module1=require('./module1.js')
    module1.func()
    var arr=[1,2,3,4,5]
    exports.arr=arr
    exports.sayHi=function(){
        console.log('Hi...')
    }
})
```

### 引入使用

```html
<script src='./js/libs/sea.js'>//引入sea.js</script>
<script>
	seajs.use('./js/mian.js')//配置主入口模块
</script>
```

### 异步加载

```javascript
require.async('./module3.js',function(m3){
    console.log(m3.num)
})
```

### 案例

- `module1.js`

```javascript
define(function(require,exports,module){
	var str='我是module1内容'
	exports.fun=function(){
		console.log(str)
	}
})
```

- `module2.js`

```javascript
define(function(require,exports,module){
	var num=10
	module.exports=num
})
```

- `app.js`

```javascript
define(function(require,expports,module){
	var module1=require('./module1.js')
	require.async('./module2.js',function(m2){
		console.log(m2)//异步加载结果最后才打印
	})
	module1.fun()
})
```

- `index.html`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
	</body>
	<script src="js/libs/sea.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		seajs.use('./js/modules/app.js')
	</script>
</html>
```

