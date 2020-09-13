# `bootstrap Day2`

[在腾讯云服务器上如何发布自己的网站](https://cloud.tencent.com/developer/article/1409411)  

[简单动态网站搭建](https://cloud.tencent.com/edu/learning/course-1064?ADTAG=gw.yjxy)  

[部署与发布（windows & Linux）](https://cloud.tencent.com/edu/learning/course-1063)  

[个人作品网站搭建复盘文章](https://www.jianshu.com/p/9a7928d5fb83)  

[域名.网站备案指南](https://www.jianshu.com/p/6886df5da617) 

[WordPress建站 | 第一篇：五分钟建站基础自学课](https://www.jianshu.com/p/bc24e56092e7) 

[WordPress建站 | 第二篇：建站流程，我是如何稀里糊涂建站的](https://www.jianshu.com/p/3b4d7c9c498f) 

[只要一小时，谁都能轻松建立个人网站](https://www.jianshu.com/p/e238222b05dd) 

[服务器搭建网站完整教程(宝塔面板+WORDPRESS)](https://www.jianshu.com/p/c14fd066cd59)

腾讯云虚拟主机
- 用户名：liwei
- 密码：lw6989661@weixin
- [指导文档](https://cloud.tencent.com/document/product/213/8044)

[less文档地址](http://www.bootcss.com/p/lesscss/)



## 首先我们要进入自己的linux服务器，在命令行输入以下命令安装宝塔面板
- yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh
- 成功之后的账号密码
- Bt-Panel: http://123.207.216.46:8888/7ffadcc1
- username: 98lz5ivn
- password: 5dfedf99



- FTP账号资料
- 用户：webstudylw_club
- 密码：dzwjz5iJH7snjjRG
- 数据库账号资料
- 用户：webstudylw_club
- 密码：yRBRGRNNb5wHxJzx
## 登录后台面板
- 选择
- 如果是512M内存，那么使用默认的配置即可，Mysql 5.5 和 PHP 5.4
- 如果是1G内存，推荐使用wordpress官方给的设置，Mysql 5.6 和 PHP 7.2，但是这里还是建议7.1，兼容的主题会多一些
- 域名：www.webstudylw.club