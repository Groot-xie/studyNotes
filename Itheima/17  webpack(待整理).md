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
+ webpack 模块能够识别一下等形式的模块之间的依赖
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

  4. 注意：在使用 webpack 命令时，应指定 node 配置。mode 的值可以是 development 或 production。如果没有指定默认是：production

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

