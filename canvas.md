### Canvas

```html
<canvas width="600" height="400" id="mycanvas"></canvas>
```

```js
var mycanvas = document.getElementById('mycanvas')
// 获取canvas的2D上下文
var ctx = mycanvas.getContext('2d')
```

#### 兼容性处理

+ 当浏览器不支持canvas时，中间的文字节点将被显示

  ```html
  <canvas id="mycanvas" width="1024" height="768">
      当前浏览器不支持canvas，请更换浏览器
  </canvas>
  ```

+ 利用js判断

  ```js
  if ( mycanvas.getContext('2d') ) {
      var ctx = canvas.getContext('2d')；
  } else {
      alert('当前浏览器不支持canvas')；
  }
  ```




#### API

+ 绘制矩形

  ```js
  ctx.rect(x, y, w, h)
  ```

+ 填充矩形

  ```js
  // fill: 填充 rectangle: 矩形
  ctx.fillRect(x, y, w, h)
  ```

+ 笔触(描边)

  ```js
  // 矩形笔触
  ctx.strokeStyle = 'red'
  ctx.strokeRect(x, y, w, h)
  ```

+ 画线

  ```js
  cxt.beginPath();	// 开始绘制路径
  ctx.moveTo(x, y);	// 移动到某个位置
  ctx.lineWidth = 5;	// 线的宽度
  ctx.lineJoin = 'miter'/'round'/'bevel';	//设置线条与线条连接点的样式
  ctx.lineCap = 'butt/round/square'; // 设置线条开始结束端的样式 
  ctx.lineTo(x, y);	
  ctx.lineTO(x,y);
  ...
  ctx.closePath();	// 封闭
  // -------------描边------------------
  ctx.strokeStyle = 'red';
  ctx.stroke();	// 画线(以上画线均为抽象)
  // -------------填充------------------
  ctx.fillStyle = 'blue';
  ctx.fill()；
  // 这里需要注意fill和stroke的顺序。 先stroke后fill可能边框会被盖住一部分
  ```

+ 弧和圆形

  ```js
  ctx.beginPath();
  // ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise)
  // x,y为圆心，以radius为半径 从starAngle到endAngle, anticlockwise顺逆时针
  // angle为弧度制
  ctx.arc( )
  
  ```

+ 贝塞尔曲线(一次)

  ```js
  ctx.beginPath()
  ctx.moveTo(x, y)
  ctx.quadraticCurveTo(cx, cy, x, y)
  ctx.stroke()
  ```

+ 贝塞尔曲线(二次)

  ```js
  ctx.beginPath()
  ctx.moveTo(x, y)
  ctx.bezierCurveTo(cx1, cy1, cx2, cy2, x, y)
  ctx.stroke()
  ```

+ 运动

   机制：上屏幕的元素，立即被像素化，也就是说上频的元素将得不到这个“对象”。所以只能   清屏 --> 重绘 --> 清屏 --> 重绘

  ```js
  ctx.clearRect(x,y,w,h); // 清除一个矩形区域
  ctx.textAlign = 'center'; // 文字居中
  ctx.fillText('文字', x, y)
  ```

+ 使用图片

  ```js
  var image = new Image();
  image.src = 'images/dogandcat.jpg';
  image.onload = function () {
     	//  五参： xy 坐标 wh 图片宽高
     	ctx.drawImage(image(图片对象), x, y, w, h)
  	//	九参： 前四个关于切片 后四个关于图片
      ctx.drawImage(image(图片对象), x, y, w, h, x1, y1, w1, h1)
  }
  ```

+ 图形变换

  ```js
  // 1.原点变换
  ctx.translate(x, y); 
  // translate 会叠加，所以要使用完后要复原
  ctx.translate(x, y);
  // dosometing...
  ctx.translate(-x, -y);
  
  // 另一种解决叠加的方案
  ctx.save();
  // todosometing...
  ctx.restore();
  
  // 2.旋转
  ctx.rotate(deg)
  
  // 3.缩放
  // 缩放会同时缩放其它数值属性
  ctx.scale(sx, sy)
  ```

+ 变换矩阵

  ![1566294593028](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1566294593028.png)

```js
ctx.transform(a, b, c, d, e, f);
ctx.setTransform(a, b, c, d, e, f); // 让之前的transform都失效，用此前设置的transform
```

