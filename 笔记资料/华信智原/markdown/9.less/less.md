# `less`

## less
- css预处理语言
- 让css书写更简洁
- 扩展css书写
- 引入JS思想：变量、函数、参数、参数传递及赋值、运算...
- less sass 

## 引入
第一种解析方式：
- <link rel="stylesheet/less" type="text/css" herf="..." />——引入自己写的less文件
- <script src="..."></script>——引入less.js文件

第二种解析方式：
- 借助第三方工具
- kaola工具：将less解析成css文件

第三种解析方式：
- 使用hbuilder自带的编译方式

## 基本语法——变量
- @value：200px;
- 注释：//注释方式编译之后不会在css中存在；使用/**/多行注释方式编译之后会在css中存在
- @bgc:background-color;使用的时候应该加大括号使用：@{bgc}:red;
- @img:"../img";使用的时候："@{img}/1.jpg";

```less
//尺寸设置
@val:600px;
//背景设置
@bgc:background-color;
@url:'../img';
@clolor:yellow;
@repeat:background-repeat;
@revalue:no-repeat;
@bgcp:background-position;
//定位设置
@p:position;
.box1{
    width: @val*1.3;
    height: @val;
    @{bgc}:@clolor;
    background-image: url('@{url}/3.jpg');
    border:5px solid @clolor;
    @{repeat}:@revalue;
    @{bgcp}:center center;
    @{p}:absolute;
    left: @val*0.6;
    top:@val*0.1;
}
```
## 混合的使用
- .class{width:@val}使用：.box3{.class;...}

## 混合参数传递
- .class(@val:10px,@color:red){border:@val solid @color;}
- .box1{.class(5px,yellow);}
- .box2{.class(@color:blue);}
- .box3{.class;}
- 兼容：-webkit-针对safari，chrome浏览器的内核CSS写法/-ms-针对ie内核的CSS写法/-moz-针对firefox浏览器的内核CSS写法/-o-针对Opera内核的CSS写法

```less
.bd(@val:1px,@type:solid,@col:#000){
    border: @arguments;
}
.box(@w:100px,@h:100px,@bgc:skyblue){
    width: @w;
    height: @h;
    background-color: @bgc;
}
.sd(@x:5px,@y:5px,@m:5px,@col2:#ccc){
    -webkit-box-shadow: @arguments;
    -ms-box-shadow: @arguments;
    -o-box-shadow: @arguments;
    -moz-box-shadow: @arguments;
}
.box2{
    .box;
    .bd;
    .sd;
}
.box3{
    .box(@w:200px,@h:200px,@bgc:yellow);
    .bd(@val:5px,@col:red);
    .sd(@col2:red);
}
```
## 制作三角形（匹配模式）

```less
.size{
    width: 0;
    height: 0;
}
.bd(top){
    border: 20px solid red;
    border-color: transparent transparent black transparent ;  
}
.bd(right){
    border: 20px solid red;
    border-color: transparent transparent transparent black;  
}
.bd(bottom){
    border: 20px solid red;
    border-color:black transparent transparent transparent ;  
}
.bd(left){
    border: 20px solid red;
    border-color: transparent black transparent transparent ;  
}
.box1{
    .size;
    .bd(top);
}
.box2{
    .size;
    .bd(right);
}
.box3{
    .size;
    .bd(bottom);
}
.box4{
    .size;
    .bd(left);
}
```

## 嵌套规则

```less
*{
    margin: 0;
    padding: 0;
}
#box{
    width: 600px;
    height: 600px;
    border: 3px solid #000;
    margin: 0 auto;
    padding:0 10px;
    h2{
        text-align: center;
        margin: 20px 0;
    }
    p{
        margin: 10px 0;
        font-size: 20px;
        text-indent: 2em;
    }
    ul{
        list-style: none;
        li{
            margin: 10px 0;
            background-color: #ccc;
            padding-left: 20px;
            width: 30%;
            &:hover{
                background-color:skyblue;
            }
            a{
                color: black;
                &:hover{
                    color: red;
                }
            }
        }
    }
}

```

- [sass参考资料](http://www.ruanyifeng.com/blog/2012/06/sass.html)