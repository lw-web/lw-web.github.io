### 1.什么是AJAX，为什么要使用AJAX？
- 什么是ajax：
  - ajax是“Asynchronous JavaScript and XML”的缩写，指的是一种创建交互式互联网页面应用的页面开发技术。
  - ajax包含以下技术：
    - 基于WEB标准XHTML+CSS的表示；
    - 使用DOM进行动态显示及交互；
    - 使用XML和XSLT进行数据交换及相关操作；
    - 使用XMLHTTPREquest进行异步数据查询、检索；
    - 使用JavaScript将所有东西绑定在一起。
- 为什么使用ajax：
  - ajax的优势在于：
    - 通过异步模式，提升了用户体检；
    - 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了宽带占用；
    - ajax引擎在客户端运行，承担了一部分本来由服务器承担的工作，从而减少了大量用户下的服务器荷载；

### 2.ajax的最大特点是什么？
- ajax可实现动态不刷新（局部刷新）；就是能够在不更新整个页面的前提下维护数据。这使得web应用程序更为迅捷的回应用户动作，并避免了在网络上发送那些没有改变过来的无效信息。

### 3.请介绍一下XMLHttpRequest对象。
- ajax的核心是JavaScript的XMLHttpRequest对象。该对象在Internet Explorer5中首次引入，它是一种支持异步请求的技术。简而言之，XMLHttpRequest使我们能够使用JavaScript向服务器发送请求，而不阻塞用户。通过XMLHttpRequest对象，web开发人员可以再页面加载以后进行页面的局部更新。

### 4.ajax技术体系的组成部分。
- HTML、CSS、DOM、XML、XMLHttpRequest、JavaScript

### 5.ajax应用和传统web应用有什么不同？
- 在传统的JavaScript编程中，如果想得到服务器端的数据库或者文件上的信息，或者发送客户端信息到服务器，需要建立一个form表单然后get或者post数据到服务器端。用户需要点击submit按钮来发送或者接收数据信息，然后等待服务器响应请求，页面重新加载。
- 因为每次服务器都会返回一个新的页面，所以传统的web应用有可能很慢而且用户交互不友好。
- 使用ajax技术，就可以使JavaScript通过XMLHttpRequest对象直接与服务器进行交互。
- 通过HTTP Request，一个web页面可以发送一个请求到web服务器从并且接受web服务器返回的信息（不用重载页面），展示给用户的还是通过一个页面，用户感觉不到页面刷新，也看不到JavaScript后台进行的发送请求和接收响应，提升用户体检。

### 6.ajax共有多少种callback？
ajax共有8中callback：
- onSuccess
- onFailure

### 7.ajax和JavaScript的区别
- JavaScript是一种在浏览器端执行的脚本语言，ajax是一种创建交互式页面应用的开发技术，它是利用了一系列相关技术，其中就包括JavaScript。  
- 在一般的web应用中JavaScript实在浏览器端执行的，我们可以使用JavaScript控制浏览器的行为和内容。
- 在ajax应用中信息是在浏览器和服务器之间传递的，通过xml（json）数据或者字符串。

### 8.在浏览器端如何得到服务器端的XML数据？
- XMLHttpRequest对象的responseXML属性。

### 9.XMLHttpRequest对象在IE和Firefox中创建方式有没有不同？
- 有，IE中通过new ActiveXObject()创建，Firefox中通过new XMLHttpRequest()创建；

### 10.介绍一下XMLHttpRequest对象的常用方法和属性。
- open(method,url);建立对服务器的调用，第一个参数是HTTP请求方式，可以为get或者post；第二个参数是请求页面的url；
- send();方法，发送具体请求；
- abort();方法，停止当前请求；
- readyState属性，请求的状态，有5个可取值：
  - 0——未初始化；
  - 1——正在加载；
  - 2——已加载；
  - 3——交互中；
  - 4——完成。
- responseText属性，服务器的响应，表示为一个字符串；
- responseXML属性，服务器的响应，表示为XML；
- status属性，副武器的HTTP状态码，200对应ok，400对应not found

### 11.什么是XML
- XML是扩展标记语言，能够用一系列简单的标记描述数据。

### 12.XML的解析方式
- 常用的有DOM解析和Sax解析。DOM解析是一次性读取XML的文件并将其构造为DOM对象以供使用，优点是操作方便，但是比较耗内存。Sax是按事件驱动的方式解析的，占用内存少，但是变成复杂。

### 13.ajax的优缺点
优点：
- 最大的优点就是页面无刷新，用户体检非常好；
- 使用异步加载方式与服务器通信，具有更加迅速的响应能力；
- 可以把一些服务器负担的工作转嫁到客户端，利用客户端闲置的能力来处理，减轻服务器和宽带的负担，节约空间和宽带租用成本。并减轻服务器的负担，ajax的原则是“按需取数据”，可以最大程度的减少冗余请求，和响应对服务器造成的负担；
- 基于标准化的并且被广泛支持的技术，不需要下载插件或者小程序。

缺点：
- ajax不支持浏览器back按钮；
- 安全问题ajax暴露了与服务器交互的细节；
- 对搜索引擎的支持比较弱；
- 破坏了程序的异常机制；
- 不容易调试。

### 14.ajax的全称是啥？介绍一下ajax。
- ajax：Asynchronous JavaScript And XML，指的是一种创建交互式互联网页面应用的页面开发技术。
- ajax不是一个新的编程语言，它是一门使用已有标准的新的编程技术。
- 使用ajax可以创建更好、更快、用户界面有好的web应用。ajax技术基于JavaScript和HTTP Request。

### 15.ajax的工作原理
- ajax的核心是JavaScript对象XMLHttpRequest。该对象是一种支持异步请求的技术。简而言之，XMLHttpRequest使我们能够使用JavaScript向服务器提出请求并处理响应，而不阻塞用户。在创建web站点时，在客户端执行内容更新为用户提供了很大的灵活性。

### 16.status属性HTTP状态码。
- 类别
  - 1xx：information（信息性状态码）——接收的请求正在处理
  - 2xx：success（成功状态码）——请求正常处理完毕
  - 3xx：redirection（重定向状态码）——需要进行附加操作以完成请求
  - 4xx：client error（客户端错误代码）——服务器无法处理请求
  - 5xx：server error（服务器端错误状态码）——服务器处理请求错误
- 2xx——相应结果表明请求被服务器正常处理了
  - 200（ok）——客户端请求被服务器正常处理
  - 204（not content）——类似于200，但是服务器不会也不允许返回任何资源实体
  - 206（partial content）——表示客户端进行了范围请求，服务器成功执行了这部分的GET请求
- 3xx——除了304，其余都和重定向相关
  - 301（moved permanently）——永久重定向，原来url不用了，跳转到新的url
  - 302（moved temporarily）——临时性重定向，原来url依旧使用，只是临时跳转到新url
  - 303（see other）——请求对应的资源存在着一个url，应使用GET方法定向获取请求的资源
  - 304（not modified）——未修改，表示客户端发送带条件请求时，服务器端允许请求访问资源，但因为发生请求为满足条件的情况后，直接返回304 not modified（服务器端资源未改变，可以直接使用客户端未过期的缓存）；
  - 307（Temporary Redirect）——临时重定向，和302类似，只是不会将post请求变成get请求；
- 4xx——都是客户端出现错误的原因，比如请求语法错误（400）、需要认证（402）、权限不够（403）、输入错误URL（404）
  - 400（Bad Request）——请求错误，请求报文中存在语法错误；
  - 401（Unauthorized）——非法的、未授权的，表示发送的请求需要有通过HTTP认证的认证信息；
  - 403（Forbidden）——被禁止的、严禁的，表示对服务器的请求访问被拒绝了；
  - 404（not Found）——未找到，服务器上无法找到请求的资源；
- 5xx——是服务器本身发生错误而引起的
  - 500（Internal Server Error）——内部服务器错误，服务器端在执行请求时发生了错误，也有可能是web应用存在bug或者某些临时的故障；
  - 503（Service Unavailable）——服务不可用、无法提供服务，表明服务器暂时处于超负载或者正在进行停机维护，现在无法处理请求；

### 17.ajax实现流程
原生JS实现：
- get请求：

```
var xhr=new XMLHttpRequest();
xhr.open("get","url?参数1="+变量1+"&参数2="+变量2)；
xhr.send(null);
xhr.onreadystatechange=function(){
    if(xhr.readyState==4 && xhr.status==200){
        var result=xhr.responseText;
    }
}
```
- post请求：

```
var xhr=new XMLHttpRequest();
xhr.open("post","url");
var parm="参数1="+变量1+"&参数2="+变量2;
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded"));
xhr.send(parm);
xhr.onreadystatechange=function(){
    if(xhr.readyState==4 && xhr.status==200){
        var result=xhr.responseText;
    }
}
```
jQuery实现：
- get方法：

```
$.get("url",{
    "参数1":变量1,
    "参数2":变量2
},function(data){
    var result=data;
});
```
- post方法：

```
$.post("url",{
    "参数1":变量1,
    "参数2":变量2
},function(data){
    var result=data
});
```
- ajax方法：

```
$.ajax({
    url:"url",
    type:"get/post",
    async:true,
    data:{
        "参数1":变量1,
        "参数2":变量2
    }，
    success:function(data){
        var result=data;
    },
    error:function(e){
        console.log(e.statusText);
    }
});
```

### 18.jsonp实现流程
原生Js实现：

```
var script=document.createElement(script);
script.src="url?callback=fun";
document.querySeclector("head").appendChild(script);
window["fun"]=function(data){
    var result=data;
}
```
jQuery实现：

```
$.ajax({
    url:"url",
    type:"get/post",
    async:true,
    dataType:"jsonp",
    data:{
        "callback":"fun"
    }
});
function fun(data){
    var result=data;
}
```