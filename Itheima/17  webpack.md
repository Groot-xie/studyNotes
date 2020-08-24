+ bundle：捆绑、收集、归拢
+ webpack 将带有依赖项的各个模块打包处理后，变成独立的浏览器能够识别的文件
+ webpack 合并以及解析带有依赖项的模块



## 一、概述

+ webpack 特点：模块化、打包

  1. webpack 是一个现代化 js 应用程序的模块打包器 module.bundler
  2. webpack 是一个模块化方案(预编译)
  3. webpack 获取具有依赖关系的模块，并生成表示这个模块的静态资源

+ 四个核心概念

  1. 入口( entry )
  2. 输出( output )
  3. 加载器( loader )
  4. 插件( plugins )

+ 打包(构建)

  1. 语法转换 less / sass / ES6 ---> ES5 / TypeScript ---> ES5
  2. 文件压缩 HTML / JS / CSS / 图片
  3. 文件合并 CSS / JS
  4. 提供开发期间的服务器环境，以 HTTP 协议的方式打开、监听文件内容变化，只要文件内容变化，自动刷新浏览器

+ 模块化

  为前端浏览器开发，提供了模块化环境。在 webpack 看来，所有资源都是模块



## 二、webpack 和 模块

+ 在 webpack 看来，所有的静态资源都是模块
+ webpack 模块能够识别以下等形式的模块之间的依赖
  1. js 的模块规范
     + ES2015 ---> import / export
     + CommonJS ---> require() / module.exports
     + AMD ---> define / require
  2. 非 js 等静态资源
     + css / sass / less 文件中的 @import
     + 图片链接。比如 css 中 url(...) 或 html 中 \<img src="" />
  3. 字体等



## 三、webpack 起源

解决了现存模块打包器的两大痛点

+ code spliting 代码分离
+ 静态资源的模块化处理方案



## 四、webpack 的基本使用

+ 基本使用

  1. 安装 `npm i webpack webpack-cli -D`

     `-D` 表示项目开发期间的依赖，只在项目开发期间使用。项目上线后 webpack 不会随着项目上线被放到服务器上去

     `webpack` 核心包

     `webpack-cli` 提供了再终端中使用 webpack 的命令

     `command line interface` 提供了一个叫 webpack 的命令，用来对项目进行打包

  2. webpack 的两种打包方式

     + 命令行
     + 配置文件方式(推荐) `webpack.config.js`

  3. 在 package.json 中的 script 脚本中添加配置

     `webpack 入口文件 --output 输出文件` 输出文件可通过配置 webpack 去掉

     ```json
     {
         "script": {
             "build": "webpack ./index.js"
         }
     }
     ```

  4. 在终端中运行命令 `npm run build`

+ 命令行使用说明

  1. 在 package.json 中的 script 中可以存放一些 bash 命令，这个 bash 命令通过 `npm run 命令名` 来执行

  2. 为什么通过 npm 就可以直接使用 webpack 命令

     原因：**<font color=red> npm 在执行脚本时，会在后台将当前目录 `/node_modules/.bin` 临时添加到环境变量中(临时环境变量) </font>**，添加后 .bin 目录中的 webpack 就可以使用了

     + 在 package.json 中的 script 添加 "build"："webpack ./index.js"
     + 然后再终端中就可以使用`npm run build`

  3. **<font color=red> wenpack 打包提供入口文件，进行递归分析 </font>**

+ 项目开发的两个环境

  1. 开发环境

  2. 生产环境(线上环境)：项目打包上线后的环境

  3. 区别：代码是否压缩

  4. 注意：在使用 webpack 命令时，应指定 mode 配置。mode 的值可以是 development 或 production。如果没有指定默认是：production

     配置：`webpack ./index.js --mode development`

+ 命令行完整语法

  `webpack 入口文件 --output 输出文件 --mode 环境`

  + `--output` 可简写 `-o`
  + `--output 输出文件` 不指定默认

+ webpack 使用方式之**<font color=red> 配置文件方式 </font>**

  + 步骤

    1. 在项目根目录中创建一个名为 `webpack.config.js` 的配置文件
    2. 修改 package.js 的 script 的命令为 `"build": "webpack"`
    3. 运行命令：`npm run build` 执行 webpack 命令，webpack 会自动找到 `webpack.config.js` 中配置项，对项目进行打包
    4. `npm run` 只做了将 `node_modules/.bin` 临时添加到环境变量中而已，真正打包的是 webpack 这个工具这个命令

  + 配置 `webpack.config.js`

    ```js
    module.exports = {
        modex: 'develoment', // 模式环境
        entry: path.join(__dirname, './index,js'), // 入口(绝对路径)
        output: { // 出口文件
            path: path.join(__dirname, './dist'), // 出口文件目录
            filename: 'main.js', // 出口文件名称
        }
    }
    ```



## 五、包工具

### webpack-dev-server

+ 安装 `npm i webpack-dev-server -D`
+ 作用：配合 webpack，创建开发环境、启动服务器、监视文件变化、自动编译、刷新浏览器等。提高开发效率
+ 注意：无法直接在终端中执行 `webpack-dev-server`， 需要在 package.json 配置 scripts 后使用 `"dev": "webpack-dev-server"`

> 使用说明

`webpack-dev-server` 将打包好的文件存储在内存中，提高编译和加载速度，效率更高

注意：输出的文件被放到项目根目录中

+ 命令行的提示：`webpack output is serverd from /`
+ 在 `index.html` 页面中直接通过 `/bundle.js` 来引入内存中的文件

> 配置说明 ---> cli 配置

+ `--contentBase` **<font color=red> 告诉服务器在哪个目录中给提供服务 </font>**(可以理解为打开哪个目录中的 index.html)
  + `--contentBase: ./` 当前工作目录
  + `--contentBase: ./src` 当前目录下的 src 文件夹
+ `--open` 自动打开浏览器
+ `--port` 端口号
+ `--hot` 热更新，只加载修改的文件(按需加载修改的内容)，而非全部加载

```json
{
    "scripts": {
        "dev": "webpack-dev-server --contentBase ./src --open --port 8888 --hot"
    }
}
```

> 配置说明 ---> webpack.config.js

```js
const webpack = require('webpack')

devServer: {
    contentBase: path.join(__dirname, './'),
    open: true,	// 自动打开浏览器
    port: 8888,	// 端口号
    hot: true,	// 热更新
},
plugins: [
    // 启动热更新插件
    new webpack.HotModuleReplacementPlugin()
]
```

> 说明

`webpack-dev-server` 命令作用

+ 在当前目录中开启一个服务器，默认地址：`localhost:8080`

+ 运行 webpack 命令，会在目录中生成一个 dist 文件夹

+ 运行 `webpack-dev-server` 命令是不会在目录中生成 dist 文件夹的，而是将打包后输入内容放在它开启的服务器的根目录中，也就是 `http://localhost:8080/bundle.js`

  **<font color=red> 实际上放在服务器自己的内存中 </font>**

+ 目的：性能考虑，如果每次输出到磁盘的目录中(文件写入操作)性能很慢，如果直接存储到内存中性能很快



### html-webpack-plugin

+ 安装：`npm i html-webpack-plugin -D`
+ 作用：根据模板
  1. **<font color=red> 自动生成 html 页面 </font>**
  2. **<font color=red> 自动引入(无需手动引入) </font>**
+ 优势：页面存储在内存中，自动引入 `bundle.js/ .css` 等文件
+ 说明
  1. 自动引入 css js 文件
  2. 能够在内存中根据指定的模板自动生成一个新的 html 页面，浏览器中打开的页面就是这个插件自动生成的页面

```js
// webpack.config.js
const htmlWebpackPlugin = require('html-webpack-plugin')

plugins: [
    new htmlWebpackPlugin({
        // 模板引擎路径
        template: path.join(__dirname, './index.html'),
        // 在内存中生成页面路径，默认值为：index.html
        // 输出文件名
        filename: 'index.html',
        // chunks 指定该页面引入哪个入口文件
        chunks: ['main']
    })
]

// 多文件打包
{
    entry: {
        main: ...,
        a: ...
    },
    output: {
        path: ...,
        // [name].js name 对应a。格式约定
        filename: [name].js
    }
}
```



### vue 相关

**<font color=red> Loaders(加载器) </font>**

+ <font color=red> webpack 看来所有的资源都是模块 </font>
+ webpack 只能处理 js 文件资源，其它模块 webpack 无法直接处理
+ webpack 通过 loaders 处理非 js 静态资源



#### css 打包

+ css 打包文件(加载)

+ sass 打包文件(编译为 css)

+ 使用 webpack 打包 css 文件

  `npm i style-loader css-loader -D`

  ```js
  // index.js 导入 css 文件
  import './css/app.css'
  // webpack.config.js 中配置各种资源文件的loader加载器
  module: {
      rules: [
          // test：用来配置匹配文件规则(正则)
          // use：一个数组，按照从后往前的顺序执行加载
          { test: /\.css$/, use: ['style-loader', 'css-loader'] }
      ]
  }
  ```

+ 解释

  + css-loader：读取 css 文件，将其转为一个模块
  + style-loader：读取模块内容，创建一个 style 标签插入到页面中



#### sass 文件打包

+ `npm i sass-loader node-sass -D`

+ 注意：`sass-loader` 依赖于 `node-sass` 模块

  ```js
  // webpack.config.js
  module: {
      rules: [
          { test: /\.(scss|sass)$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
      ]
  }
  ```

+ 解释

  + sass-loader：将 sass 编译为 css (compiles sass to css)
  + css-loader：将 css 转化为 commonJS 代码 (translates css into commonJS)
  + style-loader：创建 style 标签插入页面中 (creates style nodes from js strings)



#### less 文件打包

+ `npm i less-loader css-loader style-loader less -D` (less-loader 依赖于 less (less无需配置))

```js
// index.js
import './css/css.less'
// webpack.config.js
module: {
    rules: [
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }
    ]
}
```



#### 图片和字体打包

+ `npm i url-loader file-loader -D` 

  可以使用 url-loader 或 file-loader 中的任何一个，推荐使用 url-loader

+ `webpack.config.js`

  ```js
  // webpack.config.js
  module: {
      rules: [
         	// 打包图片
          { 
              test: /\.(jpg|jpeg|png|gif)$/, 
              use: [
                  // 控制是否解析为base64，不满足自动调用file-loader
                  { 
                      loader: 'url-loader', 
                      options: {
                          limit: 8192
                      } 
                  }
              ] 
          },
          // 打包字体
          {
              test: /\.(woff|woff2|eot|tff|otf)$/,
              use: 'file-loader'
          }
      ]
  }
  ```

+ 解释

  + file-loader：加载并重命名文件(图片字体等)

  + url-loader：将图片或字体转化为 base64 编码格式的字符串嵌入到样式文件中

    base64：只适用于很小的图片，base64一种特定的格式，浏览器会解析这种格式的字符串然后展示在页面中

+ 图片打包细节(1 ---> url-loader  2,3 ---> file-loader)

  1. limit 参数的作用(单位：字节)

     + 当图片文件大小**<font color=red> 小于 </font>**指定的 limit 时，图片被转为 base64 格式
     + 当图片文件大小**<font color=red> 大于等于 </font>**指定的 limit 时，图片被重命名以 url 路径形式加载(此时需要 file-loader 来加载图片，此时 url-loader 会调用 file-loader)

  2. 图片文件重命名，保证相同文件不会被加载多次。例如：a.jpg 拷贝一个副本 b.jpg，同时引入两张图。重命名后只加载一次，因为两张图实际为一张图

  3. 文件重命名后会通过 MD5 加密方式来计算这个文件的名称

     MD5 消息摘要算法(特征码提取) **<font color=red> MD5不可逆 </font>**

     + 使用 MD5 算法处理后，对于同一张图(名称不相同的情况)，得到特征码(32位)相同
     + MD5 可以对文件、图片、字符串等进行处理，处理后会得到一个唯一的 32 位的字符串，只要文件内容不变，那么这个 32 位的字符串不会发生改变，相当于这个文件的指纹
     + 场景：加密(比如登录时对密码加密，加密后再发送给服务器)



#### html-loader

+ `npm i html-loader -D`

+ `webpack.config.js`

  ```js
  // webpack.config.js
  module: {
      rules: [
          {
              test: /\.html$/,
              use: 'html-loader'
          }
      ]
  }
  ```



#### vue 单文件组件

`signle-file component`

- 后缀名 `.vue`，该文件需要被编译后才能在浏览器使用
- 单文件组件依赖两个包 `vue-loader` `vue-template-compiler`
- 安装 `npm i  vue-loader vue-tempplate-compiler -D`

> 单文件组件使用步骤

1. 安装

   ```npm
   npm i vue-loader vue-template-compiler -D
   ```

2. `webpack.config.js` 中配置 `.vue` 文件的 loader

   ```js
   { text: /\.vue$/, use: 'vue-loader' }
   ```

3. `webpack.config.js` 中添加 plugins

   ```js
   const VueLoaderPlugin = require('vue-loader/lib/plugin')
   new VueLoaderPlugin()
   ```

4. 创建 `App.vue` 单文件组件

5. 在 `main.js` 入口文件中，导入 vue 和 App.vue 组件。通过 render 将组件与实例挂在一起

> 有单文件组件后在入口文件 main 中的使用

```js
// main.js
import Vue from 'vue'
// 导入组件
import App from './App.vue'
//
const vm = new Vue({
    el: '#app',
    render: function(createElement) {
        return createElement(App)
    }
})
```

> 单文件组件

```vue
<template></template>
<script>
	// 组件中的逻辑代码
    export default {}
</script>
<style lang="less">
	// 样式，可指定lang，lang等于less时。表示可使用less编译
</style>
```

```js
// webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')
{ test: /\.vue$/, loader: 'vue-loader' }
plugins: [ new VueLoaderPlugin() ]
```



## 六、babel

+ babel 的作用

  1. 语法转换：将新的 ES 语法转化为浏览器能识别的语法( babel-preset-* )
  2. `transform-runtime` 或 `babel-ployfill` 浏览器兼容：让低版本浏览器兼容最新版 ES 的 API

+ 基本使用

  + babel 中的 presets 预设

    1. 作用：用来解析指定版本的 js 语法
    2. 比如：
       + ES2015(ES6) 用来解析 ES6 的语法
       + ES2016 用来解析 ES7 中的语法
       + ES2017 用来解析 ES8 中的语法
    3. 可以直接使用 env (包名：`babel-preset-env`) 这个 presets，作用相当于：ES2015 + ES2016 + ES2017，这样，使用一个包就可以解析所有的标准 js 语法了
    4. 除了标准的 js 语法之外，还有一些常用的 js 语法没有被采纳到 js 标准。因此，上面提到的 `babel-preset-env` 这个包，就无法解析这些不标准的语法了。因此，**<font color=red> 应使用 `babel-preset-stage-2` 包，它的作用就是用来解析非标准的 js 语法的 </font>**
    5. 最终：`babel-preset-env` 和 `babel-preset-stage-2` 这两个包就可以解析任意的 js 语法了

  + 基本使用

    1. `npm i babel-core babel-loader@7 babel-preset-env`

       `babel-core` ---> 核心包

       `babel-loader@7` ---> 加载器

       `babel-preset-env` ---> 解析标准语法

    2. 在项目根目录新建 `.babelrc` 配置文件

       ```js
       // 将来 babel-loader 运行时，会检查这个配置文件，并读取相关的语法和插件配置
       { "presets": ["env", "stage-2"] }
       ```

    3. 在 `webpack.config.js` 中添加 loader

       ```js
       // webpack.config.js
       module: {
           rules: [
               {
                   test: /\.js$/,
                   use: 'babel-loader',
                   // 排除不需要编译的目录，提高编译速度
                   exclude: '/node_modules/'
               }
           ]
       }
       ```

+ `babel-preset-`

  作用：将新的 ES 语法转化为浏览器能识别的语法

+ `transform-runtime`

  + 作用：实现浏览器对不支持 API 的兼容(兼容旧环境、填补)

  + 安装

    `npm i babel-plugin-transform-runtime -D`

    `npm i babel-runtime`

    注意：`babel-runtime` 包中的代码会被打包到你的代码中

  + 使用步骤

    在 `.babel` 中添加如下配置即可

    ```js
    "plugins": ["transform-runtime"]
    ```

+ 总结

  1. babel-core  ---->  babel 核心包
  2. babel-loader  ---->  用于解析 js 文件
  3. babel-preset-*  ---->  新的 ES 语法的解析和转换
  4. transform-runtime  ---->  兼容旧浏览器，到达支持新 API 目的

