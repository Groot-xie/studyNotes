# 一、特点

+ 组件简洁大方，代码规范精简，界面自定义强
+ bootstrap 是基于 H5 和 C3 开发的。它在 <font color=ff000>jquery </font>的基础上进行更加人性化 和 个性化 的完善，形成一套自己独有的网编风格，并兼容大部分 jquery 插件
+ bootstrap 包含了丰富的 web 组件，根据这些组件，可以快速搭建一个漂亮、功能完善的网络





# 二、优点

+ 有自己的生态圈，不断更新迭代
+ 提供一套简洁、直观、强悍的组件
+ 标准化的 html + css 编码规范
+ 让开发更简单，提高了开发效率
+ 扩展性强，虽然界面组件样式已经定义好，我们还可以自定义，修改默认样式





# 三、版本

+ 2.x.x 停止维护

  优点：兼容性好。IE 7/8/9

  缺点：代码不够简洁，功能不够完善

+ 3.x.x

  优点：稳定、偏向于开发响应式布局，移动设备优先的 web 项目

  缺点：放弃了 IE6/7，对 IE8 支持，但界面效果不友好

+ 4.x.x 测试版





# 四、CDN内容分发网络

+ 使用别人服务器提供的包，减轻自身服务器压力
+ cdn 可以让用户找到最近的服务器去加载资源包，速度更快





# 五、基础模块

+ 设置视口
+ 引入 css/js 注意依赖问题
+ theme 风格包
+ 提倡扁平化，让页面简洁大方，去掉冗余的效果，渐变





# 六、全局样式 `normalize.css`

+ 定义：`normalize.css` 是一种css rest的替代方案

+ 特点：

  1. 保留有用的浏览器默认样式，而不是完全去除
  2. 一般化的样式
  3. 修复浏览器自身的 bug 并保证各浏览器的一致性，统一各浏览器默认标签样式
  4. 优化 css 可用性

+ 说明：

  `normalize.css` 支持包括手机浏览器在内的超多浏览器。同时对 HTML5 元素排版、列表、嵌入的内容、表单和表格都进行一般化





# 七、container 容器

+ 定义：bootstrap 需要为页面内容和栅格系统包裹一个 `.container容器` 。默认带了 15px 的 padding 值

+ 作用：`.container类` 用于固定宽度并支持响应式布局的容器

+ 特征：

  1.  在不同的屏幕下面，有不同的版心(响应式)

     大屏幕(> 1200px) ----> 1170px

     中屏(992px ~ 1200px) ----> 970px

     小屏(768px ~ 992px) ----> 750px

     超小屏(< 768px) ----> 宽度百分比

  2. `.container-fluid类`用于 100% 宽度，占据全部视口

     + 流式布局容器，宽度 100%
     + 左右 padding 15px

  3. `.row类`用于抵消父类元素的左右 padding 值

     本质：利用的 margin 负值实现





# 八、全局 css 样式(大块一)

+ btn

  1. `.btn-success` 绿色按钮(成功)
  2. `.btn-danger` 红色(危险)
  3. `.btn-info` 浅蓝(一般信息)
  4. `.btn-primary` 蓝色(主要信息)
  5. `.btn-warning` 黄色(警告)
  6. `.btn-defalut` 默认
  7. `.btn-link` 链接样式

+ 标题

  .h1 ~ .h6 类。给内联( inline ) 属性文本赋予标题样式

+ 对齐文本

  1. `.text-left`
  2. `.text-center`
  3. `.text-right`
  4. `.text-justify` 两端对齐(将末尾多余的空间平均分布在行内的空隙中)
  5. `.text-nowrap` 不换行

+ 布局

  1. `.pull-left` 左浮
  2. `.pull-right` 右浮

+ 表格

  1. `.table` 基本样式
  2. `.table-bordered` 表格边距
  3. `.table-hover` 鼠标悬停

+ 按钮

  1. `.btn-lg` 大型
  2. `.btn-sm` 小型
  3. `.btn-xs` 超小型
  4. `.btn-block` 宽度 100% 块级按钮





# 九、栅格系统(网络系统)布局

+ 原理

  浮动 + 百分比 + media 查询

  将容器分为 12 份，12公约数最多

+ 语法：`.col-xx(屏幕)-x(份数)`

  1. lg：large 大屏以上生效
  2. md：middle 中屏以上生效
  3. sm：small 小屏以上生效
  4. xs：xsmall 超小屏以上生效

+ 响应式设计规范

  从小往大进行布局空间分配

+ 栅格系统 --- 列嵌套

  定义：在用栅格布局分配空间的盒子内，再次使用栅格分配空间

+ 栅格系统 --- 列偏移

  1. 百分比的 margin-left

  2. 结合了媒体查询

  3. 语法：`.col-xx-offset-x`

     例如：`.col-md-offset-2` 在中屏以上，给盒子加 2 份的 margin-left





# 十、响应式工具(全局css样式类)

+ `.hidden-xs`
+ `.hidden-sm`
+ `.hidden-md`
+ `.hidden-lg` 大屏隐藏，其它屏不生效(不管)
+ `.hidden`





# 十一、组件(大块二)

+ 字体图标

  在 bootstrap 内部配置好了字体文件路径，直接加类名

+  

  下拉菜单

  响应式导航条

  进度条

  1. role 开头属性，可以直接去除，给盲人设备使用的
  2. aria- 开头的属性可以直接去除，给盲人设备使用的
  3. 设置了 sr-only 类的盒子可以直接去除，给盲人设备使用的
  4. `.progress-bar-danger` 红色(情景颜色)
  5. `.progress-bar-striped` 添加条纹效果
  6. `.active`





# 十二、JavaScript 插件(大块三)

模态框 / 标签页 / 轮播图 Carousel

+ 模态框：外层为蒙层、里层为模态框

  data- 开头的属性，一般都有功能

  1. `data-toggle="modal"` 用于切换模态框的显示
  2. `data-target="#目标id"` 告诉 bootstrap 切换显示的是哪个模态框
  3. 控制大小
     + `modal-lag` 默认为中等，内层加
     + `modal-sm`

+ 轮播图

  1. bootstrap 的轮播图是基于 position：absolute 实现的，注意不要将它覆盖
  2. 由于图片大溢出父盒子，要将基 overflow：hidden

