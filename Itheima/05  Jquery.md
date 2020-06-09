+ jquery 官网：https://jquery.com/
+ jquery：本质为 JS 库中的一种
+ js 库：本质为 js 文件，将平时常用的函数封装到 js 文件中，使用时引入
+ jquery 版本
  1. 功能丰富，主要用于兼容 IE678(学这个版本)
  2. 是在 1.x 版本赋值一份，删除兼容 IE678 的功能
  3. 在 2.x 的基础上开发，新增一些 API



# 一、JQ 的入口函数

函数体中写代码

+ 入口函数

  ```js
  $(document).ready(function () {
  
  })
  // 简洁的入口函数
  $(function () {
  
  })
  ```

+ 好处

  + 不论代码位置可正常使用
  + 防止全局污染

+ 与 `window.onload` 的区别

  1. `window.onload` 存在覆盖性问题，JQ的入口函数不存在覆盖性问题

  2. 执行时机不同

     + `window.onload` 

       网页加载完毕，外部资源(css、js、img)全部加载完成后才执行

     + jq 入口函数

       只等网页加载完成便执行

+ 几个相关事件

  jq 的入口函数是否使用的是 `window.DomContentLoaded` 事件？？？

  ```js
  // 每次页面打开都触发，即使是从缓存中取的页面
  window.onpageshow
  // 
  window.onpagehide
  // 页面加载全部完成后触发，缓存页面不触发
  window.onload
  // true:缓存中的页面 false：不是
  e.persisted
  ```



# 二、JQ 使用步骤

1. 引入 jquery
2. 写入口函数
3. 在入口函数里实现功能



# 三、Jquery 对象 和 DOM 对象

+ DOM 对象：使用原生 JS 获取元素的方法返回的对象

  例如：`document.getElementById()`  `document.querySelectorAll()`

  + <font color=red> DOM 对象不能使用 JQ 的方法 </font>

+ JQ 对象：通过 Jquery 提供的 `$()` 方法获取元素返回的对象

  例如：`$('div')`

  + JQ 对象是一个伪数组，存的是获取到的 DOM 对象
  + <font color=red> JQ 对象不能使用 DOM 对象的属性和方法 </font>(下一条解决)

+ 解决

  + JQ 对象想要使用 DOM 的方法，需要将 DOM 对象转成 JQ 对象

    `$(dom)` 将 DOM 对象作为参数传入 `$()` 中

  + DOM 对象想要使用 JQ 对象的属性和方法，通过下标取出对应的 DOM 对象即可，也可通过 `.get()` 获取



# 四、$ 详解

除了 `$` 符，也可以使用 jquery ，为 jquery 的顶级对象

+ `$` 来源：jquery 引入
+ `$` 是函数
+ 作用：根据参数不同，作用不同
  + 获取元素 `$('div')`
  + 入口函数 `$(function() {})`
  + 将 DOM 对象转为 JQ 对象 `$(dom对象)` 参数：dom对象
  + 创建元素 `$('html字符串')`



# 五、选择器

返回 jquery 对象

+ 选择器

  ```js
  // id
  $('#yange')
  // 标签
  $('li')
  // 类名
  $('.btn')
  // 交集(连写)
  $('#yange.li')
  // 并集(逗号)
  $('#yange,.mage')
  // 子代
  $('.mage>ol>li')
  // 后代(空格)
  $('.mage li')
  ```

+ 过滤选择器

  | 选择器     | 说明                                         | 示例          |
  | ---------- | -------------------------------------------- | ------------- |
  | :odd       | 从获取到的所有元素中，过滤出下标为奇数的元素 | $('li:odd')   |
  | :even      | 从获取到的所有元素中，过滤出下标为偶数的元素 | $('li:even')  |
  | :first     | 从获取到的元素中过滤出第一个元素             | $('li:first') |
  | :last      | 从获取到的元素中过滤出最后一个元素           | $('li:last')  |
  | :eq(index) | 从获取到的元素中过滤出指定下标的             | $('li:eq(5)') |
  | :checked   | 被选中的                                     |               |
  | :selected  |                                              |               |

+ 筛选选择器

  + `.children()`
    + 定义：获取子代元素，通过传参选出指定的元素
    + 示例：`$(this).children('ul').show()/.hide()`
    + 说明：事件中的 this 是 dom 对象，JQ 使用时要转为 JQ 对象
  + `.siblings()`
    + 定义：获取当前元素的所有兄弟元素(不包含自己)
    + 参数：可传可不传，根据参数筛选指定的兄弟元素
  + `.parent()`
    + 定义：当前元素的父元素
  + `.parents()`
    + 定义：当前元素的父辈元素
  + `.eq()`
    + 定义：通过参数指定获取到指定下标的元素
    + 注意：与 `eq()` 过滤选择器的区别
  + `.get()`
    + 定义：通过 `.get()` 获取到 dom 对象
    + 与 `.eq` 的区别：通过 `eq()` 方法获取到的元素是 jq 对象
  + `.next()`
    + 定义：下一个兄弟元素
  + `.prev()`
    + 定义：找上一个兄弟元素
  + `.find()`
    + 定义：当前元素的后代元素
  + `prevAll()`
    + 定义：当前元素前面所有的兄弟元素
  + `nextAll()`
    + 定义：当前元素的后面所有的兄弟元素
  + `.filter()`
    + 定义：过滤 jq 对象



# 六、jQuery 操作样式

+ css 操作

  + 语法：`.css(name, value)`
  + 解释：
    + name：属性名，可用 - 和 驼峰命名法(推荐)
    + value：引号：'30px' 、数值：30
  + 多样式：`.css({键：值, color: 'red', fontSize: 40})`
  + 获取样式：`.css(name)`：如果元素多个，会获取第一个元素的样式值
  + 区别：设置时可同时设置，但获取只获取第一个的样式

+ class 操作

  + js 操作：`元素.className = ''`

  + jQ 操作：

    ```js
    // 添加类名,在原有html的基础类名上添移
    $.addClass()
    // 移除类名,在原有html的基础类名上添移
    $.removeClass()
    // 判断是否有()类名,返回true/false 判断标准：只要有一个元素有()类名返回true,所有元素都没有才返回false
    $.hasClass()
    // 判断是否有该类名,如果移除,如无添加(切换)
    $.toggleClass()
    ```



# 七、jQuery 操作属性

> `.arrt()`

jquery 封装了 H5 中操作自定义属性的方法，dataset 为 data，此时，获取标签自定义属性时去掉 'data-' 前缀

+ JS 操作属性

  ```js
  dom.setAttribute()
  dom.getAttribute()
  dom.removeAttribute()
  ```

+ jQ 操作属性：`.attr()`

  ```js
  // 设置单个属性
  jq.attr(name, value)
  // 设置多个属性
  jq.attr({
      title: '',
      alt: '',
      src: ''
  })
  // 获取属性：获取的是第一个
  jq.attr(name)
  // 移除属性：对所有元素生效
  jq.removeAttr(name)
  ```

> `.prop()`

<font color=red> 设置值为布尔类型的数据 </font>

因 `.attr()` 只获取标签静态属性，没有获取实时的

+ 定义：实时获取属性值，像表单元素的 checked、disabled、selected  这三个属性，不能使用 `.attr()`，此时使用 `.prop()` 方法获取和设置
+ 返回值：`.prop()` 方法返回的是布尔值
+ 区别
  + `.prop()` 一般用于操作标签固有属性(例：src/alt/...)
  + `.attr()` 一般用于操作自定义属性，除以上三个，其它皆可使用 `.attr()`

​	

# 八、jQuery 动画

配合 display 使用

> show/hide 系列

+ `.show(speed, easing, callback)` 展示

  + speed：动画时长，单位 ms，主要修改 width/height/opacity

    slow：600ms

    normal：400ms

    fast：200ms

  + easing：动画效果

    swing(秋千)：先慢 ---> 快 ---> 慢

    linear(匀速)

  + callback：回调函数，当动画执行结束后执行

  + 无参：相当于 `display:block` 没有动画效果

  + 说明：以上参数都是可选的

+ `.hide(speed, easing, callbck)` 隐藏

+ `.toggle(speed, easing, callbcak)` 切换

> slide 系列(意为滑动)

<font color=red> 主要修改元素高度 </font>

+ `.slideDown(speed, easing, callback)` 展示
  + speed/easing 参数同上
  + 午餐：默认 normal = 400ms
+ `.slideUp(speed, easing, callback)` 隐藏
+ `.slideToggle(speed, easing, callback)` 切换

> fade 系列(意为逐渐消失)

<font color=red> 主要修改 opacity </font>

+ `.fadeIn(speed, easing, callback)` 注入
+ `.fadeOut(speed, easing, callback)` 淡出
+ `.fadeToggle(speed, easing, callback)` 切换



# 九、自定义动画(只支持数值型属性)

+ 语法：`.animate(obj, speed, easing, callback)`
+ 参数：
  + obj：必选，键值对的对象，样式&样式值
  + 其它参数可选，同上
  + 默认：normal：400ms



# 十、动画队列与停止动画

+ 动画队列：解决先后顺序

  像链式编程，多个动画时，直接在元素后面继续.添加

  ```js
  // 顺序执行,会将多个动画添加到元素动画队列中,然后依次执行
  $('div')
      .animate({left: 600}, 1000)
      .animate({top: 300}, 1000)
      .slideUp(1000)
      .slideDown(1000)
  ```

+ 停止动画

  解决快速移进移出时，多个动画在动画队列中出现的问题

  `.stop()` 停止动画：停止<font color=red> 当前 </font>正在执行的动画，如果当前队列还有动画，执行后续动画

  `.stop(clearQueue, jumpToEnd)`

  clearQueue：清除动画队列，参数 true 才清除，默认 false

  jumpToEnd：是否跳转到当前动画的最终效果，true ---> 跳转到最终效果 false ---> 不跳转



# 十一、jQuery 节点操作

+ 创建元素(节点)

  `$('标签')`

  `var $a = $("<a></a>")`

  注意：标签引号的问题

+ 添加元素(节点)

  + 原生js

    +  `dom.appendChild()` 有剪切效果
    + `` dom.insertBefore()`

  + jq

    子元素中往后添加

    + `元素.append()` 在元素的子元素中往后添加(有剪切效果)

      `.append(页面已有元素)`：有剪切的效果

      `.append('html字符串')`：根据 HTML 字符串先创建元素，之后添加

    + `B.appendTo(A)`

      将 B 往 A 里添加，A 可以是选择器，作用同上

      `$('outerp').appendTo($('div'))`

      `$('outerp').appendTo('html字符串')`

    子元素中往前添加

    + `A.prepend(B)` 将 B 作为第一个子元素添加到 A 中
    + `B.prepend(A)` 

    兄弟之间

    + `A.before(B)` 将 B 添加到 A 的前面作为兄弟元素
    + `A.after(B)` 将 B 添加到 A 的后面作为兄弟元素

+ 清空节点

  + 删除节点

    `A.remove()` 删除，移除 ---> 自杀

  + 清空节点

    `A.empty()` 清空所有的子节点

  + 克隆节点

    `A.clone()` 

    参数：true：克隆元素事件 false：默认



# 十二、jQuery 特殊属性操作

+ val 方法

  + 作用：设置、获取表单元素的 value 属性值(专门)

    `$('input').val()` 无参：获取表单元素 value 属性的值

    `$('input').val('27期')` 传参：设置 value 值

+ html 方法

  + 作用：修改文本内容
  + 原生js：`innerHTML` 可识别标签
  + jq：`html()` 设置：传参 获取：无参

+ test 方法

  + 作用：修改文本内容
  + 原生js：`innerText` 识别不了标签，当成文本
  + jq：`test()` 设置：传参 获取：无参

+ width 和 height(通过 `A.css` 获取的带单位)

  + 获取时只能获取到内容的(不包含padding、border)

    无参：获取，传参：设置。获取(设置)的是数值类型

    `A.width()` `A.height()`

  + 内容+padding

    `A.innerWidth`

    `A.innerHeight`

    一般不用于设置

  + 内容+padding+border

    `A.outerWidth()`

    `A.outerHeight()`

    如果传入参数true，那么获取到的是 内容+padding+border+margin

  + 可视区域的宽高

    `$(window).width()`

    `$(window).height()`

+ 卷曲距离

  + `.scrollTop()` 设置和获取垂直方向的卷曲距离
  + `.scrollLeft()` 设置和获取水平方向的卷曲距离
    + 不传参：获取
    + 传参：设置 ---> `$(window).scrollTop(0)` ---> 返回顶部

+ `.offset()` 和 `position()`

  + js

    `.offsetLeft` `.offsetTop`

  + jQ

    `offset()` 获取元素距离页面的距离，和父元素无关。返回值：返回一个包含 top/left 的对象

    `position()` 获取元素与有定位的父元素之间的距离。返回值：返回一个包含 top/left 的对象



# 十三、jQuery 的事件机制

> `$().click()`

解绑不了，多个不会覆盖，同时生效

> `.bind()` `.unbind()`

`.bind()` 可同时注册多个事件

`.unbind()` 会解绑全部事件，如果要解绑单一事件，传参。缺陷：不支持动态绑定

> `delegate()` 意为委托

注册委托事件，为父元素注册事件，由子元素去触发

+ js

  ```js
  dom.addEventListener('click', function (e) {
      if (e.target.nodeName === 'LI') {
          // 原理：事件冒泡
      }
  })
  ```

+ jq

  + 语法：`delegate(selector, type, fn)`
  + selector：子元素(选择器)，指定的子元素去触发
  + type：事件类型
  + fn：事件处理函数

  ```js
  父元素.delegate('p', 'click', function() {
      
  })
  ```

  + 解绑：`undelegate()`

    `父元素.undelegate()`  解绑元素的所有委托事件

    `父元素.undelegate('p', click)` 解绑指定的子元素去触发的事件

    缺陷：父元素无法触发，只能由子元素去触发

> on 注册事件(统一之后)

+ 语法：`.on(type, selector, data, fn)`

+ 参数

  + type：事件类型
  + selector(可选)：选择器(如果有参数，表示注册事件委托，指定子元素来触发该事件，如无该参数，表示注册普通事件)
  + data(可选)：携带的数据：将该数据传递给事件处理函数内部，通过事件对象 `e.data` 来获取
  + fn：事件处理函数

+ 自身注册：不支持动态绑定，可注册多个事件

  `父元素.on('click', function() {})`

+ 注册事件委托：可注册多个事件，<font color=red> 一定要页面上存在的 </font>

  `父元素.on('click', 'p', function() {})`

+ 解绑：

  使用 on 注册的事件，使用 off 解绑

  + `元素.off()` 解绑元素的所有事件
  + `元素.off(type)` 解绑指定的事件
  + `元素.off(type, selector)` 解绑事件委托

+ 触发事件

  + `.click()`
  + `.trigger(type)`

> jQuery 事件对象

对 js 事件对象的封装，处理了兼容性问题

+ `e.screenX`

  光标相对于电脑屏幕左上角的水平位置

+ `e.screenY`

  光标相对于电脑屏幕左上角的垂直位置

+ `e.clientX`

  光标相对于可视区域左上角的水平位置

+ `e.clientY`

  光标相对于可视区域左上角的垂直位置

+ `e.pageX`

  光标相对于页面(网页)文档 document 的水平位置

+ `e.pageY`

  光标相对于页面(网页)文档 document 的垂直位置

+ `e.code`

  按键的键盘码

+ `e.data`

  事件传入的 data 数据

+ `e.stopPropagation()` 

  阻止事件冒泡

+ `e.preventDefault()`

  阻止浏览器默认行为

+ `return false`

  在 jq 中既可阻止事件冒泡还可以阻止浏览器的默认行为



# 十四、 jQuery 补充

jQ 的两大特点：1. 链式编程 2.隐式迭代

+ 隐式迭代(偷偷的遍历)

  + 在进行设置的时候，会进行隐式遍历
  + 获取性操作时，只返回第一个元素的对应样式
  + 解决手动遍历设置不同的样式
  + 语法：`.each(function(index, ele) {})`
  + 参数
    + each：是一个函数，每一个遍历的元素都执行
    + index：当前遍历的元素在所在兄弟元素的下标
    + ele：当前遍历的这个元素

  ```js
  $('li').each(function (index, ele) {
      // ele 为dom对象，注意转换，此函数内部，this即为ele
      $(ele).css({})
  })
  ```

+ 链式编程

  + 定义：可以一直使用点一直调用下去

  + 限制：对于设置性操作返回 jq 对象，可以连续链式编程。对于获取性操作，返回的是具体的值，不可继续链式编程

    `.prevObject`：返回上次的 jq 对象(属性)

    `.end()`：此方法封装了 `.prevObject` 属性

  + 原理：设执行操作内部返回 this(jq对象)



# 十五、多库共存

`jQuery.noConflict()` 

+ 释放 jQuery 对 $ 的控制权
+ 返回：jQuery 函数的功能($)，相当于 $ 符，可用变量接收



# 十六、jQuery 插件

+ 定义：本质还是 js 文件，在 jq 的基础上新增实现了一些功能
+ 使用：
  1. 引入 jQuery 文件
  2. 引入插件(引入插件依赖库)
  3. 使用配置插件
+ 常用插件
  + `jQuery.color.js`：animate 扩展
  + `jQuery.lazyload.js`：图片懒加载
  + `jQuery,ui`



# 十七、自制 jQuery 插件

+ jQuery 插件原理：jq 插件把功能添加到 jq 的原型上
+ jq 原型：
  + `jQuery.prototype`
  + `jQuery.fn`
  + `$.prototype`
  + `$.fn`



# 十八、jq 的基本架构

源码查看推荐：1.7.0

+ jq 的架构：沙箱(把函数声明解释成函数表达式，即可用()直接调用)

  ```js
  (function(window, undefined) {
  	// 外层()的作用：将函数声明转为函数表达式(函数表达式可以跟括号进行调用，函数声明不可以跟括号直接调用)
      window.jQuery = window.$ = jQuery
  })(window)
  ```

  + window

    全局对象，作用

    + 有利于代码压缩
    + 减少对 window 的搜索过程

  + undefined 的作用

    + 防止 IE678 低版本中能修改 undefined 这个数据类型的值

+ 小知识点

  + 获取版本号：`$.jQuery`
  + 数据和对象方法使用变量接收，提升到前面，目的减少搜索过程，利于代码压缩



