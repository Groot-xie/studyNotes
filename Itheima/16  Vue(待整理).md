[TOC]

# Vuex

## 一、概念

+ vuex是专门为vue提供的状态(<font color=ff0000> **状态即数据** </font>)管理工具
+ 状态管理工具采用了集中式管理数据的方式，统一管理项目中多个组件之间需要共享的数据
+ 场景：应用够简单，勿使用vuex。免得代码繁琐，冗余



## 二、基本使用

+ 安装

  ```js
  npm i vuex
  ```

+ 页面中先导入vue，再导入vuex

+ 使用



## 三、核心概念

+ store 仓库，仓储
  1. 一个vue项目中只能有一个store
  2. 提供两方面的内容：一. state(状态data)  二.操作stae的方法
  3. 注意：只能通过vuex中提供的方法来修改store中的数据，而不能直接修改state数据



## 四、基本使用

+ 基本使用

  ```js
  import Vue from 'vue'
  import Vuex from 'vuex'
  Vue.use(Vuex)
  /**
   * @param {Object} 配置对象
   */
  export default new Vuex.Store({
      // state 相当于组件中的data 获取：store.state.num
      state: {
          num: 0
      }
  })
  
  ```

+ 修改数据

  store 中提供修改 state 方法的配置对象，如要修改 store 中的数据，应该把方法放在mutations配置对象中

  ```js
  // 1.定义
  mutations: {
      addNum(state, payload) {
          state.num++
      }
  }
  
  // 2.使用
  // 参数1：方法名(字符串)；参数2：要传入的参数(建议传入对象)
  store.commit('addNum', payload)
  ```

  

## 五、配置vue使用

+ 创建vuex.store实例

  ```js
  const store = new Vuex.Store({
      state: {
          num: 0
      },
      mutations: {
        	// 1.定义方法  
          addNum(state, payload) {
              state.num += payload.count
          }
      }
  })
  ```

+ 关联

  ```js
  const vm = new Vue({
      store,
      methods: {
          fn () {
              // 2.触发 任何组件可通过 this.$store 取得数据
              this.$store.commit('addNum', { count: 8 })
          }
      }
  })
  ```

  创建文件夹位置：store/index.js中(同路由相同)



## 六、使用说明点

+ 任何组件都可以通过<font color=ff0000> **$store.state** </font>取得数据
+ <font color=ff0000> **不要在表单元素中直接使用 v-model 来操作 store 中的数据，数据由 vuex 的 store 提供，修改也套它来修改**</font>
+ 解决方案
  1. 单向绑定数据 :selected="todo.done"
  2. 绑定change事件来触发定义好的方法，在方法中通过 $store.commit() 触发 store 中的 mutations 中的方法
+ 通过时间对象 e 取得文本框的值 e.target.value



## 七、getter vuex中的计算属性

vuex允许在 store 中定义"getter"(类计算属性)，像计算属性一样，getter 返回值会根据它的依赖项被缓存起来，只当它的依赖项发生改变才会被重新计算

```js
// 1.定义
new Vuex.Store({
    getters: {
        // 根据state已有的数据得到一个新的数据
        leftCount(state) {
            return state.num + '元'
        }
    }
})

// 2.使用
this.$store.getters.leftCount
```



## 八、Action

与 mutations 相似

+ 特点
  1. 可包含任意的异步操作(mutations必须是同步函数)
  2. action 提交的是 mutations 而不是直接变更状态
+ 区别
  1. action 只负责封装异步操作，真正修改state的还是mutation
  2. DevTools 工具无法追踪记录 mutation 中的异步操作

```js
// 1.定义
actions = {
    // context 类似于store
    // addTodo mutation中的方法，实际在action中还是调用了 mutation 中的方法
    addTodoAsync (context, payload) {
        context.commit('addTodo', payload)
    }
}

// 2.组件中使用
this.$store.dispatch(addTodoAsync, payload)
```



## 九、Module

解决 state 对象繁杂的问题，分为模块

```js
const ModuleA = {}
const ModuleB = {}
const store = new Vuex.Store({
    // modules 相当于还是写了state
    modules: {
        a: ModuleA,
        b: ModuleB
    }
})

// 组件中使用
this.$store.state.a
```



## 十、mapGetters 辅助函数(其它的属性也有对应的映射方式)

将 vuex getters 中的属性，映射成为当前组件的计算属性中

```js
import { mapGetters } from 'vuex'
// mapGetters 参数：一个数组，存放store中的getter，然后在页面组件中可以直接使用
export default {
    computed: {
        ...mapGetters([])
    }
}
```





# 反向代理

![1568963102596](images/1568963102596.png)

+ 作用：解决跨域的方式(只有浏览器中有跨域问题)

  1. jsonp
  2. CORS 跨域资源共享
  3. 反向代理

+ 脚手架中配置 config/index.js

  配置反向代理(webpack-dev-server的配置项)

  ```js
  proxyTable: {
      '/api': {
          target: 'http://127.0.0.1:3000/', // 代理的目标服务器地址
          changeOrigin: true, // 是否跨域
          pathRewrite: {
              '^/api': '/' // 匹配以/api为开头的请求地址，并使用/替换(实际请求路径中不包含/api就以/替换)
          }
      }
  }
  ```

+ 参考文献

  https://www.jianshu.com/p/f489e7764cb8