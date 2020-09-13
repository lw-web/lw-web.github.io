# `Webpack`

## 安装配置`webpack`

- 生成`package.json`文件：

```shelll
cnpm init -y
```

- 安装`webpack`：

```shell
cnpm install webpack webpack-cli --save-dev
```

## 编写`webpack.config.js`文件

```javascript
const path=require('path')
const htmlWebpackPlugin=require('html-webpack-plugin')
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports={
    entry:path.resolve(__dirname,'./src/main.js'),
    output:{
        path:path.resolve(__dirname,'./dist'),
        filename:'bundel.js'
    },
    module:{
        rules:[
            {test:/\.css$/,use:['style-loader','css-loader']},
    		{test:/\.less$/,use:['style-loader','css-loader','less-loader']},
    		{test:/\.scss/,use:['style-loader','css-loader','sass-loader']},
            {
                test:/\.(jpg|png|gif|bmp|jpeg)$/,
                use:[
                	{
                		loader:'url-loader',
                		options:{
                			limit:1000,
                			name:'[hash:8]-[name].[ext]'
                		}
                	}
                ]
            },
            {test:/\.(ttf|eot|srg|woff|woff2)$/,use:'url-loader'}，
            { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ },
            {test:/\.vue$/,use:'vue-loader'}
        ]
    },
    plugins:[
        new htmlWebpackPlugin({
            template:path.resolve(__dirname,'./src/index.html'),
            filename:'index.html'
        })，
         new VueLoaderPlugin()
    ]
}
```

## 安装配置`webpack-dev-server`

```shell
cnpm install webpack-dev-server --save-dev
```

- 在`package.json`文件中的`scripts`属性中新增：

```json
"dev":"webpack-dev-server --open --hot --port 3000 --contentBase src"
```

## 安装配置`html-webpack-plugin`：

```shell
cnpm install html-webpack-plugin --save-dev
```

- 在`webpack.config.js`文件中增加配置项

## 安装配置`css-loader`：

```shell
cnpm install style-loader css-loader --save-dev
```

- 在`webpack.config.js`文件中增加配置项

## 安装配置`less`：

```shell
cnpm install less-loader less --save-dev
```

- 在`webpack.config.js`文件中增加配置项

## 安装配置`scss`：

```shell
cnpm install sass-loader node-sass --save-dev
```

- 在`webpack.config.js`文件中增加配置项

## 安装配置`url-loader`：

```shell
cnpm install url-loader file-loader --save-dev
```

- 在`webpack.config.js`文件中增加配置项

## `webpack`中高级语法处理

- 安装第三方`babel-loader`：

```shell
cnpm install babel-core babel-loader@7 babel-plugin-transform-runtime --save-dev
cnpm install babel-preset-env babel-preset-stage-0 --save-dev
```

- 在`webpack.config.js`文件中增加配置项
- 在项目根目录中添加`.babelrc`文件，并修改这个配置文件如下：

```javascript
{
    "presets":["env", "stage-0"],
    "plugins":["transform-runtime"]
}
```

## 在`webpack`中使用`vue`

```shell
cnpm install vue --save
cnpm install vue-loader vue-template-compiler --save-dev
```

- 在在`webpack.config.js`文件中增加配置项
- 在`mian.js`文件中引入`vue`：

```javascript
import Vue from 'vue'
```

- 定义`vue`组件：

```vue
<template>
	<div>
		<h1>Login---{{msg}}</h1>
		<h3>我是login组件</h3>
	</div>
</template>

<script>
	export default{
		data(){
			return {msg:'我是login组件数据'}
		}
	}
</script>

<style>
	h1{
		color: red;
	}
</style>
```

- 在`mian.js`文件中引入`login`组件并挂载到页面中：

```javascript
import login from './vue/login.vue'

var vm=new Vue({
	el:'#app',
	render:c=>c(login)
})
```

## `webpack`中使用`vue-router`

- 安装`vue-router`：

```shell
cnpm install vue-router --save
```

- 在`mian.js`文件中引入`vue-router`：

```javascript
import VueRouter from 'vue-router'
```

- 在`mian.js`文件中安装路由模块：

```javascript
Vue.use(VueRouter)
```

- 在`mian.js`文件中导入需要展示的组件：

```javascript
import login from './vue/login.vue'
import register from './vue/register.vue'
```

- 创建路由对象：

```
var router=new VueRouter({
	routes:[
		{path:'/',redirect:'/login'},
		{path:'/login',component:login},
		{path:'/register',component:register}
	]
})
```

- 将路由对象挂载到`vue`实例上：

```javascript
var vm=new Vue({
	el:'#app',
	render(c) {
	    return c(App)	
	},
	router
})
```

- 改造`app.vue`组件，在 `template` 中，添加`router-link`和`router-view`：



