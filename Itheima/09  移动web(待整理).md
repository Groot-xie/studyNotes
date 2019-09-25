# 一、移动web开发现状

+ 屏幕尺寸

  移动端屏幕尺寸非常多，碎片化严重，需要进行不同的适配(百分比布局)

+ 浏览器兼容

  移动端内核大都是 webkit 内核，就算要兼容，只需加 -webkit- 前缀即可。移动端对 C3 支持良好



# 二、移动开发分类

> 原生app(native app)

+ 特点
  1. 可直接在手机上安装，通过 java(Android)、swift(Ios) 等语言开发
  2. 可直接访问手机中的设备(摄像头、GPS定位等)
  3. 性能佳
  4. 可离线访问
+ 缺点
  1. 开发成本高，开发多套程序，跨平台性差
  2. 需要更新版本，麻烦



> web应用(webapp)

+ 特点
  1. 直接在浏览器中运行，由 html / css / js 开发
  2. 开发成本低，只需一套开发，跨平台性好
+ 缺点
  1. 不能访问手机硬件设备(GPS、摄像头等)
  2. 性能方面较差
  3. 不能离线访问



> 混合app(hybrid app)

+ 特点
  1. 可进行安装，在webapp外套原生app的壳
  2. 可访问手机硬件设备
  3. 内部本质还是网页(html / css / js)，跨平台性好



# 三、屏幕尺寸与屏幕分辨率

+ 屏幕尺寸：屏幕对角线的长度。单位：英寸。 1 英寸 = 2.54厘米
+ 屏幕分辨率：手机横向和纵向有多少个<font color=ff0000> **物理像素点**</font>



# 四、相对长度单位和绝对长度单位

+ 物理像素是一个相对长度单位，随屏幕质量的提高而改变。屏幕质量越好，画质越精细，物理像素点越多，越小。
+ 绝对长度单位：1cm、1英寸、1m等



# 五、像素密度(ppi)

+ 定义：像素密度 ppi (pixel per inch)。单位英寸的像素点个数

+ 作用：衡量不同屏幕的清晰度，屏幕质量

+ 说明：像素密度越大，说明单位长度的像素点个数越多，屏幕越清晰

+ 公式：
  $$
  ppi = \frac{\sqrt{长^{2}+宽^{2}}}{英寸}
  $$
  



# 六、设备独立像素(设备无关像素)

+ 定义：跟设备无关的像素，保证图像内容在不同的 PPI 设备看上去大小差不多

+ 叫法： IOS ----> PT   Android ----> DP   CSS ----> PX

+ 获取设备像素比

  ```js
  // 物理像素 与 css像素的比值
  window.devicePixelRatio
  ```

  $$
  DPR = \frac {物理像素} {css像素}
  $$

  



# 七、二倍三倍图

把更多的像素点压缩至一块屏幕里，从而达到更高的分辨率并提高屏幕显示的细腻程度

+ 经典2倍图： 640(320屏幕)    750(375屏幕)   720(360屏幕)
+ 经典3倍图：1080(360屏幕)
+ 结论：移动端为了在高清屏上显示更加细腻，通常会使用更大的图片，比如二倍、三倍图





# 八、视口 viewport

+ 定义：视口是一个容器，默认宽度980px，且可缩放。用于存放网页，介于手机设备 和 html 页面之间的容器

+ pc 网页宽度由浏览器宽度决定

+ 移动端的宽度由视口宽度决定，视口宽度980px

+ 视口设置

  meta:vp + tab键

  ```html
  <!-- 
      width="device-width" 宽度=设备宽度
      user-scalable="no" 用户是否可缩放
      initial-scale="1.0" 默认视口缩放比1.0不缩放
      maximum-scale="1.0" 最大缩放比
      minimum-scale="1.0" 最小缩放比
  -->
  <meta 
        name="viewport"
        width="device-width"
        user-scalable="no"
        initial-scale="1.0"
        maximum-scale="1.0"
        minimum-scale="1.0"
        content="width=device-width, initial-scale=1.0">
  ```

  



# 九、流式布局

> 移动端特点

+ 手机端的兼容问题比 pc 端小很多
+ 手机端屏幕小，能够存放的内容少
+ pc 端：固定版心
+ 移动端：采用流式布局(百分比布局)



> 流式布局(百分比布局)

+ 特征
  1. 宽度自适应，高度写死，并不是百分百还原设计图
  2. 图标都是固定死大小的，包括字体
  3. 一些大的图片，设置宽高为百分比自适应即可，随屏幕大小进行变化
+ 经典流式布局
  1. 左侧固定，右侧自适应(定位 position、flex布局)
  2. 右侧固定，左侧自适应(BFC 实现 + 浮动)
  3. 两侧固定，中间自适应(圣杯布局、双飞翼布局)
  4. 等分布局
+ 移动端布局注意点
  1. 一般都会给所有盒子设置 box-sizing：border-box
  2. 要设置视口



> BFC 块级格式化上下文

Block Formatting Context：页面上一个隔离的独立渲染区域

+ BFC盒子的特点
  1. 触发 BFC 的盒子，成为页面上一个隔离的独立容器，容器里的子元素不会在布局上影响到外面的元素。应用：解决塌陷问题，清楚浮动影响
  2. <font color=ff0000>触发了 BFC 的普通盒子，不会与浮动元素重叠</font>，应用：圣杯布局，左侧固定右侧自适应
+ 如何触发 BFC
  1. float：left / right
  2. overflow： 不为visible
  3. display：inline-block / table-cell / table-caption / flex / inline-flex...
  4. position：absolute / fixed





# 十、京东项目

+ a标签样式

  -webkit-top-highlight-color: transparent/rgba()     ---->    top轻触事件

+ 多行溢出

  ```css
  p {
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
  }
  ```

+ 单行溢出

  ```css
  p {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
  }
  ```

+ 知识点

  JS 执行的进程和浏览器的进程是互斥的。同时只能有一个运行，也就是说 js 主线程完全执行之后浏览器才开始渲染





# 十一、重绘和回流(页面性能优化)

> 浏览器渲染机制(呈现过程)

1. 解析 HTML 以构建 DOM 树

   浏览器把获取到的 HTML 代码解析成一个 DOM 树，HTML 中的每个标签都是 DOM 树的一个节点

2. 解析 CSS 样式表

   浏览器把所有样式解析成样式结构体，在解析的过程中会去不能掉识别的样式。比如 IE 会去掉 -moz- 开头的，FF 会去掉 - 开头的样式

3. 构建渲染树

   Dom + Tree + 样式结构体 = render tree

   render tree 不同 DOM 树，它能识别样式

   render tree 中的每个 node 都有自己的 style

   且 render tree 不包含隐藏节点(如：display：none的节点，还有 head 节点)

   一旦 render tree 构建完毕后，浏览器就可以根据 render tree 来绘制页面

4. 布局渲染树：从根节点递归调用，计算每一个元素的大小、位置等，给每个节点所应该出现在屏幕上的精确坐标

5. 绘制渲染树：遍历渲染树，每个节点都使用 UI 后端层绘制

说明：ul.offsetWidth 是获取性操作，能让浏览器提前渲染队列(获取性操作，浏览器保护获取的准确性，先进行之前代码的渲染，保证在此位置获取到的是之前代码执行过的数值)



> 重绘与回流

+ 回流 reflow

  发生在第四阶段，当 render tree 中的一部分或全部因元素的规模尺寸、布局、隐藏等改变而需要重新构建

+ 重绘 repaint

  发生在第五阶段，当 render tree 中的一些元素需要更新属性，而这些属性只是影响元素的外观、风格、而不影响布局的。如 background-color等

+ 关系

  1. 每一个页面至少需要一次回流+重绘
  2. 回流必将引起重绘

+ 回流发生条件

  1. 添加或删除可见的 DOM 元素
  2. 元素位置改变
  3. 元素尺寸改变(边距、填充、边框、宽、高等)
  4. 内容改变(文本改变、图片大小改变而引起的计算值，宽度和高度改变)
  5. 页面渲染初始化
  6. 浏览器窗口改变(resize事件发生时)



> 浏览器
>
> 如何性能优化