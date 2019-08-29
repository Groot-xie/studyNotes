## SVG

### 定义

+ 可伸缩矢量图形( Scalable Vector Graphics )
+ SVG 使用XML格式定义图形

### 优势

+ SVG图像中的文本是可选的， 同时也是可搜索的(适合制作地图)
+ SVG 与 JPEG / GIF 图像比起来， 尺寸更小， 且可压缩性更强
+ 可伸缩，不失真

### viewport 视口

+ 定义：SVG可见区域的大小，画布大小

```html
<!-- 默认单位px -->
<svg width="800" height="600"></svg>
```

### viewBox 视区盒子

+ 定义：视口中视图区域

+ 语法：viewBox=“x, y, w, h”

```html
<svg width="800" height="600" viewBox="0 0 80 60"></svg>
```

+ 注意：
  1. viewBox与viewport宽高比为一定比例时会撑满 viewport
  2. preserveAspectRatio属性：让viewBox保持宽高比
+ demo  1.html

#### preserveAspectRatio

+ 语法： preserveAspectRatio=[defer]<align><metOrSlice>

  + defer：可选，仅在image元素上应用

  + align：必选，控制viewBox是否强制进行均匀缩放

    + 取值： 

      1. xMin  viewBox的最小X值对齐viewport的左边部

      2. xMid  viewBox的X轴中点对齐viewport的X轴中点

      3. xMax viewBox的最大X值对齐viewport的右边部

      4. YMin  viewBox的最小Y值对齐viewport的顶边

      5. YMid  viewBox的Y轴中点对齐viewport的Y轴中点

      6. Y Max viewBox的最大Y值对齐viewport的底边

         ![1567058708677](https://gitee.com/xiexiaohua/my_notes/blob/master/images/1567058708677.png)

         https://gitee.com/xiexiaohua/my_notes/blob/master/images/1567058708677.png

  + metOrSlice：控制viewBox缩放的方式

    + 取值：
      1. meet(默认)： 保持宽高比缩放，相当于background-size: container
      2. slice： 保持宽高比缩放并将超出部分裁剪，相当于background-size:  conver
      3. none：不保持宽高比，缩放图像适合整个viewBox，图像可能变形

  ```html
  <svg 
       width="800" 
       height="600" 
       viewBox="0 0 80 60"
       preserveAspectRatio="xMidYmid meet"
  ></svg>
  ```

+ demo  2.html