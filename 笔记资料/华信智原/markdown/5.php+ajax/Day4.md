### 1.jQuery实现jsonp
```
<script type="text/javascript">
	$(function(){
		$("#btn").click(function(){
			var val=$("#txt").val();
			$.ajax({
				type:"get",
				url:"https://suggest.taobao.com/sug",
				async:true,
				data:{
					q:val,
					jsonp: "theFunction",
					jsonpCallback:"haha"
				},
				dataType:"jsonp",
				success:function (data){
					console.log(data);
				}
			});
			function theFunction(data){
					console.log(data);
				}
		});
	});
</script>
```
[jsonp的jQuery实现](https://www.cnblogs.com/chiangchou/p/jsonp.html)
### 2.模板引擎
- template：模板
- artTemplate
- npm
- 第一步引入template.js文件
- 第二步创建模板：<script type="text/html" id="myHtml"></script>
- 第三部传数据：var html=template("myHtml",data);
- 第四部插入模板引擎：{{each result as value i}}...{{/each}}
- 第五步插入html。
- 显示隐藏：{{if flag}}...{{/if}}
- 显示带标签数据：{{#tag}}

[artTemplate文档](https://aui.github.io/art-template/zh-cn/docs/)

### 3.API接口
- key:2b1cfe3291f14;
- [免费API](http://www.mob.com/product/api)
- 使用PHP实现跨域访问数据
- [curl_init函数用法](https://www.cnblogs.com/bwteacher/p/5685086.html)
- 使用PHP的cURL库可以简单和有效地去抓网页。你只需要运行一个脚本，然后分析一下你所抓取的网页，然后就可以以程序的方式得到你想要的数据了。无论是你想从从一个链接上取部分数据，或是取一个XML文件并把其导入数据库，那怕就是简单的获取网页内 容，cURL 是一个功能强大的PHP库。