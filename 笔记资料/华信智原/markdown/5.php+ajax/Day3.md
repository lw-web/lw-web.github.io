### 1.http状态码
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
- 3xx
  - 301（moved permanently）——永久重定向，原来url不用了，跳转到新的url
  - 302（moved temporarily）——临时性重定向，原来url依旧使用，只是临时跳转到新url
  - 303（see other）——请求对应的资源存在着一个url，应使用GET方法定向获取请求的资源
  - 304（not modified）——未修改，
  - 


### 2.JSON和XML区别
- 轻量、传输速度快、方便创建


### 3.jQueryAjax
- 

### 4.跨域
- 同源策略
- 跨域报错
- src解决跨域问题
- eval----

[ajax常见面试题](https://www.imooc.com/article/23836)