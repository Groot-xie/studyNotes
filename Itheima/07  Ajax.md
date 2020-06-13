# 一、介绍

+ 本质：在 HTTP 协议的基础上通过 js 的 `XMLHttpRequest` 对象与 服务器通信
+ 作用：可以在页面不刷新的情况下请求服务器，局部更新页面数据
+ AJAX：asynchronous JavaScript and xml





# 二、XMLHttpRequest

具备与服务器通信的能力，浏览器的內建对象，实现网页的局部刷新

> 发送 GET 请求

+ 创建 `XMLHttpRequest` 对象

  ```js
  var xhr = new XMLHttpRequest()
  ```

+ 设置请求行(设置请求报文第一步)

  ```js
  // 参数1：请求方式 get/post 
  // 参数2：请求的地址，需要在url后面拼接参数列表
  // 参数3：是否异步 true(异步) false(同步)
  xhr.open('get', '08.hph?name=xiexiaohua')
  ```

+ 设置请求头(get 方法无需设置)(设置请求报文第二步)

  ```js
  xhr.setRequestHeader('content-type', 'text/html')
  ```

+ 设置请求主体(设置请求报文第三步)

  ```js
  // get请求的请求主体为空对象，因为参数列表拼到url后面了
  xhr.send(null)
  ```

+ 获取响应

  ```js
  // HTTP 响应分为三个部分：状态行、响应头、相应主体
  // 给xhr注册onreadystatechange事件
  xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 200) {
          var result = xhr.responseText;
          // 参数：响应头中的某一个信息
          xhr.getResponseHeader()
          // 获取响应头的全部信息
          xhr.getAllResponseHeaders()
      }
  }
  ```

  + `readyState` 记录 `XMLHttpRequest` 对象的当前状态 
    + 0：请求初始化(还未调用 `open()`)
    + 1：请求已经建立，但还未发送(还未调用 `send()`)
    + 2：请求已发送，正在处理中
    + 3：请求在处理，但服务器还没有完成响应的生成
    + 4：响应已完成，可获取并使用服务器的响应了
  + `status` 服务器成功处理响应
  + `responseText` 获取服务器返回的数据

> 发送 POST 请求

```js
// 1.创建XMLHttpRequest对象
var xhr = new XMLHttpRequest()
// 2.设置请求行 参1：请求的方式 参2：请求的地址 参3：是否异步 true(异步) false(同步)
xhr.open('post', '09.php')
// 3.设置请求头(post方式必须设置content-type,不然后端无法取得数据)
xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded')
// 4.设置请求主体
xhr.send('name=xiexiaohua&age=18')
```





# 三、JSON 文件格式

JavaScript object notation

一种轻量级的文本数据交换格式，独立于语言的文件格式，体积小，解析方便高效

+ 语法规则

  + 数据在名称/值对中(数据用键值对表示)
  + 数据由逗号分隔(最后一个键值对不能带逗号)
  + 花括号存储对象，方括号存储数组
  + 使用双引号

+ JSON 解析

  <font color=red> JSON 类型为字符串 </font>，不同的语言有不同的解析方法

  + JavaScript 解析方法

    ```js
    // json字符串 --> js对象
    JSON.parse()
    // js对象 --> json字符串
    // 参3：优化缩进
    JSON.stringify({}, null, 2)
    ```

  + php 解析方法

    ```php
    json_encode();
    json_decode();
    ```





# 四、前后端分离思想

使用 ajax 进行前后端交互思路

+ 前端向后台发送请求
+ 后台返回数据
+ 前端渲染展示数据





# 五、Ajax 同异步

通过 `open()` 传参控制，默认为 true 异步

+ 同步：同一时刻只能做一件事
+ 异步：同一时刻可以做都件事





# 六、命名空间

+ 解决全局污染
+ 一个用于命名的区域，在命名空间定义变量和函数可以解决全局污染的问题





# 七、jQuery 中的请求数据

## 7.1 API

+ `$.ajax(obj)`

  ```js
  // 1. 在jQuery中药中止请求用return false
  // 2. .delay() 参数：数值(毫秒),暂停1秒
  $.ajax({
      // 接口地址
      url: '',
      // 请求方式(get/post)
      type: 'get',
      // 超时时间(数值毫秒),请求超过设定时间,浏览器停止请求,失败error
      timeout: 5000,
      // 后台返回数据以什么格式处理(json/xml/text(默认)),如果设置成json,会自动转换成对象(调用JSON.parse)
      dataType: 'text',
      // 请求携带的数据
      data: {
          name: 'xiexiaohua'
      },
      // 调用前的回调函数
      beforeSend: function () {},
      // 成功的回调函数
      success: function () {},
      // 失败的回调
      error: function () {},
      // 完成后的回调
      complete: function () {}
  })
  ```

+ 其它API

  ```js
  // 只发送post请求
  $.post(url, callback, [data])
  // 只发送get请求
  $.get(url, callback, [data])
  // 将返回结果自动调用JSON.parse()方法
  $.getJSON(url, callback)
  // 请求服务器的js文件,返回后可使用.js读取json文件可用FileReader对象配合input:file使用
  $.getScript(url, callback)
  // 载入一个服务器端的html页面,url这个页面的内容加载到div这个dom对象中
  $('div').load(url)
  ```



## 7.2 表单序列化

```js
$('form').serialize()
```

只能获取表单的键值拼接 ---> FormData

定义：表单序列化将表单的 name 属性和 value 属性进行拼接，jQuery 的 ajax 方法的 data 参数可以直接识别表单序列化的数据(可直接传拼接的字符串 `"name=zs&age=18"` )





# 八、模板引擎

+ 介绍

  + 是一个 js 插件，js文件
  + 作用：渲染数据到页面中
  + 缘由：由于拼接字符串方法渲染数据存在很多的弊端，易出错，后期维护麻烦
  + 地址：https://aui.github.io/art-template/zh-cn/index.html

+ `ArtTemplate`

  + 引入模板引擎 `template-web.js`

  + 准备数据

  + 准备模板

    ```html
    <!-- 指定type为text/template后,这个标签不会解析也不会显示 -->
    <!-- data = {
        title: '传智',
        nav: [1, 2, 3, 4]
    } -->
    <script type="text/template" id="temp">
    	<h1>{{ title }}</h1>
    	<ul>
           {{ each nav v i }}
               <li>{{ v }}</li>
           {{ /each }}
        </ul>
    </script>
    ```

  + 模板语法：js代码用 `{{ }}` 包裹

  + 模板与数据绑定：`template('id', data)`

  + 注意点：

    + 传递给模板的数据必须为对象，如果不是要包装成对象
    + 在模板中直接使用对象的属性名





# 九、瀑布流布局

+ 每张图片在布局前，先找当前最小的列，向高度最小的列之后进行追加
+ 追加时
  + left：最小列的 left：`当前列索引值 * (width + 间距)`
  + top：最小列的列高 + 间距
+ 要理解更新当前列列高，用新列高参与下一列比较





# 十、接口化开发

后台给前端提供一个接口文档，前端只要基于接口文档就可以独立于后台进行开发，提高工作效率





# 十一、同源与跨域

## 11.1 同源

+ 同源：协议相同、域名相同、端口相同(来自同一个服务器的资源)
+ 目的：保护用户信息安全，防止恶意网站窃取数据
+ 限制范围(非同源、跨域)
  + cookie localstorage 无法读取
  + DOM 无法获得
  + ajax 请求不能发送



## 11.2 跨域

+ jsonp(json with padding)

  + 目的：解决主流浏览器跨域数据访问问题
  + 原理：服务器返回一个预先定义好的 js 函数调用，并且将服务器的数据以该函数参数的形式传递过来

+ jQuery 对于 jsonp 的封装

  跟普通的 get 请求区别在于将 dataType 固定成 jsonp 即可

+ js 解决

  ajax 里的 dataType 设置成 jsonp

+ 跨域解决原理

  + 在跨域的情况下，受浏览器限制，不能进行 ajax 请求。不能使用 `XMLHttpRequest` 请求服务器。就算设置 `dataType: "jsonp"` 也不行
  + 当将 `$.ajax` 的 `dataType` 设置为 `jsonp` 时，`$.ajax` 内部用其它方式请求服务器，可以利用 script 标签的 src 属性请求服务器
  + 实现：
    + 前端定义一个方法
    + <font color=red> 使用 script 的 src 属性 </font>将方法名传递给后台
    + 后端获取前端传递的方法名，在方法名后拼括号(调用)，在括号中填充数据
    + 后台拼接好带有参数的方法调用后，返回给浏览器，浏览器接收后，会立即当做 js 代码执行，即可获取到后台返回的数据
  + jsonp 注意
    + jsonp 只能发送 get 请求
    + jsonp 需要后台配合才能实现



## 11.3 CORS

服务器端跨域，跨域资源共享

+ 前提：

  + 浏览器支持

  + 服务器允许这种跨域

    ```php
    // 全开放可访问
    header('Access-Control-Allow-Origin:*');
    // 指定可访问
    header('Access-Control-Allow-Origin:http://www.baidu.com');
    ```

+ 结论：**<font color=red> 跨域行为是浏览器行为，是浏览器组织了 ajax 请求 </font>**





# 十二、XMLHttpRequest 2.0

## 12.1 介绍

+ 1.0 缺点

  + 传递数据中没有进度信息
  + 不能设置超时
  + 无法传递二进制文件，如图片视频
  + 受到 同源策略 的影响

+ 2.0

  + 可以设置超时时间
  + 可以使用 FormData 对象管理表单数据
  + 可以获取数据传递的进度信息

+ 设置超时(发送请求之前)

  ```js
  // 设置超时时间
  xhr.timeout = 2000
  // 超时后执行的函数
  xhr.ontimeout = function () {}
  ```



## 12.2 FormData 管理表单数据(send前)

新增 `FormData` 对象用于管理表单数据

```js
var myForm = document.querySelector('#myForm')
// 创建FormData实例
var formData = new FormData(myForm)
// 监听上传文件进度(send发送前)
xhr.upload.onprogress = function(e) {
    // value:0.000~1
    var value = e.loaded / e.total
    }
// 发送
xhr.send(formData)
```

+ `FormData` 对象注意点

  + 必须使用 <font color=red>POST</font> 方式传递数据

  + FormData <font color=red> 不需要设置请求头 </font>(浏览器会自动设置合适的请求头)

  + FormData 实例可以直接作为 `xhr.send()` 的参数，此时传输的是二进制形式

  + FormData 有 append 方法，可以添加参数

    ```js
    formData.append('id', 18)
    ```

+ 如何用 FormData 配合 Ajax 请求(jQuery)

  ```js
  $.ajax({
      url: '',
      // FormData 必须使用post请求
      type: 'post',
      data: new FormData(myForm),
      success: function () {},
      // 告诉$.ajax无需处理数据
      processData: false,
      // FormData不能设置请求头
      contentType: false
  })
  ```

  

# 十三、其它

+ 直接输入网址或点击 a 标签的请求方式为 get 方式

+ 标签增添自定义属性一般用 `xx-xx`

+ input 事件

  + h5 新增事件，`oninput` 事件，当用户输入时触发

    jq 不支持 `.input` 形式绑定事件，使用 `on('input')` 绑定

  + onchange：值发生改变时，输入完成市区焦点后才触发，不实时，有延迟

+ 时间标签(时间格式化插件)

  input：datatime-local

  value格式：2018-09-18T01:57

  给标签设置当前的时间

  ```js
  var date = new Date()
  ```

  插件转换格式( `moment.js` )，时间格式化插件

  `moment(时间).format(格式)` 不传时间默认为当前时间

+ 分页插件

  `pagination.js`

+ 图片本地预览

  + 限制文件上传的类型

    + 语法：`accept="大类型/小类型"`
    + `input/file` 增添 `accept` 属性
    + `accept="image/gif,image/jpg"`
    + `accept="image/*"` 只上传图片类型，不限制格式

  + 本地预览

    ```js
    document.querySelector('input').onchange = function () {
        // 获取被选中的图片(上传的文件存在this.files中)
        var file = this.files[0]
        // 通过文件获取文件的url,创建文件的url地址
        var url = URL.createObjectURL(file)
    }
    ```

+ 富文本编辑器 `wangEditor.js`

+ 模态框(遮挡层)

+ 表单元素重置(js 提供的 dom 方法)

  ```js
  // 相当于reset表单(input:reset)
  $('form').get(0).reset()
  ```





# 十四、前端模块化(require.js)

## 14.1 基本介绍

+ 传统加载 js 文件的缺点

  + 同步加载，加载时浏览器停止渲染。如加载文件多，网页失去响应时间久
  + 由于 js 文件存在依赖关系，因此要严格保证加载顺序。依赖关系复杂后，代码的编写和维护困难

+ 解决：`require.js`

  + 实现 js 文件异步加载，避免网页失去响应
  + 管理模块之间的依赖性，便于代码的编写和维护

+ 模块化标准

  + AMD：`Async Module Definition` 异步模块定义 `require.js`

    依赖前置：在一开始就将所有的依赖项全部加载

  + CMD：`Common Module Defintion` 通用模块定义 `sea.js`

    依赖延迟：在需要的时候才去加载依赖项



## 14.2 定义模块

```js
define(模块名称, ['模块依赖项'], function() {
    // 模块中所有的代码全部放在这个函数中
})
```

+ 每一个模块都有自己单独的作用域
+ 定义模块时，需要用 `require.js` 提供的函数 `define()` 定义
+ 参数说明
  + 模块名：模块名称，一版不建议起模块名，建议匿名模块
  + 依赖项：当前模块所依赖的其它模块，依赖项为相对路径，相对的是 html 文件



## 14.3 引用模块

在 `require.js` 中，引用一个模块使用 `require.js` 提供的函数 `require()`

```js
require(['模块文件的路径'], function () {
    // 模块加载成功之后的回调函数
    // 模块的加载是异步的，加载完成后才能使用模块的相关功能
})
// 引入模块时，`.js` 后缀名可以省略
require(['./js/a'], function() {
    console.log()
})
```



## 14.4 模块注意项

+ 模块有导出项，直接用 `return` 语句进行导出，引用模块时用回调函数接收
+ 引入多个模块时，形参顺序和模块加载顺序一一对应
+ 一般将没有返回值的模块放在后面，避免要为没有返回值的模块写形参



## 14.5 模块化路径的查找方式

+ 不做任何配置，直接以当前文件的路径作为参照

+ 如果设置 `data-main` 属性，那么模块的查找会以 `data-main` 指定的路径作为基础(几乎不用)(在引入 require 的 script 标签设置) 

  ```js
  <script src="require.js" data-main="./js/vendor/"></script>
  ```

+ 配置路径：如果通过 `require.config` 方法配置了基础路径，那么所有的模块查找都会以这个基础路径作为参照

  规则：`baseUrl + paths`

  ```js
  require.config({
      // 基础路径(公用路径)
      baseUrl: '',
      // 给路径起别名
      paths: {
          code: 'font/five/...js'
      }
  })
  ```



## 14.6 第三方插件使用

define 定义模块 ---> 用 require 引入

支持模块化与不支持模块话插件的区别：不支持模块化：不知道自己依赖项

解决方式：手动给不支持模块化的插件绑定依赖项

```js
require.config({
    baseUrl: '',
    // 此时引入文件不能加.js，否则报错
    paths: {
        jquery: '',
        moment: '',
        pagination: '', // 不支持模块化
    },
    // 手动绑定依赖项
    shim: {
        pagination: {
            deps: ['jquery'],
            // 如果有输出
            exports: '输出项'
        }
    }
})
```

