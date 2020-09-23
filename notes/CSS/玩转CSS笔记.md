# 玩转CSS

## 前言

- VSCode CSS 插件：Caniuse —— 查看CSS兼容性、CSScomb —— 排序CSS属性
- 自动化构建脚手架 bruce-cli
-  项目开发框架 vue，样式与处理 scss
- CSS学习方法
  - 按照类型将CSS属性进行分类并记忆
  - 按照功能将CSS选择器进行分类并记忆
  - 将效果粒度化：将效果进行组件拆分，分析其细节是否能由纯CSS实现，由下往上分析并组装，若每个组件都能由CSS实现，那么大体就能由CSS实现
  - 放弃JS实现效果的固有思维
  - 多浏览设计类网站

## 浏览器

- 浏览器内核
  - Google Chrome：Webkit（前期）、Blink（后期）
  - App Safari：Webkit
  - Mozilla Firefox：Gecko
  - ASA Oprea：Presto（前期）、Blink（后期）
  - Microsoft IExplorer：Trident
  - Microsoft Edge：Trident（前期）、Blink（后期）
- 浏览器渲染过程
  - 解析文件
    - 将 html 文件转换为 DOM 树
      - 字节 —— 字符 —— 标签 —— 节点 —— DOM
    - 将 css 文件转换为 CSSOM 树
      - 字节 —— 字符 —— 标签 —— 节点 —— CSSOM
    - 将 DOM 树和 CSSOM 树合并生成渲染树
      - DOM、CSSOM、渲染树三者没有先后顺序，边加载、边解析、边渲染
  - 绘制图层
    - 根据渲染树布局（回流）
      - 根据渲染树计算每个节点在页面中的布局、尺寸等几何属性
      - 回流：集合属性需要改变的渲染
      - 重绘：更改外观属性而不影响几何属性的渲染
      - 回流必定应发重绘，重绘不一定引发回流
    - 根据布局绘制（重绘）
  - 合成图层
    - 将回流、重绘生成的图层逐张合并并显示在屏幕上
- 浏览器兼容性
  - 查询 CSS/JS 在各种浏览器中兼容性的网站 [Caniuse](https://caniuse.com/)
  - CSS 兼容性的三种方法
    - 磨平浏览器默认样式：[normalize.css](https://github.com/necolas/normalize.css)、[reset.css](https://static.yangzw.vip/css/reset.css)
    - 插入浏览器私有属性：在一些CSS属性前面加入 -webkit- 、-moz-、-ms-、-o-
      - 兼容性写法放到前面，标准写法放到最后
      - 使用 webpack 打包，可以引入 postcss-loader 和 postcss-preset-env 来实现自动添加前缀
    - CSS Hack：针对不同的浏览器编写不同的CSS

## 回流重绘

- 回流：又名重排，指几何属性需要改变的渲染

- 重绘：更改外观属性而不影响几何属性的渲染

- 属性分类

  - 几何属性：包括布局、尺寸等可用数学几何衡量的属性
    - 布局：display、float、position、list、table、flex、columns、grid
    - 尺寸：margin、padding、border、width、height
  - 外观属性：包括界面、文字等可用状态向量描述的信息
    - 界面：appearance、outline、background、mask、box-shadow、box-reflect、filter、opacity、clip
    - 文字：text、font、word

- 性能优化

  - 引发性能问题的场景：

    - 改变窗口大小
    - 修改盒模型
    - 增删样式
    - 重构布局
    - 重设尺寸
    - 改变字体
    - 改动文字

  - 浏览器事件循环（[HTML文档](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)）

    - 浏览器刷新频率为 60HZ，即每16.6ms更新一次
    - 事件循环执行完成微任务
    - 判断 document 是否需要更新
    - 判断 resize/scroll 事件是否存在，存在则触发事件
    - 判断 Media Query 是否触发
    - 更新动作并发送事件
    - 判断 document.isFullScreen 是否为 true（全屏）
    - 执行 requestAnimationFrame 回调
    - 执行 IntersectionObserver 回调
    - 更新界面

  - 如何减少和避免回流重绘

    - 使用 transform 代替 top
    - 使用 visibility：hidden 代替 display：none
      - 占位表现
        - DN不占据空间
        - VH占据空间
      - 触发影响
        - DN触发回流重绘
        - VH触发重绘
      - 过渡影响
        - DN影响过渡不影响动画
        - VH不影响过渡不影响动画
      - 株连效果
        - DN后自身及其子节点全都不可见
        - VH后自身及其子节点全都不可见，但是可以声明子节点 visibility：visible 单独显示
    - 避免使用 table 布局
    - 避免样式节点层级过多：CSS规则是从右到左匹配查找，样式层级过多会影响回流重绘效率，建议保持CSS规则在3层左右

    - 将频繁回流或者重绘的节点设置为图层
      - 设置新图层有两种方法：将节点设置为 video 或 iframe；为节点添加 will-change 属性
    - 动态改变类名而不改变样式
    - 避免节点属性值放在循环里当成循环变量
    - 使用 requestAnimationFrame 作为动画速度帧

- 属性排序：按照预设规范排列 CSS 属性

  - 属性排序顺序：布局 —— 尺寸 —— 界面 —— 文字 —— 交互
  - 布局属性
    - 显示：display、visibility
    - 溢出：overflow、overflow-x、overflow-y
    - 浮动：float、clear
    - 定位：position、left、right、top、bottom、z-index
    - 列表：list-style、list-style-type、list-style-position、list-style-iamge
    - 表格：table-layout、border-collapse、border-spacing、caption-side、empty-cells
    - 弹性：flex-flow、flex-direction、flex-wrap、justify-content、align-content、align-items、align-self、flex、flex-grow、flex-shrink、flex-basis、order
    - 多列：columns、column-width、column-count、column-gap、column-rule、column-rule-width、column-rule-style、column-rule-color、column-span、column-fill、column-break-before、column-break-after、column-break-inside
    - 格栅：grid-columns、grid-rows
  - 尺寸属性
    - 模型：box-sizing
    - 边距：margin、margin-left、margin-right、margin-top、margin-bottom
    - 填充：padding、padding-left、padding-right、padding-top、padding-bottom
    - 边框：border、border-width、border-style、border-color、border-colors、border-[direction]-<param>
    - 圆角：border-radius、border-image-source、border-image-slice、border-image-width、border-image-outset、border-image-repeat
    - 大小：width、min-width、max-width、height、min-height、max-height
  - 界面属性
    - 外观：appearance
    - 轮廓：outline、outline-width、outline-style、outline-color、outline-offset、outline-radius、outline-radius-[direction]
    - 背景：background、background-color、background-image、background-repeat、background-repeat-x、background-repeat-y、background-position、background-position-x、background-position-y、background-size、background-origin、background-clip、background-attachment、background-composite
    - 遮罩：mask、mask-mode、mask-iamge、mask-repeat、mask-repeat-x、mask-repeat-y、mask-position、mask-position-x、mask-position-y、mask-size、mask-origin、mask-clip、mask-attachment、mask-composite、mask-box-iamge、mask-box-image-source、mask-box-image-width、mask-box-image-outset、mask-box-image-repeat、mask-box-image-slice
    - 滤镜：box-shadow、box-reflect、filter、mix-blend-mode、opacity
    - 裁剪：object-fit、clip
    - 事件：resize、zoom、cursor、pointer-events、touch-callout、user-modify、user-focus、user-input、user-select、user-drag
  - 文字属性
    - 模式：line-height、line-clamp、vertical-align、direction、unicode-bidi、writing-mode、ime-mode
    - 文本：text-overflow、text-decoration、text-decoration-line、text-decoration-style、text-decoration-color、text-decoration-skip、text-underline-position、text-align、text-align-last、text-justify、text-indent、text-stroke、text-stroke-width、text-stroke-color、text-shadow、text-transform、text-size-adjust
    - 字体：src、font、font-family、font-style、font-stretch、font-weight、font-variant、font-szie、font-size-adjust、color
    - 内容：overflow-wrap、word-wrap、word-break、word-spacing、letter-spacing、white-sapce、caret-color、tab-size、content、counter-increment、counter-reset、quotes、page、page-break-before、page-break-after、page-break-inside
  - 交互属性
    - 模式：will-change、perspective、perspective-origin、backface-visibility
    - 变换：transform、transform-origin、transform-style
    - 过滤：transition、transition-property、transition-duration、transition-function、transition-delay
    - 动画：animation、animation-name、animation-duration、animation-timing-function、animation-delay、animation-iteration-count、animation-direction、animation-play-state、animation-fill-mode

- 配置

  - 自动排列CSS属性的网站[Csscomb](https://csscomb.com/)
  - 配置快捷键，保存自动对 CSS 代码进行排序

## 盒模型

- 组成：box = margin + border + padding + content

  - 注意点：padding 部分会随着 background-color 改变，可使用 background-clip 隔离

- 类型：标准盒模型、怪异盒模型

  - CSS3里面对应属性 box-sizing：content-box（标准）、border-box（怪异）
  - 标准盒模型：由 margin + border + padding + content 组成，节点的 height/width 只包含 content，不包含 padding 和 border
  - 怪异盒模型：IE盒模型，由 margin + content 组成，节点的 height/width 包含 border、padding、content

- 视觉格式化模型

  - 块级元素：display 声明为 block、list-item、table、flex、grid 的时候，节点被标记为块级元素；块级元素默认宽度 100%，在垂直方向上按顺序放置
  - 行内元素：display 声明为 inline、inline-block、inline-table、inline-flex、inline-grid 时，该节点被标记为行内元素，行内元素默认宽度为 auto，在水平方向按顺序放置
  - 互相转换
    - 块级元素转行内元素 display：inline
    - 行内元素转块级元素 display：block
  - 占位表现
    - 块级元素默认单独占一行，默认宽度为父元素的 100%，可声明边距、填充、宽高
    - 行内元素默认不独占一行，默认宽度随内容自动撑开，可声明水平边距和填充，不可声明垂直距离和宽高
  - 包含关系
    - 块级元素可包含块级元素和行内元素
    - 行内元素可包含行内元素，不能包含块级元素

- 格式化上下文

  - 格式化上下文指决定渲染区域里节点的排版、关系和相互作用的渲染规则。简单来说就是页面中有一个 ul 及其多个子节点 li，格式化上下文决定这些 li 如何排版，li 与 li 之间处于什么关系，以及 li 与 li 之间如何相互影响

  - 格式化上下文组成
    - 块格式化上下文 —— BFC —— 块级盒子容器
    - 行内格式化上下文 —— IFC —— 行内盒子容器
    - 弹性格式化上下文 —— FFC —— 弹性盒子容器
    - 格栅格式化上下文 —— GFC —— 格栅盒子容器
  - BFC 是页面上一个独立且隔离的渲染区域，容器里面的子节点不会在布局上影响到外面的节点，反之亦然
    - 规则
      - 子节点在垂直方向上按顺序放置
      - 子节点的垂直方向距离由 margin 决定，相邻节点的 margin 会发生重叠，以最大的 margin 为合并值
      - 每个节点的 margin-left/right 与父节点的 左边/右边 相接触，即使处于浮动也如此，除非自行形成 BFC
      - BFC区域不会与同级浮动区域重叠
      - BFC是一个隔离且不受外界影响的独立容器
      - 计算BFC高度时其浮动子节点也参与计算
    - 成因
      - 根节点：html
      - 非溢出可见节点 —— overflow：!visible
      - 浮动节点 —— float：left/right
      - 绝对定位节点 —— position：absolute/fixed
      - 被定义成块级的非块级节点 —— display：inline-block/table-cell/table-caption/flex/inline-flex
      - 父节点与正常文档流的子节点（非浮动）自动形成 BFC
    - 场景
      - 清除浮动
      - 已知宽度水平居中
      - 防止浮动节点被覆盖
      - 防止垂直 margin 合并
    - margin塌陷：两个BFC的相邻盒或父子盒相互作用时产生的效果，两个盒子会取相临边最大 margin 作为相临边的公用 margin
  - 行内格式化上下文 IFC 的宽高由行内子元素中最大的实际高度决定，不受垂直方向的margin 和 padding 影响
    - 规则
      - 节点在水平方向上按照顺序放置
      - 节点无法指定宽高，其 margin 和 padding 在水平方向有效在垂直方向无效
      - 节点在垂直方向上以不同形式对齐
      - 节点的宽度由包含块和浮动决定，高度由行高决定
    - 成因
      - 行内元素 —— display：inline[-x]
      - 声明 —— line-height
      - 声明 ——  vertical-align
      - 声明 —— font-size
  - 弹性格式化上下文 —— 声明 display 为 flex 或者 inline-flex 时
  - 格栅格式化上下文 —— 声明 display 为 grid 或者 inline-grid 时

- 文档流 —— 节点在排版布局过程中默认使用从左往右、从上往下的流式排列方式。

  - 三个常见缺陷
    - 空白折叠：HTML中换行编写行内元素，排版会出现 5px 空隙
      - 紧密连接节点，取出换行
      - 子节点增加 margin-left：-5px
      - 使用 flex 布局，居中显示 display：flex；justify-content：center；
    - 高矮不齐：行内元素统一以底边垂直对齐
    - 自动换行：排版若一行无法完成则换行接着排版
  - 























