# `html+css`

## **WEB第一阶段总结**

### **HTML**

**基本骨架**

<DOCTYPE	html>	声明文档类型

</html>	跟标签

<head>.....</head>	头部标签

<bady>......<body>	身体标签

head头部标签：

title：标题标签

meat：声明网页元数据

UTF-8国际标准字符集

keywords关键字描述网页主题词

description实现网页描述

<meat http-equiv="refrsh" content="5;url=...."/>实现网页5s跳转

body身体标签：

一对双标签，html主要内容都写在这里面

使用frameset框架标签时要把body删掉才能起作用

**常用标签**

**a.文本标签：**

h1-h6标题标签

双标签，一个页面h1只能使用一次，其余标签不限制使用次数

p段落标签

**b.超链接标签：**

一对a标签，其中href属性用来定义链接地址

链接路径

绝对路径	<http://ww......>

相对路径	../表示返回上一级

锚点链接	链接到网页指定位置

**c.图片标签**

img单标签

src属性用来定义图片文件地址

绝对路径

相对路径

**d.表格标签：**

table双标签

caption标签定义表格名

thead表头标签

tbody表身体标签

tr行标签—td单元格标签

rowsapn跨行合并

colspan跨列合并

th表头标签	字体自动加粗并居中显示

**e.列表标签：**

无序列表

双标签	ul-li

有序列表

双标签	ol-li

定义列表

双标签	dl-dt-dd

**f.表单标签：**

form双标签

input标签

text属性	用户名	label标签用于扩大输入时获取焦点范围

label标签可用for和id属性搭配达到定位效果

password属性	 密码

radio属性	单选框	用checked属性来设置默认选项

checkbox属性  复选框	

submit属性	提交按钮	可用button标签来实现

reset属性	 重置

tel属性	电话号码

search属性	搜素框

date属性	日期

textarea文本域标签

rows定义行数

cols定义列数

select表单

用于做选项菜单

直接嵌套option标签		下拉列表中用selected来设置默认选项

嵌套optgroup标签用来分组列表内容	然后再嵌套option标签

fieldset标签

用来将表单内容分组

结合结合legend标签使用，legend标签用来定义组名

**标签分类**

单标签

br、img、hr、link、meat、、、

双标签

h、p、div、span、、、、

表格

表单

**三层中的结构层**

### **CSS**

**三层中的样式层、专门负责样式**

**层叠样式表**

Cascading Style Sheets

**三种书写方式**

写在标签上（行内样式）

通过style标签写在html文件中（内联样式）

写在css文件中，通过link标签进行引入（外部样式表）——推荐使用（结构样式分离）

**选择器**

标签选择器

通过标签名选择

类选择器

使用最多

ID选择器

一个id名只能使用一次

后代选择器

并级选择器

*通配符选择器——效率低

​      子代选择器

属性选择器

：nth—child（n）

**常用属性**

背景属性（重点）

background-color

background-image

background-position

background-repeat

background-attachment 		 fixed	卷闸门效果

**盒模型**

我们给定的宽高

内填充（padding）

外边框（border）

外边距（margin）

margin重叠

margin塌陷

margin塌陷解决办法:		

​				1.为父盒子设置border（可以设置成透明：border：1px solid transparent）。

​				2.为父盒子添加overflow：hidden；

​				3.为父盒子设定padding值；

​				4.为父盒子添加position：fixed；

​				5.为父盒子添加 display：table；

**浮动**

浮动的元素脱离文档流（飘起来）

清除浮动—方式比较多

a.给父盒子设置固定宽度（高度限制死不利于后期改动）

b.在结尾处添加一个空的块元素（div），清除浮动效果  clear：both;

c.父级元素定义 overflow：hidden;

d.父级元素定义 overflow：auto;

e.父级元素定义  display：table;

f.父级元素定义一个伪类：after和zoom

类名：after { content："";

display：block;

clear：both;

height：0px;  

visibility：hidden; }  （推荐使用）

参考：<https://www.cnblogs.com/nxl0908/p/7245460.html>

**定位**

静态定位		static

绝对定位		absolute

相对定位		relative

固定定位		fixed

**布局**

版心		1000px、1024px（经典尺寸）

**css的三大特性**

层叠性

继承性

权重

继承的权重为0

0（行内），0（id），0（class），0（标签）

**css3中的几个简单属性**

过渡

transition属性

transition：width 2s；想要改变的属性、改变的时间

transition：all 2s；改变所有属性

前缀-webkit-浏览器内核不一样做兼容处理

变形（旋转）

transform属性

rotate	旋转		deg表示“度”

使用transition	给定变化时间

course 	pointer	鼠标经过时变成手形状

**精灵图—雪碧图、图像整合技术**

为什么使用精灵图？

a.当访问该网页时，载入的图片就不会一帧一帧的加载出来

b.降低浏览器向服务器的请求次数，大大提高了网页的加载速度

c.文件体积变小，方便管理

d.后期修改不方便

如何使用精灵图？

应用background-position属性来完成

background:url(img_navsprites.gif) 0 0; ——定义背景图像和它的位置（左0px，顶部0px，通过定位为止达到显示想要部分的目的）

如何制作精灵图？

通过ps把所有需要用到的小图标，全部放在一张画布中来完成













html、css文件在线压缩工具：<http://tool.oschina.net/>