## mock在vue-cli中的基本使用

### 第一步

安装依赖(应该是开发时依赖就好了)

```npm
npm i mockjs -D
```

### 第二步

在项目结构中的src中创建mock文件夹存放假数据

![1548214512327](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1548214512327.png)

### 第三步

在main.js中引入mock/index.js

```js
// index.js可省略
import './mock/index.js'
```

### 第四步

在mock/index.js中造假数据

```js
// mock/index.js文件
import Mock from 'mockjs'
const Random = Mock.Random
// 参1： 接口地址
// 参2: 请求方式
// 参3: 假数据
Mock.mock('mock/home', 'get', {
  title: Random.ctitle(1, 5)
})
```

### 第五步

在.vue文件中使用

```js
created () {
    // 请求方式和请求路径对应造的数据
    this.$axios.get('mock/home').then(data => {
        console.log(data)
    })
}
```

## mock 文档

http://mockjs.com/