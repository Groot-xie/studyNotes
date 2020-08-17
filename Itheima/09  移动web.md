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

如果每句 JS 操作都去重绘，浏览器可能受不了，所以浏览器都会优化这些操作

+ 浏览器机制：回流重绘机制

  浏览器会维护一个队列，把所有会引起回流、重绘的操作放入这个队列，等队列中的操作到了一定数量或一定的时间间隔。浏览器就会 flush 队列，进行一次批处理，将多次的回流、重绘变成一次回流重绘

+ 例外情况

  一些代码可以强制浏览器提前 flush 队列，当向浏览器请求一些 style 信息的时候，会让浏览器 flush 队列

  1. offsetTop / offsetLeft / offsetWidth / offsetHeight
  2. scrollTop / scrollLeft / scrollWidth / scrollHeight
  3. clientTop / clientLeft / clientWidth / clientHeight
  4. getComputedStyle() / curremtStyle(IE)

  

> 如何性能优化

本质：减少回流、重绘的次数(需要简单对渲染树的操作)，尤其减少回流

+ 直接使用 className 修改样式，少用 style 设置样式

+ 让要操作的元素进行 <font color=ff0000> 离线处理 </font>,处理完后一起更新。使用 display=none 技术(只会引起两次重绘回流)，减少回流和重绘的次数

  离线处理：

  1. 先 display: none

  2. 设置样式(此时在 DOM 树，不能 render tree)

  3. display: block

     最终只需触发两次回流和重绘

     原理：display： none 的元素不在 render tree 中，设置样式不会引起回流重绘

+ 将需要多次重排的元素，postion 属性设置为 absolute 或 fixed (不影响 render tree 结构，只影响自身，相当于单独渲染)。此时元素脱离文档流，它的变化不会影响到其它元素为动画的 HTML 元素

  例如动画：那么修改它们的 css 是会大大减少 reflow

  C3 实现动画的 transform 变换只有一种视觉效果，所以通过 transform 位移或者变换只会触发重绘，不会触发回流(比position 为 absolute fixed 好)

+ 避免频繁操作 DOM，创建一个 documentFragment，在它上面应用所有 DOM 操作，最后把它添加到文档中

+ 完成功能是前提，在完成功能的情况下优化代码性能

+ 尽量不要将获取性操作放在 for 循环中( 重复渲染性能低下 )

  注意：重绘、回流的作用一方面可以解决一些小bug，其主要作用是性能优化





# 十二、web移动端事件

+ touch 事件：pc 端无法触发

  > touchstart

  触发：手指开始触摸时

  e事件对象( jquery 对 e 对象包装，真正原始事件对象为 e.orginalEvent )：

  1. e.changedTouches 所有发生改变的手指
  2. e.targetTouches 目标对象上的所有手指
  3. e.touches 屏幕上的所有手指

  

  > touchmove

  触发：手指在屏幕滑动时触发

  

  > touchend

  触发：手指离开屏幕触发

  

  > touchcancel

  触发：触摸事件被一些系统事件(电话等)打断时

  应用：一般用于单机游戏暂停

+ 事件对象 e

  1. e.changedTouches
  2. e.targetTouches
  3. e.touches
  4. clientX / clientY 相对于可视区域(浏览器)的xy坐标
  5. screenX / sceenY 相对于屏幕的xy坐标
  6. pageX / pageY 相对于页面文档的xy坐标

  注意：在手指离开屏幕时(touchend)要通过 e.changedTouches 来获取坐标





# 十三、zepto框架(N个模块)

zepto 是一个轻量级的针对现代高级浏览器的 js 库，类似 jquery ，有类似的 api

+ zepto 与 jquery 的区别

  1. jquery 针对 pc 端， 主要用于解决浏览器兼容性问题，zepto 主要针对移动端
  2. zepto 比 jquery 轻量，文本体积更小
  3. zepto 封装了一些移动端手势事件

+ 版本

  1. 生产版
     + zepto
     + event
     + ajax
     + form
     + ie
  2. 开发版(很多模块)
  3. 定制版

+ zepto 定制

  安装 nodejs 环境

  1. 下载 zepto.js
  2. 解压缩
  3. cmd 命令进入解压缩后的目录
  4. 执行 npm i 命令
  5. 编辑 make 文件的 41 行，添加自定义模块并保存
  6. 执行命令 npm run-script dist
  7. 查看目录 dist 构建好的 zepto.js

+ zepto 手势事件(封装 touchstart、touchend、touchmove)

  1. swipe 手指滑动时触发
  2. swipeLeft 左滑时触发
  3. swipeRight 右滑时触发
  4. swipeUp 上滑触发
  5. swipeDown 下滑触发
  6. tap：轻触事件，用于替代移动端的click事件，因为click事件在老版本中会有 300ms 的延迟

  说明：

  1. click 事件在 pc 端非常有用，但在移动端会有 300ms 左右的延迟， 300ms 用于判断双击还是长按事件。只有 300ms 之内没有后续动作发生时才会触发 click 事件

     解决方案：

     + 设置视口，并禁用用户缩放 
     + 使用 tap 事件代替 click (保留用户缩放的功能)

  2. tap 只要轻触了，就会触发，体验更好

  3. 注意：在一些老版本的 iphone 3/4 中，就算设置了视口禁用用户缩放，也有 300ms 延迟，使用第二种方案即可





# 十四、iscroll 插件(版本5，版本4有很多bug)

+ 区域滚动实现原理

  1. 一定要满足父盒子嵌套了子盒子(iscroll 使用时)
  2. 子盒子大小一定要超过父盒子的大小
  3. iscroll 只对元素中的第一个子元素起作用，其它元素会被忽略
  4. iscroll 默认是垂直方向进行滚动的，如需要水平方向滚动，需要传参配置
  5. 为保证计算准确，iscroll 初始化在 window.onload 事件中(保证图片已加载)
  6. 清浮动(准确计算高度)

+ 配置

  ```js
  // 以下为默认配置
  // 都设置为true 可斜滑
  new Iscroll(domId, {
      scrollX: false,
      scrollY: true
  })
  ```





# 十五、响应式布局(媒体查询)

定义：网站能够兼容多个终端(手机、平板、电脑、手表)

+ 为什么要有响应式布局？

  1. pc 端开发的网页已无法满足移动设备的要求
  2. 通常的做法针对移动端单独做一套特定的版本
  3. 如终端越来越多，开发的版本就会越来越多
  4. 响应式布局：一个网页能够兼容多个终端(节约成本开发)

+ 优缺点

  1. 优点
     + 面对不同分辨率设备灵活性强
     + 能够快捷解决多设备显示适应问题
  2. 缺点
     + 兼容各种设备工作量大，效率低下
     + 代码累赘，会出现隐藏无用的元素，加载时间加长
     + 这是一种折中性质的设计解决方法，多方面因素影响而达不到最佳效果
     + 一定程度上改变了网站原有的布局结构，出现用户混淆的情况

+ 响应式开发的现状

  1. 如果已有 pc 的网站，那么一般不会使用响应式开发，针对移动端再开发一套系统
  2. 在新建站点上采用响应式开发的越来越多
  3. 国内，响应式开发还不是特别流行。但响应式开发是大势所趋

+ 响应式开发的原理

  对不同屏幕做兼容，根据屏幕尺寸的变换，给不同元素设置不同样式

+ <font color=ff0000> 设备分类 </font>

  1. 超小屏(手机)   <   768px
  2. 小屏(平板)   768px ~ 992px
  3. 中屏(老式机)   992px ~ 1200px
  4. 大屏(电脑)   > 1200px

+ <font color=ff0000> 媒体查询 </font>

  定义：媒体查询(Media Query)是 css 提出的新属性。通过媒体查询到 screen 的宽度从而指定某个宽度区间的网页布局

  1. 语法

     ```css
     // screen 媒体类型
     @media screen and 条件 {} and...
     ```

  2. 条件写法

     + min-width(最小宽)：只要屏幕宽大于等于这个值的设备就生效
     + max-width(最大宽)：只要屏幕宽度小于这个值的设备就生效
     + width：宽度完全等于这个值时生效

  3. 例子

     ```css
     // 缺点：太繁琐麻烦
     @media screen and (min-width: 1200px) {}
     @media screen and (max-width: 992px) {}
     @media screen and (min-width: 600px) and (max-width: 1000px) {}
     ```

     