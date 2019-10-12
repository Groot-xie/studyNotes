# LESS

## 一、变量

+ 语法：@变量名：变量值;

+ 规则：与 JS 命名规则相同 、不能以数字开头、由字母，数字，下划线组成



## 二、注释(两种)

+ //：  less 中的语法，不会编译到 css 文件中。一般用于 less 文件中的变量、函数加以注释(变量、函数也不会编译到 css 文件中)

+ /**/：css中的注释，会被编译到 css 文件中。一般用于进行模块的注释，提升 css 文件的可读性



## 三、less 混入类、mixin混入、混入类样式

+ 特点：将另一个类当成函数调用，将类中属性设置混入其中。

+ 缺点：不能传参，会被编译到css文件中

+ 例如

```less
// 定义
.base {
  background: red;
}
.one {
  font-size: 18px;
  // 调用
  .base();
}
```



## 四、less 中的函数(替代上面方案)

特点：

1. 不会被编译到 css 文件中

2. 可以传参，如果有参数，一般必须传参

3. 用于解决兼容性问题很方便

4. 可以设置默认值默认参数

   ```less
   // 定义
   // @value 参数(可有可无)
   // 50% 默认值(可有可无)
   .base (@value:50%) {
     border-radius: @value;
     -webkit-border-radius: @value;
     -moz-border-radius: @value;
   }
   // 调用
   .myBtn {
     .base(20px);
     color: red;
   }
   ```

   

## 五、less 嵌套

```html
<div class="one">
    <div class="two">
        <div class="there"></div>
    </div>
</div>
```

```less
// 后代
.one {
  color: red;
  .two {
    .there {}
  }
}
// 子代
.one {
  > .two {}
}
// 交集
.one {
  // &表上层
  &.two {}
  // 伪元素
  &::after{}
}
```

+ 后代
+ 子代   > .son
+ 交集   &.active
+ 伪元素   &::after



## 六、导入

ps：variable.less 一般用于存放变量集合

语法

```less
@import "文件路径.less";
// 省略文件名后缀
@import "文件路径";
```



## 七、函数(运算)

+ 可以进行加减乘除运算

  ```less
  .box {
      width: 100px / 2;
  }
  ```

+ less 内置了很多函数，可以直接使用

  与自定义函数使用有区别

  ```less
  // round(num, [保留小数,默认小数])
  .box {
      width: round(33.333);
      width: round(100px / 3);
  }
  ```







# REM 布局

font size of the root element

+ 定义：相对于<font color=ff0000> 根元素 </font>的字体大小的单位。相对单位

  另 em(font size of element)：相对于<font color=ff0000> 当前元素 </font>的字体大小的单位。相对单位。

  1. 流式布局(百分比布局)：可以让各种屏幕都适配，只有在大屏幕显示效果不是非常的友好。开发效率高，成本低。
  2. 响应式布局：工作量大，可维护性不好，节约成本
  3. rem布局：可以适配所有屏幕

+ REM 与 响应式

  不同屏幕的 HTML 的 font-size 大小。可以达到不同屏幕的适配

  1. 动态设置不同屏幕的 HTML 的 font-size 大小
  2. 使用 rem 单位
  3. 动态设置需配合媒体查询 @media

+ REM 与 媒体查询 @media

  1. 优点：使用媒体查询适配速度快
  2. 缺点：适配多个终端时，需要添加响应式代码。有兼容性。无法一次适配所有屏幕

+ REM 与 Javascript

  1. 定义：通过 js 获取可视区的宽度，计算fontSize的值
  2. 优点：直接适配所有终端
  3. 缺点：必须在页面加载之前设置 html 的 fontSize 值，不然会出现文字大小调用的情况
  4. 插件：手淘 rem 适配方案：flexible.js(引入在 title 下。头部内)

+ 基准值(自定义)

  1. 定义：设计图尺寸下屏幕的 HTML 根字体大小

  2. 公式
     $$
     fontSize = \frac{实际屏幕宽度}{设计图大小} \times 基准值
     $$

+ flexible.js

  1. flexible 要在 header 引入
  2. flexible 本质是在监听屏幕变化，动态设置根字体大小
  3. flexible 定义基准值：设计图尺寸 / 10

+ 补充

  vw vh 将屏幕分为100份(有限大的兼容性)