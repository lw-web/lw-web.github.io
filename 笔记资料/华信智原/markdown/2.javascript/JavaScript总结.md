## 前端三层
- **HTML ==结构层==**
- **CSS ==样式层==**
- **JavaScript ==行为层==**  

### JS能做什么？
- 嵌入动态文本于HTML页面。
- 对浏览器事件作出反应。
- 读写HTML元素
- 在数据被提交到服务器之前验证数据。
- 检测访客的浏览器信息。
- 基于Node.js技术进行服务器端编程。

### JS简介
JavaScript是一种==直译式脚本语言==，是一种==动态型==、==弱类型==、==基于原型==的语言。  
**基本特点：**  
- 是一种解释性脚本语言（*代码不进行预编译，解释一条，执行一条*）。  
- 前期只要用来向HTML页面添加交互行为。
- 可以直接嵌入HTML页面，但写成单独的JS文件有利于结构和行为的分离。
- 跨平台性，在绝大多数浏览器的支持下，可以在多种平台运行。

### JS组成部分
- **ECMAScript**，描述该语言的语法和基本内容,是JS执行的标准。  
- **DOM**（文档模型），描述处理网页内容的方法和接口。
- **BOM**（浏览器模型），描述与浏览器进行交互的方法和接口。

### JS书写方式
- 行内式  
- 外链式    ==外部引入之后，script标签中不能再写代码了，写的是不会执行的==
- 内联式     ==相同的引号不能嵌套使用，可以单双引号嵌套使用==

### 三个简单输出语句
```
alert("这里面的内容会在弹框中显示！");  
document.write("这里面的内容会在页面文档中显示");  
console.logo("这里面的内容会在控制台打印输出")；  
```
alert（"你好"）  完整写法是 window.alert(); window对象可以省略  
- 使用不多，比较麻烦，要去点击
- 各个浏览器弹窗效果不一样
- 后期需要弹窗效果的话，一般都是div+css来完成  

console.log("你好"); 
- 打印输出一些内容，用来查错误
- console.warn("警告");
- console.error("错误");

document.write("今天天气不好");  
document.write("\<h2>我是二级标题\</h2>");

### 变量
在JavaScript中，变量一般都是==直接量==，也叫==字面量==。  
**变量声明**  
基本语法：==var 变量=赋值;==  
**变量、函数名命名规则：**  
- 不能以数字开头
- 不建议使用汉字
- 建议使用英文（要有语义，使用驼峰命名法）
- 可以使用$或者_开头
- 区分大小写（例如：A和a是两个变量）
- 关键字或保留字（未来的关键字）不能使用

### 变量及变量的作用域
- 全局变量  在函数外部声明的变量    在函数内部能够调用
- 局部变量  在函数内部声明的变量    在函数外部不能调用
- 函数中变量会优先使用局部变量，找不到才会调用全局变量  

### 变量声明的提升
==JS执行前会预解析，会把var后面紧跟的变量声明全部提升到最前面==，然后再开始一条一条执行。 示例如下：
```
console.log(b);// undefined
var b=20;
相当于
var b;
console.log(b);
b=20;
```
### 五种数据类型
|   名称    |   类型   |                           注意事项                           |
| :-------: | :------: | :----------------------------------------------------------: |
|  number   |  数值型  | *在JavaScript中，不分浮点型和整型，全部都叫数值型。*  控制台显示蓝色 |
|  string   | 字符串型 | 采用单引号或双引号包裹，其中内容可以使任何形式，包括==数字、html标签、符号等==所有能见到的内容。 |
|  boolean  |  布尔值  |                    它的值只有false和true                     |
|   null    |    空    |                                                              |
| undefined |  未定义  | 只声明变量，而不赋值，打印输出结果为undefined；==不声明，直接打印输出，会报错  **is not defined**== |

### 五种假：  
- 0
- false
- ""
- null
- undefined  
- ==NaN也是假==

### isNaN
==isNaN(参数);==    里面的参数是数值类型返回false，不是返回true  
==判断机制和parseInt（）一样==，能识别出字符串中打头的数字。

### 算术运算符
#### \+ 执行加法运算
-  ==在两个数值类型中间时，和数学中的加号作用相同==
-  ==在数值型和字符串型之间，或者连个字符串之间时，起到拼接字符串的作用==

#### \- 执行减法运算
-  ==在两个数值型中间时，作用和数学中减号相同==
-  ==在两个字符串型的数字中间时，会将字符串型数字自动转换成数值型，然后进行减法运算，返回结果是数值型。而在加法运算中，这种境况下进行的是字符串拼接。==

####  \* 就是乘法运算
#### / 就是除法运算
#### % 就是取余运算
==字符串型做乘、除、取余运算时，会报错。==  

### 关系运算符
| 符号 |    意思    |      |
| :--: | :--------: | ---- |
|  \>  |   大于号   |      |
|  <   |   小于号   |      |
| \>=  | 大于或等于 |      |
|  <=  | 小于或等于 |      |
|  ==  |   等等于   |      |
| ===  |   全等于   |      |
| ！=  |   不等于   |      |
| ！== |  不全等于  |      |
==特别注意==**“=” 代表的是赋值**  
==**注意：** 在两个等于号判断的时候，两个字符串型的数字比较，加空格返回true；但是两个纯字符串比较，加空格返回的是false。==  

### 逻辑运算符
- && 与 和、且
- || 或 或者
- ！ 非 否定、取反 

### 一元运算符
- typeof 
- i++
- ++i
- i--
- --i

**总结：**
- ==++或--前置，先赋值后计算==
- ==++或--后置，先计算后赋值== 

### 字符串型数字转成数值型
- **parseInt();** 该方法有直接取整的效果，采用的是去尾法，==不会四舍五入==。  
  - parseInt("23abc"); 这种情况会返回23，但是==只能识别打头的数字==，后面加在字符串中的数字是不能识别的。  
如果里面是纯字符串，返回number型的NaN。
- **parseFloat();** 该方法和parseInt()方法功能类似，但是能保留小数，少位小数，就输出多少位小数。  

### 基本数据类型之间的转换
**number变成字符串类型**  
- 12+"";
- a=String(12);  

**字符串转换成number类型**  
- "22"-0
- Number("22")  

**number转成boolean类型** 
- Boolean(0);// 返回false
- Boolean("");// 返回false
- Boolean(null);// 返回false
- Boolean(undefined);// 返回false
- Boolean(NaN);// 返回false 
- ！！也可以转成Boolean值 

### if语句
if基本语句  
多分支if语句
```
if(条件1){
    条件1满足执行
}else if(条件2){
    条件1不满足,条件2满足执行
}else{
    以上条件都不满足执行
}
```
if语句嵌套使用
- 标签可以嵌套使用
```
if(条件1){
	if(条件2){
		同时满足条件1和条件2,才会执行
	}
}
```
注意if语句的跳楼现象

### for循环
基本语法  for（var i=0;i<10;i++）{代码块}  
- 最经典的就是：从1到100求和。

```
var sum=0;
for(var i=1;i<=100;i++){
sum+=i;
}
```

### 函数
函数需要2步基本操作：

```
1.声明函数
function hanshu(){
	console.log(123);
}
2.调用函数(可以多次调用)
hanshu();
```
==函数调用可以再函数声明前也可以在声明后==  
每一个函数都有变量名，命名规则和变量名一样：


我们函数名后面的括号中传递的是参数，这个是==形参==（形式上的参数）。  
调用函数的函数名后面的括号中也可以传递参数，这个是==实参==（具有实际意义的参数）。  
函数可以传递多个参数，中间用逗号分隔。  
**return**关键字，用来返回函数值。  
==return后面的内容不能换行。==  
==return后面的代码是不会执行的，return后面就不要写东西了。==   

**函数定义：**
- 可以==重复调用==的代码块。
- 可以单独写在JS文件中，需要时最是调用。  

### 函数的创建方式
- 函数声明式
```
function fun(){
    console.log("helloWorld");
}
fun();
```
==fun函数名，代表整个函数==  
==fun（）代表函数的调用==
- 函数表达式
```
var func=function(){
    console.log("helloWorld");
}
console.log(func);
func();
```
- 构造函数（这种方式很少使用）
```
var funct=new Function("var num1=10;var num2=20;console.log(num1+num2)");
funct();
```
首字母大写开始的叫==构造函数== 


### JS两种声明函数的方法以及调用顺序
两种声明方法：  
- 第一种： var a = function () {...};  
- 第二种function a() {...};  

第一种方式必须==先声明后调用==，而第二种方式==函数调用在声明之前之后都可以==。  
页面加载过程中，浏览器会对页面上或载入的每个js代码块(或文件)进行扫描，如果遇到定义式函数，则进行预处理(类似于C等的编译)，处理完成之后再开始由上至下执行；遇到赋值式函数，则只是将函数赋给一个变量，不进行预处理(类似1中变量必须先定义后引用的原则)，待调用到的时候才进行处理。
### 入口函数
**window.onload=funciotn(){
    代码块;
}**   
==页面加载完成后，再执行代码块。==  
JS文件引入是存在==顺序关系==的，如果存在==依赖关系==的JS文件，他们的引入顺序是不能变的。
### 内置对象
- JS本身自带的对象
- - 日期对象
- - Math对象
- - window对象
### 获取一个元素
- getElementById();方法，通过Id名获取某个元素（绝对是唯一的）。
### 事件及事件三要素
事件三要素：  
- 事件源    关闭的按钮
- 事件  鼠标点击事件
- 事件处理程序  广告关闭了  
常用的事件：  
- onclick
- onmouseover
- onmouseout
- onload
### 一些注意事项
==is not defined 未声明函数时报错内容==  
==undefined   声明函数未赋值，显示的内容==  
==null    是一个值，未赋值不会显示null==
### 几个有用的方法
- ==typeof== 判断变量数据类型
- ==Number.MAX_VALUE== Number的最大值
- ==Number.MIN_VALUE== Number的最小值  
### Math对象
**乘方** ==Math.pow(4,5);== *计算4的5次方*  
**开根号** ==Math.sqrt(4);== *计算4的平方根*  
### 用户输入框
==prompt("提示内容");== 用户输入框  
可以用变量接收输入的内容，再对变量进行操作，但是==接收到的都是string类型==的数据。  
一定要牢记，使用prompt()接收到的数据是==字符串型==的，要做算术运算，要先使用==parseInt()转换成数值型==，才能进行操作。 

### 两种消失的的区别
- **display：none；**   消失后不占用原来位置  
- **visibility：hidden；**  消失后依旧占用原来位置
### 容器在页面居中显示
实现容器在页面中间显示，垂直水平都居中：  
```
position: absolute;
top:0;
bottom:0;
left:0;
right:0;
margin:auto;
```


### 函数参数
- 注意点一：
```
function fun(a,b,c){
	console.log(a+b+c);
}
fun();// 返回NaN
```
- 注意点二：
  - 形参实参不统一，会按照顺序为参数赋值，多了少了都是这样。
  - undefined执行任何操作返回NaN
- 注意点三：arguments
  - console.log(fun.length);// 获取到的是形参的个数
  - console.log(arguments);// ==获取到实参数组==
  - console.log(arguments[0]);// 第一个实参
  - console.log(arguments.length);// 实参的个数
  - 实现形参实参统一的判断代码：==fun.length=arguments.length。==  

### return
- return后面的代码不会执行；
- 后面的代码不能换行。  
- 可以使用return返回需要值，来封装函数。

### 表单常用事件  
- onfocus（获得焦点）
- onblur（失去焦点）
- focus()自动获取焦点
- value 获取表单输入的内容
- select() 表单选择内容
- checked=true 选中
- oninput 输入内容时(IE6、7、8兼容的是onpropertychange。)
  


### 获得元素的方式
- 通过Id获取元素，document.getElementById();  
- 通过标签名获取元素，documnet.getElementsByTagName()，获取到的是一个伪数组；
- 通过类名获取元素，document.getElementsByClassName(),获取到的也是一个伪数组；
- 对于获取到伪数组的情况，一般处理方式如下：
  - 通过for循环遍历所有元素
  - 通过父级元素缩小范围之后再获取里面的元素

  


### 数组
- 创建数组：
  - var arr=[1,2,3,4,5...];
  - var arr2=new Array(1,2,3,4,5....)// 使用不多
- 通过下标（索引）来获取数组中元素，没有的元素返回undefined
- 遍历数组元素，for循环
- 数组常用的几个方法
  - pop：删除并返回最后一个元素；
  - push：向数组末尾添加一个或多个元素，并返回新数组长度；
  - shift：删除并返回数组第一个元素；
  - unshift：向数组开头添加元素，并返回新数组长度；
  - concat：连接多个数组并返回结果；
  - reverse：颠倒数组顺序；
  - sort：对数组元素进行排序；证明是没用的！！！
  - toString：把数组转成字符串，并返回结果；
  - join：把数组所有元素放入一个字符串，并用指定符号分割；
  - slice：从已有的数组返回选定的元素，可以传负值；
  - splice：删除元素并添加新元素，改变的元素比slice多一个，基本涵盖slice功能，记这个就够了；  
  - split('字符串中符号')==符号必须统一==用指定符号分隔，把字符串转成数组

### 运算符
- 一元运算符
  - typeof
  - ++、--
  - +a、-a和数学上的正负相同
- 二元运算符
  - +、-、*、/、%
  - 与或非
- 三元（三目）运算
  - 表达式？结果1：结果2；
  - 全选、反选代码优化，同样的重复内容，要想到使用函数重复调用来简化。
  - 事件调用函数，如果不使用匿名函数的话，调用函数会直接执行，所以必须用匿名函数包裹调用函数内容。

### 循环
- for循环，从1到100求和；
- while循环，while(条件){代码块}；
- do{代码块}while(条件)；
```
while(i<=100){
	sum+=i;
	i++;
}
do{
	sum+=i;
	i++
}while(i<=100)
```
### switch语句
- switch(条件){case value:语句；break；......default 语句；break;}


### DOM
JS组成部分：
- ECMAScript
- DOM——Document Object Model 文档对象模型
- BOM  

DOM：
- DOM树
- 节点：（元素、标签）
  - 标签节点
  - 属性节点
  - 文本节点
- 访问节点
  - 访问标签节点：getElementsByTagName
  - id属性：getElementById
  - class属性：getElementsByClassName（IE6、7、8不支持这个写法）
    - 例如IE6、7基本上没有人在用了，但是IE8使用人数还不少
    - IE9及以后的版本是兼容的
    - 写一个兼容的函数，直接调用来处理兼容问题
    

### 节点关系
- 父节点parentNode，这个操作可以连续使用，如span.parentNode.parentNode
- 兄弟节点nextElementSibling、previousElementSibling；注意nextSibling、previousSibling是IE6、7、8专用获取方式。
- 子节点firstElementChild、lastElementChild；注意firstChild、lastChild是IE6、7、8专用获取方式。
  - childNodes，他是一个W3C指定推荐的，包含换行在内
  - nodeType==1，表示这是元素节点
  - children能拿到子元素，且没有多余内容，这是一个非标准，但是好用，且没有兼容问题。  


### 节点操作
- 创建元素 document.creatElement(标签==字符串==);
  - 插入元素 .appendChild(创建元素);
  - 创建的是子元素，插入到父元素的最后面
  - 另一种插入元素 insertBefore(新创建元素，参考元素);如果参考元素传null，就和appendChild一样了。
- 删除元素 .removeChild(要删除的元素);
- 克隆一个元素 cloneNode(); true深克隆

### 属性操作
- 获得属性 getAttribute()；
- 删除属性 removeAttribute；
- 修改属性 setAttribute；

### 小总结
- 如果要改变的元素样式是写在style标签中的，一般是.style再加上属性名来修改样式；不是写在style标签中的属性，例如src是不用再写.style的，而是直接写.src。
- innerHTML，修改元素内容
- this关键字，指的是事件的调用者
- 通过className改变样式  
- 字符串拼接，变量要单独提出来，用+号拼接，空格坚决不能少。
- 排它思想，首先把所有都干掉，再给自己添加
- 自定义属性.index拿到当前元素下标
- ||使用或符号来写兼容==注意点：需要先写高级浏览器== 
- 事件可以连写，.oninput=.onpropertychange=function(){}
- 常用事件回顾：
  - onchange
  - oninput（onpropertychange）
  - onfocus
  - onblur
  - onmouseover
  - onmouseout
  - onclick
  - ondblick
  - onload



### 日期对象
- 内置对象，JS中有很多内置对象 Math Array Date Vue
- var date=new Date();// 调用的是系统时间，如果运行程序的电脑时间改了，获取到的时间也会跟着变
- getTime，获得到的毫秒数
  - 1秒等于1000毫秒
  - 从1970年至今的毫秒数
  - 2038年问题
- getFullYear，获取年份 当前年份
- getMonth，获取月份 0-11月
- getDate，获取几号 1-31号
- getDay，获取星期几 0-6
- getHours，获取时 
- getMinutes，获取分
- getSeconds，获取秒

### 定时器
- window.setInterval(执行函数，间隔时间);//间隔时间必须是==毫秒==；window可省略。
  - 注意：==第一个参数必须是一个函数，可传入函数名，但是不能加括号。== 
- setTimeout(函数，间隔时间)；
  - 这个定时器是间隔时间之后执行函数，只执行一次，和定时炸弹类似
  - setInterval定时器是每间隔多少秒就执行一次，一直循环，除非清除定时器
  - 案例：5s之后页面自动跳转
    - window.location.href="url";//BOM里面内容
    - setTimeout可以实现倒计时

### arguments
- arguments.length 实参个数
- arguments.callee 代表当前执行的函数  
==函数自己调用自己可以使用arguments.callee来替代==  
- 递归的典型案例——斐波那契数列 1 1 2 3 5 8 13 21

### 运算符
- 一元运算符    正号、符号、++、--
- 二元运算符    +、-、*、/、%
- 三元运算符    表达式？真：假
- 逻辑运算符    &&、||、！
- 关系运算符    >、<、>=、<=、\==、\===、！=、！\==
- 优先级顺序
  - ()括号
  - ！非、-符号++、--
  - *、/、%
  - +、-
  - \>、<、>=、<=
  - \==、\===、！=、！\==
  - &&
  - ||
  - 三元运算符  
- 五种假：0、null、undefined、""、false
- &&：同真为真；
- ||：同假为假；  

```
var a =  2  &&  4  || 3 ;//返回4
var b = 0 && 3 || 4 ;//返回4
var c= 0 && 1 || 3 && 4;//返回4
var d = 4 && 5 && 6 ;//返回6
```

### 数值转字符串
- String()      ==它的参数是字符串==
```
var str=123;
String(str);//返回的是字符串的123
```
- +""           ==+起到字符串拼接作用==
```
var str=123;
str+"";//返回的是字符串的123
```
- toString()    ==它的参数是基数，可以传2，8，10，16等进制数==
```
var str=123;
str.toString(2);//返回的是字符串的二进制的123
```
### 检测字符串长度
- charAt(); （下标）    ==根据下标，返回对应的字符==
- charCodeAt();     ==根据下标，返回对应的字符编码==
- length;   ==返回字符串长度==
  - 空格也算字符，一个字母对应的长度是1，汉字长度是2
  - 但是length方法获取到的汉字长度是1，当成字母来处理，所以有问题
  - 封装一个方法来处理这个汉字长度的问题，借助charCodeAt方法
  - 一般英文字符字符编码在0~121之间  

### 根据字符返回下标
- indexOf();  ==找最前面的那个指定字符，找到就结束了==
- lastIndexOf();  ==找的是最后面的那个指定字符，找到就结束。但是也是从最前面开始计数。==  
- 查找结果返回-1，指的是没有找到指定字符。

### 网址编码及解码
- 编码encodeURICompent;
- 解码decodeURICompent;

### 字符串操作
- concat;   ==能进行数组及字符串的合并==
- slice;    ==有两个参数，开始位置和结束位置。包含开始位置下标，但不包含结束位置下标。如果不传第二个参数，默认截取到结束。可以传负值，就是从最后面开始数负数的绝对值个数。==
- substr；  ==两个参数，开始位置和截取长度。包含开始位置下标字符。类似于数组的splice。== 文档中\[  \]里面的是可选参数。
  - 一般不要使用负数，在IE6、7、8中会出问题。
- substring；   ==两个参数，始终会以小的为开始位置，大的为截取长度，==

**对数值保留两位小数**
- 方法一：toFixed(2);   ==数学里面提供的方法，对象必须是数字,有四舍五入。==
- 方法二：数值乘100，取整，再除以100
- 方法三：sunstr(0,indexOf("."))

### 文件上传判断
- input中type="file"属性    ==HTML5中的表单新控件==
- onchange事件

### 转换大小写
- toUpperCase
- toLowerCases

### 另一种获取元素方式
- querySelector  ==HTML5中提供的方法，可以传span、.span、#span，只返回第一个元素。==
- querySelectorAll  ==获取全部元素。==
- IE8是兼容这两个方法的，可以放心使用

### 缓动公式
加速运动公式：leader=leader+(target-leader)/10;  
- leader：起始位置
- target：目标位置

### 获取元素的尺寸
- 通过style是拿不到写在style样式表中尺寸信息的，只能用来添加行内样式，也只能获取行内样式数据，以字符串形式返回，比如："200px"。
- offset：自己。offsetWidth、offsetHeight来获取样式表或行内的宽高信息。
  - offsetWidth和offsetHeight能获取==内容区和内边距、边框==的累积尺寸。
  - offsetWidth=width+padding+border。
- offsetLeft、offsetTop：找离自己最近的带有定位的父元素，如果父元素都没有添加定位，就找body。
  - offsetLeft==包含内边距、不包含边框。==
- offsetParent：拿到的是离他最近的带有定位的父元素。tagName，拿到标签名，大写的。

### event
- js是事件驱动的
- event事件对象
- 存在兼容问题，IE只认识window.event
- event事件对象属性
  - clientX;    ==是以当前窗口、可视区为基准的。==
  - clientY;
  - pageX;      ==是以整个文档为基准的。==
  - pageY;
  - screenX;    ==是以电脑屏幕为基准的。==
  - screenY;
- onmouseover   ==鼠标经过元素，只触发一次==
- onmousemove   ==鼠标移动，鼠标只要动就会触发事件==

### 短信验证案例
- 单标签内容用value
- 双标签内容用innerHTML
- 在定时器中，this指向的是window
- 声明that或者_this变量存储this，后面就可以调用了
- 声明timer等于null，然后使用clearInterval清除定时器
- 用定时器一般都是先清除定时器
- disabled="disabled" 按钮点击禁用
- 在定时器外面在单独调用一次函数，可以清除页面的短暂停留，能很好的过渡

### 新增属性
- text-shadow 文字阴影
- box-shadow 盒子阴影

### scroll
- window对象的screenTop、screenLeft属性
- scrollTop、scrollLeft
- window.onscroll事件，滚动条滚动时
- document.documentElement.scrollTop    ==要注意兼容问题，Safari和没有文档声明的IE6、7、8中要使用特殊写法。==
  - 兼容写法：var scrolltop=document.documentElement.scrollTop||document.body.scrollTop||window.pageYOffset||0;
- window.scrollTo(x,y); 让水平和垂直滚动条去到啥位置。

### 盒子尺寸获取方法
- client：可视区
- offsetHeight：包含内height、padding、border
- clientHeight：包含height、padding，没有border
- scrollHeight：元素的内容的高度，内容没有超过盒子就和clientHeight一样

### 屏幕尺寸
- IE9+：通过window.innerWidth
- 标准浏览器：通过document.documentElement.clientWidth
- 非标准浏览器：通过document.body.clientWidth
- 兼容处理：

### 新增事件
- window.onresize:窗口尺寸发生改变时
- onmousedown：鼠标点下
- onmouseup：鼠标松开

### 检测屏幕分辨率
- window.screen.width、window.screen.height
- 不会随着浏览器窗口改变而改变，除非改变电脑系统的分辨率

### HTML结构访问
- 获取title、head等文档内容
  - document.title  ==标题==
  - document.head   ==头部==
  - document.body   ==身体==
  - document.documentElement    ==HTML==
- 数组表示法

### 阻止冒泡
- 事件冒泡顺序IE6：div——body——html——document；正常浏览器：div——body——html——document——window。
  - 相同事件才会触发冒泡
  - 很多事件是没有冒泡的，比如focus、blur、load等是没有冒泡的。
- 阻止事件冒泡：event.stopPropagation;存在兼容问题，IE使用window.event.cancelBubble=true;

### target
- event.target;获取点击元素本身。
- event.target.id;获取点击元素的id名。
- IE中识别的是srcElement
- document.body.style.overflow="hidden";超出隐藏
- document.body.style.overflow="visible";显示滚动条

### 文字选择
- 获取选中文字：
- 正常浏览器：window.getSelection().toString();
- IE中使用：document.selection.createRange().text;
- ==opacity:.7;存在兼容问题，IE低版本不认识。==



### Math对象
- parseInt
- 数学意义上的取整
  - Math.ceil;  进一法
  - Math.floor; 去尾法
  - Math.round; 四舍五入法
- Math.abs();   取绝对值
- Math.sqrt();  开根号
- Math.pow(x,y);    x的y次方
- Math.random();

### 通过style方式获取的样式
- 只能拿到行内样式；
- 拿到的是字符串数据类型，带px；
- 简单的封装（使用[]可以传变量）；
- 存在问题：只能拿到行内样式，但是我们一般是不使用行内样式的。
```
function getAttr(attr){
    console.log(box.style[attr]);
}
getAttr("left");
```
### currentStyle当前样式/window.getComputedStyle(obj,null)
- box.currentStyle.width    ==IE6、7、8使用的方式==
- window.getComputedStyle(box,null).width   ==W3C推荐的==
  - 拿到的是css样式，获取的是字符串类型的，带px的属性值。
- 背景颜色background-color的方式IE是不能获取的，需要使用backgroundColor。
- 兼容处理
```
function getAttr(obj,attribute){
	if(obj.currentStyle){
		return obj.currentStyle[attribute];
	}else{
		return window.getComputedStyle(obj,null)[attribute];
	}
}
```
### 数据类型
- 五种基本数据类型：number、string、Boolean、null、undefined。
- 引用数据类型：Object（Array、function...）。
- 对象：属性和方法。
- 对象创建方式：
  - var arr=new Array();/var date=new Date();/var obj=new Object();//构造函数方式
  - var obj={};//对象字面量方式

### 创建对象的封装
- 对象创建的工厂模式
- 构造函数模式
```
//工厂模式
function Person(name,age,gender){
	var obj={};
	obj.name=name;
	obj.age=age;
	obj.gender=gender;
	obj.sayName=function(){
		console.log(this.name);
	}
	return obj;
}
var p1=Person("zhangsan",32,"nan");
//构造函数模式
function Person(name,age,gender){
	this.name=name;
	this.age=age;
	this.gender=gender;
	this.sayName=function(){
		console.log(this.name);
	}
}
var p1=new Person("zhangsan",23,"nan");
```
### this
- 以函数形式调用，指向window
- 以方法形式调用，指向方法调用者。
  - setInterval中this指向window，因为setInterval是window.setInterval的简写。
- 当以构造方法调用时，this指的是新创建的对象。

### 构造函数
- 就是函数
- 函数名首字母大写
- 认为是创建了一个类，实例化时要使用new关键字

### 数组方法的使用
- Array数组中没有的方法，我们可以再原型中添加自定义方法。
- prototype：原型
- 使用prototype改造构造函数   
- prototype中，必须使用this关键字，否则无法明确指向

### 函数的回顾
- 函数两种创建方式
  - 函数声明：function fun(){}
  - 函数表达式：var fun=function(){};只能先声明后调用
- 变量作用域
  - 在函数中形成的是局部变量，在全局的就是全局变量(都是以window的属性形式存在)。
  - 全局中无法访问局部变量。
  - 函数内部可以再写函数。

### 闭包
- 函数里面嵌套函数，内部函数可以访问外部函数的变量。
- 函数访问了函数外部的变量，就是闭包。
- 用于创建需要隐藏的变量。

### 闭包传参
- 分清内外函数的传参位置

```
function biBao(num){
	return function(str){
		console.log(num);
		console.log(str);
	}
}
biBao(1000)("hello");//打印输出10000，hello
```

### 求一个数组的偶数的和——原型的应用
- 奇数：odd；偶数：even；
- Array.prototype.evenAdd=function(){};
- ==内置对象的拓展（面试会问到）。==

### 箭头函数(IE6/7/8不支持)
- 箭头=>
- function fun(){}
- 箭头函数：(传参位置) => {代码块位置}
- 假如参数只有一个，括号可以省略:a=>{}
- 假如代码只有一个返回值，大括号可以省略，return也可以省略：id=>document.getElementById(id)
- 入口函数：window.onload=()=>{...}
- 框架中才会用到箭头函数，暂时了解（箭头函数能够改变this指向）

### 正则表达式
- 表单注册
- 正则表达式：是个对象RegExp内置对象。
- var reg=new RegExp('正则表达式','匹配模式');
- test()方法，检测字符串是否符合正则表达式，符合返回true，区分大小写检测。
  - reg.test(str);
- i：ignore忽略，忽略大小写检测
- g：global全局，全局匹配
- var reg=/a|b/ig;竖线表示或者
- /[A-z]/;表示A到z，[]也表示或者
- split方法：把字符串以指定符号切割成数组，参数可以传正则表达式，返回结果数一个数组。
  - str.split(/[A-z]/);以字母分隔str字符串。
- search方法：
  - str.search("abc");//返回找到的位置下标，找不到返回-1
  - str.search(/ff/);//参数可以传正则表达式
- replace方法：两个参数，第一个参数是正则表达式，第二个参数是要替换成的新内容。
  - str.replace(/世界/g,"world");替换之后返回新的字符串
- match方法，在字符串中检索指定的值，可以找到一个或多个正则的匹配值。
  - str.match(searchvalue或者reg)；把匹配到的值(字符串)存入一个新数组，然后返回新数组。

[正则表达式全集](http://tool.oschina.net/uploads/apidocs/jquery/regexp.html)

### 转移字符
- 反斜杠：转义字符，\n 换行。

### 立即执行函数
- IIFE：立即执行函数
- 函数声明
- 函数表达式
- 自执行函数，自调用函数
  - 形成封闭区间，声明局部变量，形成早期的模块化概念。
  - 对外公开方法：通过window.num=num;可以在自执行函数外部访问它内部的变量和方法。
  - 通过返回对象统一暴露需要公开的变量和方法。

```
for(var i=0;i<lis.length;i++){
	(function(i){
		lis[i].onclick=function(){
			alert(i+1);
		}
	})(i)
}
```

### 函数对象的方法
- fun.call();
- fun.apply();  ==apply:申请，请求。==
- 这两个方法能够改变函数中this的指向，==使this指向第一个对象参数==。（直接调用函数，函数中this指向的是window。）
- call方法实参传递是逐个传递的，apply方法实参传递是把所有实参放在一个数组传递的。

### 事件的阶段
- 捕获阶段（由外向内开始执行）
- 目标阶段（类名是son的这个元素）
- 冒泡阶段（由内向外开始执行）
- 面试经常会问：是否了解事件的三个阶段？

### 新的事件添加方式
- 给同一个元素添加多个同名事件，后面的事件会覆盖前面的事件，最终只会执行最后添加的那个时间。
- 事件监听：addEventListener，添加事件监听
  - btn.addEventListener("click",function(){},false);
  - 第一个参数，事件名；第二个参数，要执行的函数；第三个参数，布尔值，是否在捕获阶段执行，一般都是false。
  - 这样添加的事件，后面添加的同名事件不会覆盖前面的同名事件，==先添加的先执行,执行函数中this指向的是事件调用者==。
  - IE6、7、8不兼容，替代方法attachEvent,添加多个同名事件，==先执行后添加的，执行函数中this指向的是window==;
  - btn.attachEvent("onclick",function(){});
  - 兼容：
  - function bind(obj,eventName,callback){};

```
<script type="text/javascript">
	function bind(obj,eventName,callBack){
		if(obj.addEventListener){
			obj.addEventListener(eventName,callBack);
		}else{
			obj.attachEvent("on"+eventName,function(){
				callBack.call(obj);
			});
		}
	}
	var btn=document.getElementById("btn");
	bind(btn,"click",function(){
		console.log(this);
	})
</script>
```
### js事件的三个阶段分别为：捕获、目标、冒泡
- 捕获：事件由页面元素接收，逐级向下，到具体的元素
- 目标：具体的元素本身
- 冒泡：跟捕获相反，具体元素本身，逐级向上，到页面元素
- 事件捕获：当使用事件捕获时，==父级元素先触发，子元素后触发==
- 事件冒泡：当使用事件冒泡时，==子级元素先触发，父元素后触发==
- W3C ：任何事件发生时，==先从顶层开始进行事件捕获，直到事件触发到达事件源，再从事件源向上进行事件捕获==
- 标准浏览器：addEventListener("click","doSomething","true")方法,若第三参数为true则采用事件捕获，若为false，则采用事件冒泡
- IE浏览器==只支持事件冒泡，不支持事件捕获==，所以它不支持addEventListener("click","doSomething","true")方法,所以ie浏览器使用ele.attachEvent("onclick",doSomething)
- 事件传播的阻止方法： 
  - 在W3C中，使用 ==stopPropagation()== 方法
  - 在IE下使用==cancelBubble = true==方法
- 阻止默认行为：
  - 在W3c中，使用 ==preventDefault（）== 方法
  - 在IE下==return false==

[javascript高级总结](http://www.cnblogs.com/suihui/p/3186499.html)  
[博客随笔](https://www.cnblogs.com/suihui/category/412532.html)  
[源码下载](http://down.admin5.com/texiao/)  

### 回调函数（callBack）
- 事件里面的触发函数都是回调函数
- animate方法：jQuery中的动画
- 回调函数：自定义的函数，但是不需要你去调用

### 事件委托
- 动态创建的元素，无法获得添加的事件
- 事件委托：动态添加的元素也能具有相同的事件
- 把事件委托给新建元素的父元素
- event.target获取当前触发事件元素
```
<script type="text/javascript">
	var btn=document.querySelector("button");
	var uu=document.querySelector("ul");
	btn.onclick=function(){
		var cLi=document.createElement("li");
		cLi.innerHTML="n";
		cLi.className="lis"
		uu.appendChild(cLi);
	}
	uu.onclick=function(event){
		var event=event||window.event;
		alert(111);
		if(event.target.className=="lis"){
			event.target.style.backgroundColor="blue";
		}
	}
</script>
```







