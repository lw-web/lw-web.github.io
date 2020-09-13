### 1.标准盒模型
- 存在问题：布局时border和padding会撑大盒模型
- 非标准盒模型
  - box-sizing:content-box;
  - box-sizing:border-box;
  - IE8以上才兼容

### 2.flex布局：弹性盒子布局
- IE10以上才支持，移动端可大胆使用
- display:flex/inline-flex;定义盒子为弹性容器。
- dispaly:-webkit-flex;兼容webkit内核浏览器兼容。
- 设置为flex后，子元素的float、clear、vertical-align就不生效了。
- 容器：父元素；项目：子元素；主轴：main axis；交叉轴：cross axis；主轴开始结束位置：main start/end；交叉轴开始结束位置：cross start/end；项目占据位置：main size/cross size;
- 容器属性（添加给父元素的属性）：
  - flex-direction：决定主轴的方向（即项目的排列方式）。
    - row：默认值，方向水平从左向右；float：left；
    - row-reverse：水平从右往左；float：right；
    - column：列方式排列从上往下；
    - column-reverse：从下往上；
  - flex-wrap：决定项目排不下时如何换行。
    - nowrap：默认值，不换行；
    - wrap：正常换行，多出的排在下面；
    - wrap-reverse：多出的排在上面；
  - flex-flow：就是flex-direction和flex-wrap的简写合并；
  - justify-content：定义项目在主轴上的对齐方式。
    - center：项目居中；
    - flex-start：默认值，左对齐；
    - flex-end：右对齐；
    - space-between：两端对齐，项目之间距离等分；
    - space-around：每个项目之间间隔相等，项目与父元素之间距离是项目之间距离的一半；
  - align-items：定义项目在交叉轴上的对齐方式。
    - center：居中；
    - flex-start：顶部对齐；
    - flex-end：底部对齐；
    - baseline：项目第一行文字基线对齐；
    - stretch：默认值；
  - align-content：定义多根轴线的对齐方式。（用的不多）
- 项目属性（添加给子元素的属性）：
  - flex-grow：弹性分组，默认值0，1占满剩余空间。==加了该属性，width属性就失效了。==
  - flex-shrink：项目缩小比例。
  - align-self：允许项目有不同于其他项目的属性。可覆盖父元素的align-items属性。
  

[阮一峰日志](http://www.ruanyifeng.com/blog/archives.html)

### 3.视口：meta标签
- meta_viewport
- name=viewport；
- content="width=device-width（设置宽度为视口宽度）,initial-scale=1（设置初始缩放为1）,minimum-scale=1（设置最小缩放比例为1）,maxmum-scale=1（设置最大缩放比例为1）,user-scalable=no（禁止用户缩放）";//为移动端设计的标签

### 4.CSS3媒体查询
- @media only screen and(max-width:600px){div{...}};
- @media only screen and(min-width:601px) and (max-width:800px){div{...}};
- @media only screen and(min-width:801px) and (max-width:960px){div{...}};
- @media only screen and(min-width:961px){div{...}};



### 1.页面尺寸分区
- 超小屏幕768px以下
- 小屏幕768px到992px
- 中等屏幕992px以上
- 大屏幕1200px以上

### 2.尺寸单位（面试题）
- rem：root相对于根元素值大小的倍数
- html{font-size：16px;//Chrome默认大小是16px，最小是12px}
  - 在媒体查询中改变根元素font-size大小，可实现动态页面布局；
- 1rem=16px；
- em：相对其父元素字体值大小的倍数
- px：固定值
- rem配合媒体查询代码




[电子书查询网站](https://www.jiumodiary.com/)  
[资源搜索网站](https://www.chongbuluo.com/)  
[网站设计欣赏](https://www.xuansite.com/)